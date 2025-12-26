---
description: '{{url}}/ecom/execute_request/hpp/v1/create-order'
---

# Створення замовлення

**Вхідні параметри:**

<table data-full-width="true"><thead><tr><th width="173">Параметр</th><th width="162">Опиc</th><th width="130.1038818359375">Формат даних</th><th width="116.399169921875">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>hppPayType</td><td>тип оплати</td><td>string</td><td>Так</td><td>Доступні значення -PURCHASE, A2A</td></tr><tr><td>directType</td><td>спосіб перенаправлення клієнта на платіжні сторінку</td><td>enum</td><td>Ні</td><td><p></p><ul><li>REDIRECT - (по замовчуванню) редірект на сторінку HPP</li><li>BANK_LINK - редірект в мобільний додаток</li></ul></td></tr><tr><td>expirationTimeMinutes</td><td>термін дії посилання</td><td><p>int (4) (значення передається в хвилинах)</p><ul><li>max значення 1440 хвилин </li><li>min значення 60 хвилин для hppPayType = A2A</li></ul></td><td>Ні</td><td>1440 </td></tr><tr><td>coinAmount</td><td>сума замовлення в копійках</td><td>long</td><td>Так</td><td>2000</td></tr><tr><td>paymentMethods</td><td>методи оплати </td><td>enum</td><td>Так</td><td>Доступні значення - CARD, APPLE_PAY, GOOGLE_PAY</td></tr><tr><td>language</td><td>мова платіжного віджета. ISO 639-1 2 digits</td><td>string (50)</td><td>Ні</td><td><p>Доступні значення : uk(за замовчуванням)</p><p>en,es,de,pl,fr,tr,it,nl,pt</p></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</td></tr><tr><td>successUrl</td><td>url, для редіректу на сайт мерчанту при успішному статусі </td><td>string (1000)</td><td>Так </td><td><p><a href="https://example.com/success">https://example.com/success</a></p><p></p></td></tr><tr><td>failUrl</td><td>url, для редіректу на сайт мерчанту при неуспішному статусі</td><td>string (1000)</td><td>Так</td><td><a href="https://example.com/fail">https://example.com/fail</a></td></tr><tr><td>statusPageType</td><td>тип сторінки статусу </td><td>enum</td><td>Так</td><td><p></p><p>Доступні значення: </p><ol><li>STATUS_TIMER_PAGE - сторінка за замовчуванням, якщо мерчант не обрав бажаний тип, таймер редірект автоматично 1 хвилина відображення статус сторінки з автоматичним редіректом юзера на сайт мерчанта (редірект урл)</li><li>STATUS_REDIRECT_MERCHANT_PAGE - одразу редірект на урл мерчанта</li><li>STATUS_PAGE - редірект, на нашу статус сторіншку (завантажити квитанцію …)</li></ol></td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$ <br><br>min 14, max 255 символів для hppPayType = A2A</p></td><td>Так, якщо hppPayType = A2A</td><td>merchant Comment id 1258728c1</td></tr><tr><td>priorityBankCode</td><td>id пріоритетного застосунку. Для генераціі QR НБУ</td><td>string</td><td>Ні</td><td><p>PRIVAT_BANK </p><p><a href="../../dovidniki/dovidnik-prioritybankcode.md">Доступні значення</a></p></td></tr><tr><td>paymentCategoryGoal</td><td>категорія ціль. Для генераціі QR НБУ</td><td>string</td><td>Ні</td><td>MP2B/OTHR</td></tr><tr><td>generateQrNbu</td><td>ознака генераціі QR НБУ</td><td>boolean</td><td>Ні</td><td>true|false, default = false</td></tr><tr><td>customerData</td><td>об'єкт з customer даними </td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>не може містити “NULL”, “3D SECURE”, “SURNAME”, “CARDHOLDER”, ”UNKNOWN”</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника </td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td>IPv4 адреса відправника</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>Індекс відправника</td><td>string (50)</td><td>Ні</td><td> 49000</td></tr></tbody></table>

**Вихідні параметри:**

