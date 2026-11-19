# Створення замовлення

Метод `client.createOrder(orderData)` створює HPP-замовлення й повертає посилання на сторінку оплати. SDK сам додає `merchantId` та генерує `merchantRequestId`.

### Поля orderData

| Поле                     | Тип               | Опис                                                                                                                                    |
| ------------------------ | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `coinAmount`             | number (ціле)     | Обов’язково. Додатна сума у найменших одиницях валюти замовлення. Для UAH: 10050 = 100,50 грн.                                          |
| `currencyCode`           | number            | Необов’язково. 980 — UAH (за замовчуванням), 840 — USD, 978 — EUR. Для A2A дозволено лише 980.                                          |
| `hppPayType`             | string            | Обов’язково. PURCHASE — оплата, PREAUTH — попередня авторизація, A2A — переказ між рахунками.                                           |
| `paymentMethods`         | string\[]         | Обов’язково. Непорожній список способів оплати, доступних вашому мерчанту, наприклад CARD, APPLE\_PAY, GOOGLE\_PAY.                     |
| `successUrl`             | string            | Обов’язково. URL повернення покупця після успішної оплати, до 1000 символів.                                                            |
| `failUrl`                | string            | Обов’язково. URL повернення покупця у разі невдалої оплати, до 1000 символів.                                                           |
| `statusPageType`         | string            | Обов’язково. Тип сторінки статусу, наприклад STATUS\_TIMER\_PAGE.                                                                       |
| `customerData`           | object            | Обов’язково. Дані покупця; мінімально містить senderCustomerId.                                                                         |
| `notificationUrl`        | string            | Необов’язково. Публічна URL-адреса вашого обробника callback, до 255 символів.                                                          |
| `notificationEncryption` | boolean \| string | Необов’язково. Параметр формату повідомлень. Значення узгодьте з банком; перевірку JWS виконуйте за фактичним форматом тіла.            |
| `directType`             | string            | Необов’язково для PURCHASE; обов’язково для A2A. REDIRECT або BANK\_LINK.                                                               |
| `priorityBankCode`       | string            | Необов’язково. Код пріоритетного банку; у прикладі A2A використано ALL\_BANKS.                                                          |
| `merchantComment`        | string            | Коментар мерчанта, до 255 символів. Обов’язково для A2A.                                                                                |
| `purpose`                | string            | Необов’язково. Призначення платежу, до 255 символів.                                                                                    |
| `expirationTimeMinutes`  | number (ціле)     | Необов’язково. Строк дії замовлення: від 60 до 1440 хвилин.                                                                             |
| `language`               | string            | Необов’язково. Мова платіжної сторінки, до 50 символів.                                                                                 |
| `hppTryMode`             | string            | Необов’язково. Режим спроб HPP; використовуйте значення, погоджене для вашої інтеграції.                                                |
| `preAuthExpDate`         | string \| null    | Для PREAUTH. Якщо не передати, SDK встановить поточний час + 2 години 30 секунд. Формат і межі наведено на сторінці PREAUTH/COMPLETION. |
| `hppPageAdditionalInfo`  | object \| null    | Необов’язково. Деталі товарів: productsSum та products.                                                                                 |
| `paymentCategoryGoal`    | string            | Необов’язково. Категорія / ціль платежу.                                                                                                |
| `generateQrNbu`          | boolean           | Необов’язково. Запит на формування QR НБУ; за замовчуванням false.                                                                      |
| `merchantId`             | string            | SDK додає з налаштувань клієнта.                                                                                                        |
| `merchantRequestId`      | string            | SDK генерує для кожного виклику createOrder.                                                                                            |

### Основні поля customerData

| Поле               | Тип    | Опис                                                                                 |
| ------------------ | ------ | ------------------------------------------------------------------------------------ |
| `senderCustomerId` | string | Обов’язково. Постійний ідентифікатор покупця у вашій системі, від 1 до 255 символів. |
| `senderFirstName`  | string | Необов’язково. Ім’я, до 30 символів.                                                 |
| `senderLastName`   | string | Необов’язково. Прізвище, до 30 символів.                                             |
| `senderEmail`      | string | Необов’язково. Коректна email-адреса, до 256 символів.                               |
| `senderPhone`      | string | Необов’язково. Номер телефону, до 20 символів.                                       |
| `senderIp`         | string | Необов’язково. Коректна IPv4- або IPv6-адреса.                                       |

### Приклад PURCHASE

```javascript
import { client } from './alliance-client.js';

const orderData = {
    coinAmount: 10050, // Сума в копійках: 10050 = 100,50 грн
    currencyCode: 980,
    hppPayType: 'PURCHASE',
    directType: 'REDIRECT',
    paymentMethods: ['CARD', 'APPLE_PAY', 'GOOGLE_PAY'],
    successUrl: 'https://your-site.com/payment/success',
    failUrl: 'https://your-site.com/payment/fail',
    notificationUrl: 'https://your-site.com/api/payment/callback',
    statusPageType: 'STATUS_TIMER_PAGE',
    customerData: { senderCustomerId: 'customer_id_1' },
};

try {
    const response = await client.createOrder(orderData);
    console.log('HPP Order ID:', response.hppOrderId);
    console.log('Посилання на оплату:', response.redirectUrl);
} catch (error) {
    console.error('Не вдалося створити замовлення:', error.message);
}
```

