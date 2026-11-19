# Виконання повернень

Метод `client.createRefund(data)` ініціює повне або часткове повернення за успішною операцією. SDK автоматично формує `merchantId`, `merchantRequestId` та `date`.

### Поля запиту на повернення

| Поле                     | Тип            | Опис                                                                                                                    |
| ------------------------ | -------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `operationId`            | string         | Обов’язково. Ідентифікатор успішної операції оплати, за якою повертаються кошти. Це не hppOrderId.                      |
| `coinAmount`             | number         | Додатна сума повернення в копійках. Передайте ціле число; може бути замінена парою sourceAmount + conversionRate.       |
| `sourceAmount`           | number         | Необов’язково. Сума в основних одиницях вихідної валюти, наприклад 10.50 USD. Використовується разом із conversionRate. |
| `conversionRate`         | number         | Необов’язково. Курс перерахунку вихідної валюти в UAH. Використовується разом із sourceAmount.                          |
| `merchantComment`        | string         | Необов’язково. Коментар до повернення.                                                                                  |
| `notificationUrl`        | string         | Необов’язково. URL callback-обробника результату.                                                                       |
| `notificationEncryption` | string         | Необов’язково. Параметр повідомлення у схемі RefundRequestDto цього релізу.                                             |
| `merchantId`             | string         | SDK підставляє з налаштувань.                                                                                           |
| `merchantRequestId`      | string         | SDK генерує для кожного виклику.                                                                                        |
| `date`                   | string \| Date | SDK формує дату запиту.                                                                                                 |

### Приклад часткового повернення

```javascript
import { client } from './alliance-client.js';

try {
    const result = await client.createRefund({
        operationId: 'ORIGINAL_OPERATION_ID',
        coinAmount: 500, // 5,00 грн
        merchantComment: 'Часткове повернення',
        notificationUrl: 'https://your-site.com/api/payment/callback',
    });
    console.log('Статус повернення:', result.status);
    console.log('ID операції:', result.ecomOperationId);
} catch (error) {
    console.error('Помилка повернення:', error.message);
}
```

### Перерахунок валютної суми

Якщо передані обидва поля `sourceAmount` та `conversionRate`, SDK розраховує `coinAmount = Math.round(sourceAmount * conversionRate * 100)`. Ця пара має пріоритет над явно заданим `coinAmount`. Передавайте курс, що відповідає операції.

```javascript
const result = await client.createRefund({
    operationId: 'ORIGINAL_OPERATION_ID',
    sourceAmount: 10.50,
    conversionRate: 41.20,
    merchantComment: 'Повернення з перерахунком у UAH',
});
// Сума запиту: 43260 копійок = 432,60 грн.
```

### Основні поля RefundResponseDto

| Поле                      | Тип            | Опис                                                    |
| ------------------------- | -------------- | ------------------------------------------------------- |
| `status`                  | string         | Статус операції повернення.                             |
| `type`                    | string         | Тип операції.                                           |
| `operationId`             | string \| null | Необов’язково. Ідентифікатор операції.                  |
| `ecomOperationId`         | string         | Ідентифікатор операції в e-commerce API.                |
| `hppOrderId`              | string         | Ідентифікатор пов’язаного HPP-замовлення.               |
| `merchantRequestId`       | string         | Ідентифікатор запиту.                                   |
| `coinAmount`              | number         | Сума операції у найменших одиницях transactionCurrency. |
| `transactionCurrency`     | string         | Валюта операції.                                        |
| `originalOperationId`     | string         | Необов’язково. Ідентифікатор початкової операції.       |
| `originalCoinAmount`      | number         | Необов’язково. Сума початкової операції.                |
| `transactionResponseInfo` | object         | Додаткові відомості про результат.                      |
| `creationDateTime`        | string \| Date | Час створення операції.                                 |
| `modificationDateTime`    | string \| Date | Час останньої зміни.                                    |

Збережіть ідентифікатори та перевірте фактичний статус повернення у відповіді, callback або через перевірку замовлення. Успішне виконання HTTP-запиту ще не означає успішне повернення.