| Параметр          | Опис                                                                                                                                      | Формат даних | Приклад                                                                                                                                                                                                                                                                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| hppOrderId        | Id замовлення                                                                                                                             | string       | 1764688635274xVtoUo7bDcn                                                                                                                                                                                                                                                                                                                        |
| merchantRequestId | унікальний ідентифікатор мерчанта                                                                                                         | string       | 64d9304-0368-11ed-b939-0242ac1221458                                                                                                                                                                                                                                                                                                            |
| hppPayType        | тип оплати                                                                                                                                | string       | PURCHASE, A2A                                                                                                                                                                                                                                                                                                                                   |
| paymentMethods    | методи оплати                                                                                                                             | enum         | CARD                                                                                                                                                                                                                                                                                                                                            |
| orderStatus       | статус замовлення                                                                                                                         | string       | SUCCESS, FAIL, PENDING, REQUIRED\_3DS, CANCELED, PARTIAL\_REFUND                                                                                                                                                                                                                                                                                |
| coinAmount        | сума замовлення в копійках                                                                                                                | long         | 2000                                                                                                                                                                                                                                                                                                                                            |
| merchantId        | Id мерчанту згенерований в Єкомі                                                                                                          | string       | 37d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                                                                                                                                                             |
| expiredOrderDate  | дата та час дії замовлення                                                                                                                | string       | 2024-09-05 18:35:18.210+03:00                                                                                                                                                                                                                                                                                                                   |
| redirectUrl       | <ul><li>посилання на перенаправлення клієнта на hpp сторінку </li><li>посилання на перенаправлення клієнта в мобільний додаток </li></ul> | string       | <ul><li>{{url}}/?hpp_id=1728551936236-DAfCP7wrKT</li><li>{{url}}/?redirectUrl=https%3A%2F%2Fbankalliance.go.link%2Fecomc2a%3Forder_id%3D1762950448860FERkLl76lCp%26adj_t%3D1rknh2ig%26adj_deep_link%3Dbankalliance%253A%252F%252Fecomc2a%253Forder_id%253D1762950448860FERkLl76lCp</li></ul>                                                    |
| createDate        | дата та час створення замовлення                                                                                                          | string       | 2024-09-05 18:35:18.210+03:00                                                                                                                                                                                                                                                                                                                   |
| statusUrl         | url для редіректу на сторінку статусу                                                                                                     | string       | \{{url\}}/?hpp\_id=1728551936236-DAfCP7wrKT                                                                                                                                                                                                                                                                                                     |
| nbuQrCode         | url редіректу для відображення QR НБУ. Default: [https://bank.gov.ua/qr/](https://bank.gov.ua/qr)                                         | string       | https://bank.gov.ua/qr/QkNECjAwMwoxCklDVAoK0JrQvtCy0LDQu9GM0YHRjNC60LjQuSDQktC70LDQtNC40YHQu9Cw0LIg0KLQtdGB0YIKVUExMjMyMjAwMTAwMDAwMjYyMDYzNjM1MDU1MTMKVUFIMTAuMDAKMzQ2NzgwODE1MApNUDJCL09USFIKMTc2Mjk1MDQ0ODg2MEZFUmtMbDc2bENwCjEzN2Q5MzA0LTAzNjgtMTE9ZWI5MzkKUGF5bWVudCBmb3IgT3JkZXIg4oSWMTIzNDU2CkZGRkYKMjUxMTEyMTQ0MjI4CjI1MTExMjE0MjcyOAoK |

**Приклад тіла запиту hppPayType = PURCHASE:**

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "hppPayType": "PURCHASE",
    "directType": "REDIRECT",
    "failUrl": "https://example.com/fail",
    "successUrl": "https://example.com/success",
    "merchantRequestId": "137d93491081eb",
    "merchantComment": "12",
    "statusPageType": "STATUS_PAGE",
    "expirationTimeMinutes": 1440,
    "paymentMethods": [
        "CARD",
        "APPLE_PAY",
        "GOOGLE_PAY"
    ],
    "customerData": {
        "senderCustomerId": "Id", 
        "senderEmail": "aaaa@gmail.com",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStret",
        "senderCity": "senderCity",
        "senderIp": "255.255.244.255",
        "senderBirthday": "22081989",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "senderPassport",
        "senderItn": "5555557777",
        "senderPhone": "380957388888"
    },
    "coinAmount": 1000,
    "purpose": "Payment for Order №123456",
    "language": "uk",
    "notificationUrl": "https://example.com/notify"
}
```

**Приклад тіла відповіді hppPayType = PURCHASE:**

```json
{
    "coinAmount": 1000,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "statusUrl": "https://defe-status-page.develop.bankalliance.ua/?hpp_id=1762952514564YK07ZIElutD",
    "hppOrderId": "1762952514564YK07ZIElutD",
    "ecomOrderId": "b57fdfad-a7ba-4f4a-bd5f-07c07e2f2813",
    "redirectUrl": "https://defe-pgi-ecom.develop.bankalliance.ua/?hpp_id=1762952514564YK07ZIElutD",
    "hppPayType": "PURCHASE",
    "merchantRequestId": "137d93491081eb",
    "orderStatus": "PENDING",
    "paymentMethods": [
        "CARD",
        "APPLE_PAY",
        "GOOGLE_PAY"
    ],
    "createDate": "2025-11-12 15:01:54.50+02:00",
    "expiredOrderDate": "2025-11-13 15:01:54.56+02:00",
    "nbuQrCode": null
}
```

**Приклад тіла запиту hppPayType = A2A та priorityBankCode = null:**

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "hppPayType": "A2A",
    "directType": "BANK_LINK",
    "failUrl": "https://example.com/fail",
    "successUrl": "https://example.com/success",
    "merchantRequestId": "137d93491081eb939",
    "merchantComment": "137d9304-0368-11=eb939",
    "statusPageType": "STATUS_PAGE",
    "expirationTimeMinutes": 1440,
    "priorityBankCode": null,
    "paymentMethods": [
        "CARD"
    ],
    "customerData": {
        "senderCustomerId": "Id", 
        "senderEmail": "aaaa@gmail.com",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStret",
        "senderCity": "senderCity",
        "senderIp": "255.255.244.255",
        "senderBirthday": "22081989",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "senderPassport",
        "senderItn": "5555557777",
        "senderPhone": "380957388888"
    },
    "coinAmount": 1000,
    "purpose": "Payment for Order №123456",
    "language": "uk",
    "notificationUrl": "https://example.com/notify",
    "generateQrNbu": "true"
}
```

