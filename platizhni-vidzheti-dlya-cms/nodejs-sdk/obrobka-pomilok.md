# Обробка помилок

SDK використовує типізовані помилки для точного визначення причини відмови.

| **Клас помилки**         | **Опис**                                                                              |
| ------------------------ | ------------------------------------------------------------------------------------- |
| `ValidationException`    | Дані не пройшли перевірку за схемою DTO (відсутні обов'язкові поля або невірний тип). |
| `AuthorizationException` | Помилки авторизації, невірні ключі або прострочені сесії.                             |
| `PaymentException`       | Помилки на рівні платіжної логіки (наприклад, недостатньо коштів для повернення).     |
| `AllianceSdkException`   | Базовий клас для всіх кастомних помилок SDK.                                          |

**Приклад перевірки помилок:**

```
import { ValidationException, AllianceSdkException } from '@alliancepay/sdk-nodejs';

try {
    await client.createOrder(orderData);
} catch (error) {
    if (error instanceof ValidationException) {
        // error.errors містить масив усіх знайдених помилок валідації DTO
        console.error('Validation errors:', error.errors);
    } else if (error instanceof AllianceSdkException) {
        // Обробка бізнес-помилок банку
        console.error(`Bank Error Code: ${error.code}`); // напр. 'b_terminal_not_found'
        console.error(`Message: ${error.message}`);
        console.error(`Raw Response Data:`, error.originalError); // Тіло відповіді банку
    } else {
        console.error('Unexpected system error:', error);
    }
}
```
