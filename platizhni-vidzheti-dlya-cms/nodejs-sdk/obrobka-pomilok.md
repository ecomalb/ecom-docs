# Обробка помилок

SDK розділяє помилки валідації, підпису JWS і платіжних операцій. Перевіряйте тип помилки, її код та поточний стан операції перед повторним запитом.

### Класи помилок

| Поле                                                      | Тип                  | Опис                                                                                                     |
| --------------------------------------------------------- | -------------------- | -------------------------------------------------------------------------------------------------------- |
| `ValidationException`                                     | Error                | Дані не відповідають схемі. Масив errors містить пояснення. Цей клас не успадковує AllianceSdkException. |
| `JwsSigningException`                                     | AllianceSdkException | Не вдалося підписати запит. Перевірте приватний ключ, формат PKCS#8 PEM і kid.                           |
| `JwsVerificationException`                                | AllianceSdkException | Помилка отримання ключа банку або перевірки JWS. Не застосовуйте отримані дані до замовлення.            |
| `GeneralApiException`                                     | AllianceSdkException | Помилка HTTP/API. Зокрема, для HTTP 401 перевірте JWS-ключ і kid.                                        |
| `PaymentException`                                        | AllianceSdkException | Помилка створення платіжного замовлення.                                                                 |
| `RefundException`                                         | AllianceSdkException | Помилка повернення.                                                                                      |
| `CompletionException`                                     | AllianceSdkException | Помилка завершення PREAUTH.                                                                              |
| `CompletionAmountException`                               | AllianceSdkException | Сума COMPLETION відхиляється від PREAUTH більш ніж на ±20%.                                              |
| `CreatePlanException / UpdatePlanException`               | AllianceSdkException | Помилка створення або оновлення плану.                                                                   |
| `UpdatePlanStatusException`                               | AllianceSdkException | Помилка зміни статусу плану.                                                                             |
| `UpdatePlanVersionException / DeletePlanVersionException` | AllianceSdkException | Помилка роботи з версією плану.                                                                          |
| `GetPlanException / SearchPlansException`                 | AllianceSdkException | Помилка отримання або пошуку планів.                                                                     |
| `CreateSubscriptionOrderException`                        | AllianceSdkException | Помилка створення замовлення підписки.                                                                   |
| `CancelSubscriptionOrderException`                        | AllianceSdkException | Помилка скасування підписки.                                                                             |
| `TriggerRecurringPaymentException`                        | AllianceSdkException | Помилка запуску повторного платежу.                                                                      |

### Поля AllianceSdkException

| Поле            | Тип     | Опис                                                                              |
| --------------- | ------- | --------------------------------------------------------------------------------- |
| `message`       | string  | Текст помилки.                                                                    |
| `code`          | string  | Код SDK або API; використовуйте для розрізнення причин.                           |
| `originalError` | any     | Початкова помилка або дані відповіді.                                             |
| `rawPayload`    | unknown | Початкові дані помилки; у цьому класі містить те саме значення, що originalError. |

### Приклад обробки

```javascript
import {
    ValidationException,
    CompletionAmountException,
    JwsSigningException,
    JwsVerificationException,
    AllianceSdkException,
} from '@alliance-bank/payment-sdk';

export function reportSdkError(error) {
    if (error instanceof ValidationException) {
        console.error('Перевірте поля запиту:', error.errors);
    } else if (error instanceof CompletionAmountException) {
        console.error('Недопустима сума COMPLETION:', error.message);
    } else if (
        error instanceof JwsSigningException ||
        error instanceof JwsVerificationException
    ) {
        console.error('Помилка JWS:', error.code, error.message);
    } else if (error instanceof AllianceSdkException) {
        console.error('Помилка API:', error.code, error.message);
    } else {
        throw error;
    }
}

// У catch вашої платіжної операції викличте reportSdkError(error).
```

### Повторні запити та частковий результат

* Виправляйте `ValidationException` до повторної відправки.
* Після таймауту або обриву з’єднання спочатку звірте стан операції. Новий виклик SDK генерує новий `merchantRequestId` і може створити повторну операцію.
* Для `createPlanWithInfiniteSchedule` та `updatePlanWithInfiniteSchedule` додатково перевіряйте `result.isFullySuccessful()`. Помилка другого кроку повертається як частковий результат, без обов’язкового винятку.
* Зберігайте діагностику в захищеному журналі. Не виводьте приватні ключі, повні JWS або необроблені платіжні дані у відповідь покупцю.

Старий клас `AuthorizationException` не експортується з клієнта релізу v1.5.0. Для цієї версії використовуйте класи JWS/API з таблиці.