**Приклад тіла відповіді hppPayType = A2A та priorityBankCode = null::**

```json
{
    "coinAmount": 1000,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "statusUrl": null,
    "hppOrderId": "1762952144215CrdMyJEw_AI",
    "ecomOrderId": "80820e24-af95-4a7e-991b-f83efe851e86",
    "redirectUrl": "https://defe-ecom-deep-link.develop.bankalliance.ua/?redirectUrl=https%3A%2F%2Fbankalliance.go.link%2Fecomc2a%3Forder_id%3D1762952144215CrdMyJEw_AI%26adj_t%3D1rknh2ig%26adj_deep_link%3Dbankalliance%253A%252F%252Fecomc2a%253Forder_id%253D1762952144215CrdMyJEw_AI",
    "hppPayType": "A2A",
    "merchantRequestId": "137d93491081eb939",
    "orderStatus": "PENDING",
    "paymentMethods": [
        "CARD"
    ],
    "createDate": "2025-11-12 14:55:44.18+02:00",
    "expiredOrderDate": "2025-11-13 14:55:44.21+02:00",
    "nbuQrCode": "https://bank.gov.ua/qr/QkNECjAwMwoxCklDVAoK0JrQvtCy0LDQu9GM0YHRjNC60LjQuSDQktC70LDQtNC40YHQu9Cw0LIg0KLQtdGB0YIKVUExMjMyMjAwMTAwMDAwMjYyMDYzNjM1MDU1MTMKVUFIMTAuMDAKMzQ2NzgwODE1MApNUDJCL09USFIKMTc2Mjk1MjE0NDIxNUNyZE15SkV3X0FJCjEzN2Q5MzA0LTAzNjgtMTE9ZWI5MzkKUGF5bWVudCBmb3IgT3JkZXIg4oSWMTIzNDU2CkZGRkYKMjUxMTEzMTQ1NTQ0CjI1MTExMjE0NTU0NAoK"
}
```

