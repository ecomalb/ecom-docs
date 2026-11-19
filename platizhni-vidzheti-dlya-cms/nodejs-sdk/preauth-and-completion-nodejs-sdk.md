---
description: >-
  PREAUTH дозволяє заморозити кошти на картці клієнта без їх фактичного
  списання. Кошти утримуються до моменту виконання COMPLETION або закінчення
  терміну дії авторизації.
---

# PreAuth and Completion NodeJS SDK

PREAUTH резервує кошти, а COMPLETION завершує авторизацію списанням. Виконуйте COMPLETION після підтвердженої успішної PREAUTH.

### Попередня авторизація PREAUTH

| Поле              | Тип            | Опис                                                                                                   |
| ----------------- | -------------- | ------------------------------------------------------------------------------------------------------ |
| `hppPayType`      | string         | Передайте PREAUTH у createOrder.                                                                       |
| `coinAmount`      | number (ціле)  | Обов’язково. Сума попередньої авторизації у найменших одиницях валюти. У прикладі 25000 = 250,00 грн.  |
| `currencyCode`    | number         | У прикладі 980 (UAH).                                                                                  |
| `preAuthExpDate`  | string \| null | Необов’язково. Строк дії авторизації. За відсутності SDK встановлює поточний час + 2 години 30 секунд. |
| `paymentMethods`  | string\[]      | Обов’язково. У прикладі — CARD.                                                                        |
| `successUrl`      | string         | Обов’язково. URL успішного повернення покупця.                                                         |
| `failUrl`         | string         | Обов’язково. URL повернення після помилки.                                                             |
| `statusPageType`  | string         | Обов’язково. У прикладі STATUS\_TIMER\_PAGE.                                                           |
| `customerData`    | object         | Обов’язково. Мінімум senderCustomerId.                                                                 |
| `notificationUrl` | string         | Необов’язково. URL обробника повідомлень про результат.                                                |

Якщо передаєте `preAuthExpDate` вручну, використовуйте формат `YYYY-MM-DD HH:mm:ss.SS±HH:MM`. Дата має бути **строго пізніше ніж через 2 години та раніше ніж через 28 днів** від поточного моменту. Нижче SDK обчислює її автоматично.

```javascript
import { client } from './alliance-client.js';

const order = await client.createOrder({
    coinAmount: 25000,
    currencyCode: 980,
    hppPayType: 'PREAUTH',
    paymentMethods: ['CARD'],
    successUrl: 'https://your-site.com/payment/success',
    failUrl: 'https://your-site.com/payment/fail',
    notificationUrl: 'https://your-site.com/api/payment/callback',
    statusPageType: 'STATUS_TIMER_PAGE',
    customerData: { senderCustomerId: 'customer_id_1' },
});

console.log('ID замовлення:', order.hppOrderId);
console.log('Посилання на оплату:', order.redirectUrl);
```

Збережіть `hppOrderId`. Після перевіреного callback із `operation.type === 'PREAUTH'` та `operation.status === 'SUCCESS'` збережіть `operation.operationId` і `operation.coinAmount`. Вони потрібні для COMPLETION.

### Завершення авторизації COMPLETION

Виклик: `client.createCompletion(data, originalCoinAmount)`. Допустима сума списання — у межах ±20% від підтвердженої суми PREAUTH. Для 25000 копійок це від 20000 до 30000 копійок.

| Поле                  | Тип           | Опис                                                                                                                 |
| --------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------- |
| `originalOperationId` | string        | Обов’язково. operationId успішної PREAUTH.                                                                           |
| `coinAmount`          | number (ціле) | Додатна сума списання в копійках; має пройти перевірку ±20%. Може бути замінена парою sourceAmount + conversionRate. |
| `notificationUrl`     | string        | Необов’язково. URL callback про результат.                                                                           |
| `sourceAmount`        | number        | Необов’язково. Сума в основних одиницях вихідної валюти для перерахунку в UAH.                                       |
| `conversionRate`      | number        | Необов’язково. Курс перерахунку в UAH; передається разом із sourceAmount.                                            |
| `merchantId`          | string        | SDK додає з налаштувань.                                                                                             |
| `merchantRequestId`   | string        | SDK генерує для кожного виклику.                                                                                     |
| `date`                | string        | SDK автоматично формує дату запиту.                                                                                  |
| `originalCoinAmount`  | number        | Обов’язковий другий аргумент методу, поза об’єктом data. Підтверджена сума оригінальної PREAUTH в копійках.          |

```javascript
import {
    CompletionAmountException,
    AllianceSdkException,
} from '@alliance-bank/payment-sdk';
import { client } from './alliance-client.js';

const originalCoinAmount = 25000; // Збережена сума успішної PREAUTH

try {
    const result = await client.createCompletion(
        {
            originalOperationId: 'PREAUTH_OPERATION_ID',
            coinAmount: 24000,
            notificationUrl: 'https://your-site.com/api/payment/callback',
        },
        originalCoinAmount,
    );

    console.log('Статус списання:', result.status);
    console.log('ID операції:', result.ecomOperationId);
} catch (error) {
    if (error instanceof CompletionAmountException) {
        console.error('Сума виходить за допустимі межі:', error.message);
    } else if (error instanceof AllianceSdkException) {
        console.error('Помилка SDK:', error.code, error.message);
    } else {
        throw error;
    }
}
```

### Списання з перерахунком у UAH

Пара `sourceAmount` + `conversionRate` має пріоритет над `coinAmount`. Перевірка ±20% застосовується до результату `Math.round(sourceAmount * conversionRate * 100)`. Другий аргумент залишається сумою оригінальної PREAUTH в копійках.

```javascript
const result = await client.createCompletion(
    {
        originalOperationId: 'PREAUTH_OPERATION_ID',
        sourceAmount: 6.00,
        conversionRate: 41.20,
    },
    25000,
);
// 6,00 × 41,20 × 100 = 24720 копійок.
// 24720 перебуває у дозволеному діапазоні 20000–30000.
```

### Основні поля CompletionResponseDto

| Поле                      | Тип                   | Опис                                                    |
| ------------------------- | --------------------- | ------------------------------------------------------- |
| `status`                  | string                | Статус операції списання.                               |
| `ecomOperationId`         | string                | Ідентифікатор операції COMPLETION в e-commerce API.     |
| `operationId`             | string \| null        | Необов’язково. Ідентифікатор операції.                  |
| `hppOrderId`              | string                | Пов’язане HPP-замовлення.                               |
| `coinAmount`              | number (ціле)         | Сума списання у найменших одиницях transactionCurrency. |
| `transactionCurrency`     | string                | Валюта операції.                                        |
| `preauthOperationId`      | string \| null        | Необов’язково. Ідентифікатор початкової PREAUTH.        |
| `preauthCoinAmount`       | number (ціле) \| null | Необов’язково. Сума початкової PREAUTH.                 |
| `preauthEcomOperationId`  | string \| null        | Необов’язково. E-commerce ідентифікатор PREAUTH.        |
| `transactionResponseInfo` | object                | Додаткові дані про результат.                           |

Змінюйте статус замовлення на оплачене після перевірки успішного результату списання. Успішна PREAUTH сама по собі означає резервування коштів.

