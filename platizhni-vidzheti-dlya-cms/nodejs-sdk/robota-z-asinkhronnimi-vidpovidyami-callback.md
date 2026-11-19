# Робота з асинхронними відповідями Callback

Метод `client.handleCallback(rawBody)` розбирає повідомлення про PURCHASE, REFUND, A2A, PREAUTH та COMPLETION. Якщо передано compact JWS, SDK перевіряє підпис банку перед поверненням даних.

### Прийом підписаного callback

Зберігайте початкове тіло запиту як текст. Обробник `express.text()` для callback зареєструйте **до** загального `express.json()`. Нижче маршрут приймає тільки compact JWS: три частини через крапку — це перевірка формату; справжність підпису перевіряє SDK.

Функція `processPaymentOnce` у прикладі — ваша логіка роботи з базою, а не метод SDK. Вона має звірити мерчанта, замовлення, суму та валюту, а потім атомарно зберегти операцію й оновити статус без повторного нарахування.

```javascript
import express from 'express';
import { client } from './alliance-client.js';
import { processPaymentOnce } from './payment-store.js';

const app = express();

app.post(
    '/api/payment/callback',
    express.text({ type: '*/*', limit: '1mb' }),
    async (req, res) => {
        const rawBody = typeof req.body === 'string' ? req.body.trim() : '';
        if (!/^[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+$/.test(rawBody)) {
            return res.status(400).send('Очікується compact JWS');
        }

        let callback;
        try {
            callback = await client.handleCallback(rawBody);
        } catch {
            return res.status(400).send('Callback не пройшов перевірку');
        }

        try {
            await processPaymentOnce(callback);
            return res.status(200).send('OK');
        } catch {
            return res.status(500).send('Не вдалося зберегти результат');
        }
    },
);

// JSON-парсер для інших маршрутів — після callback-маршруту.
app.use(express.json());
```

SDK також допускає звичайний JSON, але розбір JSON не є перевіркою JWS-підпису. Якщо для вашої інтеграції банк надсилає JSON, перед зміною статусу звірте результат серверним запитом `checkOrderData(hppOrderId)`.

### Основні поля CallbackDto

| Поле                     | Тип            | Опис                                                                |
| ------------------------ | -------------- | ------------------------------------------------------------------- |
| `hppOrderId`             | string         | Ідентифікатор HPP-замовлення. Зіставте із замовленням у вашій базі. |
| `ecomOrderId`            | string         | Ідентифікатор замовлення в e-commerce API.                          |
| `merchantId`             | string         | Ідентифікатор мерчанта.                                             |
| `merchantRequestId`      | string         | Ідентифікатор запиту створення.                                     |
| `orderStatus`            | string         | Статус замовлення.                                                  |
| `coinAmount`             | number         | Сума замовлення у найменших одиницях його валюти.                   |
| `paymentMethods`         | string\[]      | Способи оплати.                                                     |
| `statusUrl`              | string \| null | Посилання на сторінку статусу.                                      |
| `redirectUrl`            | string         | Посилання на платіжну сторінку.                                     |
| `notificationUrl`        | string         | Адреса повідомлення.                                                |
| `notificationEncryption` | boolean        | Необов’язково. Параметр повідомлення у відповіді.                   |
| `createDate`             | string \| Date | Необов’язково. Дата створення замовлення.                           |
| `expiredOrderDate`       | string \| Date | Необов’язково. Строк дії замовлення.                                |
| `operation`              | object         | Дані операції, через яку надійшло повідомлення.                     |

### Основні поля operation

| Поле                  | Тип                   | Опис                                                                                               |
| --------------------- | --------------------- | -------------------------------------------------------------------------------------------------- |
| `type`                | string                | PURCHASE, REFUND, A2A, PREAUTH або COMPLETION.                                                     |
| `status`              | string                | Статус операції. Для успішної операції — SUCCESS.                                                  |
| `operationId`         | string                | Необов’язково за схемою. Зберігайте, якщо отримано; потрібен для повернення та завершення PREAUTH. |
| `ecomOperationId`     | string                | Ідентифікатор операції в e-commerce API; зберігайте для звірки та захисту від повторної обробки.   |
| `coinAmount`          | number                | Сума операції у найменших одиницях transactionCurrency.                                            |
| `transactionCurrency` | string                | Валюта операції.                                                                                   |
| `creationDateTime`    | string \| Date        | Необов’язково. Час створення операції.                                                             |
| `preauthOperationId`  | string \| null        | Необов’язково для COMPLETION. Посилання на оригінальну PREAUTH.                                    |
| `preauthCoinAmount`   | number (ціле) \| null | Необов’язково для COMPLETION. Сума оригінальної PREAUTH.                                           |

### Правила зміни статусу

* Для `PURCHASE`, `A2A` і `COMPLETION` враховуйте `status === 'SUCCESS'` та перевірені дані операції.
* Для успішної `PREAUTH` зберігайте авторизацію, її суму та `operationId`; списання виконується окремим COMPLETION.
* Для успішного `REFUND` враховуйте суму повернення окремо від початкової оплати.
* Повторний callback обробляйте без повторного нарахування. Зберігайте ідентифікатор операції та її стан, щоб повтори не блокували допустиме оновлення статусу.
* Відповідайте HTTP 200 після збереження результату. Помилка бази має залишати можливість повторної доставки.

Не використовуйте неперевірені дані callback для видачі товару чи послуги.