**Приклад тіла запиту hppPayType = A2A та priorityBankCode = PRIVAT\_BANK:**

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "hppPayType": "A2A",
    "directType": "BANK_LINK",
    "failUrl": "https://example.com/fail",
    "successUrl": "https://example.com/success",
    "merchantRequestId": "137d93491081eb93",
    "merchantComment": "137d9304-0368-11=eb939",
    "statusPageType": "STATUS_PAGE",
    "expirationTimeMinutes": 1440,
    "priorityBankCode": "PRIVAT_BANK",
    "paymentMethods": [
        "CARD"
    ],
    "customerData": {
        "senderCustomerId": "Id", 
        "senderEmail": "aaaa@gmail.com",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStret",
        "senderCity": "senderCity",
        "senderIp": "255.255.244.255",
        "senderBirthday": "22081989",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "senderPassport",
        "senderItn": "5555557777",
        "senderPhone": "380957388888"
    },
    "coinAmount": 1000,
    "purpose": "Payment for Order №123456",
    "language": "uk",
    "notificationUrl": "https://example.com/notify",
    "generateQrNbu": "true"
}
```

**Приклад тіла відповіді hppPayType = A2A та priorityBankCode = PRIVAT\_BANK:**

```json
{
    "coinAmount": 1000,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "statusUrl": null,
    "hppOrderId": "1762952263495CsBJT9xC-s4",
    "ecomOrderId": "cce880f8-18e5-4cbc-8d88-0a85903d80e9",
    "redirectUrl": "https://www.privat24.ua/rd/send_qr/nbu/QkNECjAwMwoxCklDVAoK0JrQvtCy0LDQu9GM0YHRjNC60LjQuSDQktC70LDQtNC40YHQu9Cw0LIg0KLQtdGB0YIKVUExMjMyMjAwMTAwMDAwMjYyMDYzNjM1MDU1MTMKVUFIMTAuMDAKMzQ2NzgwODE1MApNUDJCL09USFIKMTc2Mjk1MjI2MzQ5NUNzQkpUOXhDLXM0CjEzN2Q5MzA0LTAzNjgtMTE9ZWI5MzkKUGF5bWVudCBmb3IgT3JkZXIg4oSWMTIzNDU2CkZGRkYKMjUxMTEzMTQ1NzQzCjI1MTExMjE0NTc0MwoK",
    "hppPayType": "A2A",
    "merchantRequestId": "137d93491081eb93",
    "orderStatus": "PENDING",
    "paymentMethods": [
        "CARD"
    ],
    "createDate": "2025-11-12 14:57:43.46+02:00",
    "expiredOrderDate": "2025-11-13 14:57:43.49+02:00",
    "nbuQrCode": "https://bank.gov.ua/qr/QkNECjAwMwoxCklDVAoK0JrQvtCy0LDQu9GM0YHRjNC60LjQuSDQktC70LDQtNC40YHQu9Cw0LIg0KLQtdGB0YIKVUExMjMyMjAwMTAwMDAwMjYyMDYzNjM1MDU1MTMKVUFIMTAuMDAKMzQ2NzgwODE1MApNUDJCL09USFIKMTc2Mjk1MjI2MzQ5NUNzQkpUOXhDLXM0CjEzN2Q5MzA0LTAzNjgtMTE9ZWI5MzkKUGF5bWVudCBmb3IgT3JkZXIg4oSWMTIzNDU2CkZGRkYKMjUxMTEzMTQ1NzQzCjI1MTExMjE0NTc0MwoK"
}
```