Збережіть `hppOrderId` разом із номером замовлення у своїй базі та перенаправте покупця на `redirectUrl`. Повернення на `successUrl` саме по собі не підтверджує зарахування коштів: перевіряйте callback або стан замовлення через API.

### Приклад A2A

> **A2A платіж:** щоб використати наведений вище приклад для A2A, задайте `hppPayType: 'A2A'` та змініть такі параметри:
>
> * `directType: 'BANK_LINK'` — для A2A. Для `PURCHASE` використовується `directType: 'REDIRECT'`.
> * `priorityBankCode: 'ALL_BANKS'` — передайте це значення в запиті A2A.
> * `merchantComment: 'Оплата замовлення №1001'` — **обов’язкове поле для A2A.** Вкажіть коментар для свого замовлення.
> * `currencyCode: 980` — A2A підтримує лише гривню (UAH).

```javascript
const a2aOrder = await client.createOrder({
    ...orderData,
    hppPayType: 'A2A',
    currencyCode: 980,
    directType: 'BANK_LINK',
    priorityBankCode: 'ALL_BANKS',
    merchantComment: 'Оплата замовлення №1001',
});
```

Для A2A SDK перевіряє наявність `directType` і `merchantComment`. Валюта, відмінна від 980, спричинить `ValidationException`.

### Платежі в USD та EUR

Валюта має бути доступна вашому мерчанту. `coinAmount` завжди передається цілим числом у найменших одиницях вибраної валюти.

```javascript
// Використовується orderData з попереднього прикладу.
// USD: 1050 центів = 10,50 USD.
const usdOrder = await client.createOrder({
    ...orderData,
    currencyCode: 840,
    coinAmount: 1050,
});

// EUR: 2000 центів = 20,00 EUR.
const eurOrder = await client.createOrder({
    ...orderData,
    currencyCode: 978,
    coinAmount: 2000,
});
```

### Поля відповіді OrderResponseDto

| Поле                | Тип            | Опис                                                                    |
| ------------------- | -------------- | ----------------------------------------------------------------------- |
| `hppOrderId`        | string         | Ідентифікатор HPP-замовлення. Зберігайте для callback і checkOrderData. |
| `merchantRequestId` | string         | Ідентифікатор запиту, згенерований SDK.                                 |
| `hppPayType`        | string         | Тип платежу.                                                            |
| `paymentMethods`    | string\[]      | Доступні способи оплати.                                                |
| `orderStatus`       | string         | Поточний статус замовлення.                                             |
| `coinAmount`        | number         | Сума у найменших одиницях валюти замовлення.                            |
| `merchantId`        | string         | Ідентифікатор мерчанта.                                                 |
| `redirectUrl`       | string         | URL платіжної сторінки.                                                 |
| `statusUrl`         | string \| null | Посилання на сторінку статусу.                                          |
| `nbuQrCode`         | string \| null | Необов’язково. Посилання на QR НБУ.                                     |
| `createDate`        | string \| Date | Необов’язково. Час створення.                                           |
| `expiredOrderDate`  | string \| Date | Необов’язково. Строк дії замовлення.                                    |

Поля, позначені як необов’язкові, можуть бути відсутні у відповіді. Зберігайте отримані ідентифікатори разом із замовленням у вашій системі.

Повний опис параметрів API: [Створення замовлення HPP](https://docs.merchant.alb.ua/platizhni-metodi-hpp/stvorennya-zamovlennya/stvorennya-zamovlennya).

| Поле                | Тип            | Опис                                                                    |
| ------------------- | -------------- | ----------------------------------------------------------------------- |
| `hppOrderId`        | string         | Ідентифікатор HPP-замовлення. Зберігайте для callback і checkOrderData. |
| `merchantRequestId` | string         | Ідентифікатор запиту, згенерований SDK.                                 |
| `hppPayType`        | string         | Тип платежу.                                                            |
| `paymentMethods`    | string\[]      | Доступні способи оплати.                                                |
| `orderStatus`       | string         | Поточний статус замовлення.                                             |
| `coinAmount`        | number         | Сума у найменших одиницях валюти замовлення.                            |
| `merchantId`        | string         | Ідентифікатор мерчанта.                                                 |
| `redirectUrl`       | string         | URL платіжної сторінки.                                                 |
| `statusUrl`         | string \| null | Посилання на сторінку статусу.                                          |
| `nbuQrCode`         | string \| null | Необов’язково. Посилання на QR НБУ.                                     |
| `createDate`        | string \| Date | Необов’язково. Час створення.                                           |
| `expiredOrderDate`  | string \| Date | Необов’язково. Строк дії замовлення.                                    |
