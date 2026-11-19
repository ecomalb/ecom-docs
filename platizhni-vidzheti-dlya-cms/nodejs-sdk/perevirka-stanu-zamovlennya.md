# Перевірка стану замовлення

Метод `client.checkOrderData(hppOrderId)` повертає стан HPP-замовлення та історію операцій. Використовуйте його для звірки, зокрема після втрати callback або закриття покупцем сторінки оплати.

### Параметр методу

| Поле         | Тип    | Опис                                                                      |
| ------------ | ------ | ------------------------------------------------------------------------- |
| `hppOrderId` | string | Обов’язково. Ідентифікатор HPP-замовлення, отриманий під час createOrder. |

### Приклад перевірки

```javascript
import { client } from './alliance-client.js';

try {
    const order = await client.checkOrderData('HPP_ORDER_ID');

    console.log('Статус замовлення:', order.orderStatus);
    for (const operation of order.operations) {
        console.log({
            type: operation.type,
            status: operation.status,
            operationId: operation.operationId,
            ecomOperationId: operation.ecomOperationId,
            coinAmount: operation.coinAmount,
        });
    }
} catch (error) {
    console.error('Помилка перевірки замовлення:', error.message);
}
```

### Поля OrderDataResponseDto

| Поле                | Тип                    | Опис                                                          |
| ------------------- | ---------------------- | ------------------------------------------------------------- |
| `hppOrderId`        | string                 | Ідентифікатор HPP-замовлення.                                 |
| `ecomOrderId`       | string                 | Ідентифікатор замовлення в e-commerce API.                    |
| `merchantId`        | string                 | Ідентифікатор мерчанта.                                       |
| `merchantRequestId` | string                 | Ідентифікатор запиту створення.                               |
| `hppPayType`        | string                 | Тип платежу.                                                  |
| `orderStatus`       | string                 | Статус замовлення.                                            |
| `coinAmount`        | number                 | Сума замовлення у найменших одиницях його валюти.             |
| `paymentMethods`    | string\[]              | Способи оплати.                                               |
| `operations`        | object\[]              | Історія операцій: PURCHASE, REFUND, A2A, PREAUTH, COMPLETION. |
| `statusUrl`         | string \| null         | Необов’язково. URL сторінки статусу.                          |
| `redirectUrl`       | string \| null         | Необов’язково. URL платіжної сторінки.                        |
| `notificationUrl`   | string \| null         | Необов’язково. URL callback.                                  |
| `createDate`        | string \| Date \| null | Необов’язково. Час створення.                                 |
| `expiredOrderDate`  | string \| Date \| null | Необов’язково. Строк дії замовлення.                          |

### Основні поля operations\[]

| Поле                      | Тип            | Опис                                                                                                                                                    |
| ------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`                    | string         | Тип конкретної операції.                                                                                                                                |
| `status`                  | string         | Статус конкретної операції, наприклад SUCCESS.                                                                                                          |
| `operationId`             | string         | Необов’язково. Ідентифікатор операції; потрібен для подальшого повернення або COMPLETION.                                                               |
| `ecomOperationId`         | string         | Ідентифікатор операції в e-commerce API.                                                                                                                |
| `coinAmount`              | number         | Сума операції у найменших одиницях transactionCurrency.                                                                                                 |
| `transactionCurrency`     | string         | Валюта операції.                                                                                                                                        |
| `sourceAmount`            | number (ціле)  | Необов’язково. Вихідна сума, отримана від API. Одиниці звіряйте з контрактом операції; не прирівнюйте це поле до вхідного sourceAmount для конвертації. |
| `sourceCurrencyCode`      | number (ціле)  | Необов’язково. Код вихідної валюти.                                                                                                                     |
| `conversionRate`          | number         | Необов’язково. Курс конвертації.                                                                                                                        |
| `creationDateTime`        | string \| Date | Необов’язково. Час створення операції.                                                                                                                  |
| `transactionResponseInfo` | object         | Додаткові відомості про результат.                                                                                                                      |

Звіряйте `merchantId`, `hppOrderId`, суму, валюту, тип і статус операції з даними вашого замовлення. Успішна PREAUTH означає авторизацію коштів; факт списання підтверджуйте за успішною PURCHASE або COMPLETION, а для A2A — за відповідною успішною операцією.
