---
description: '{{url}}/ecom/execute_request/hpp/v1/create-order'
---

# Створення замовлення

**Вхідні параметри:**

<table><thead><tr><th width="173">Параметр</th><th width="162">Опиc</th><th width="161">Формат даних</th><th width="82">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>hppPayType</td><td>тип оплати</td><td>string</td><td>Так</td><td>Доступні значення -PURCHASE</td></tr><tr><td>coinAmount</td><td>сума замовлення в копійках</td><td>long</td><td>Так</td><td>2000</td></tr><tr><td>paymentMethods</td><td>методи оплати </td><td>enum</td><td>Так</td><td>Доступні значення - CARD, APPLE_PAY, GOOGLE_PAY</td></tr><tr><td>language</td><td>мова платіжного віджета. ISO 639-1 2 digits</td><td>string (50)</td><td>Ні</td><td><p>Доступні значення : uk(за замовчуванням)</p><p>en,es,de,pl,fr,tr,it,nl,pt</p></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</td></tr><tr><td>successUrl</td><td>url, для редіректу на сайт мерчанту при успішному статусі </td><td>string (1000)</td><td>Так </td><td><p><a href="https://example.com/success">https://example.com/success</a></p><p></p></td></tr><tr><td>failUrl</td><td>url, для редіректу на сайт мерчанту при неуспішному статусі</td><td>string (1000)</td><td>Так</td><td><a href="https://example.com/fail">https://example.com/fail</a></td></tr><tr><td>statusPageType</td><td>тип сторінки статусу </td><td>enum</td><td>Так</td><td>доступні значення - statusPage</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>customerData</td><td>об'єкт з customer даними </td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>не може містити “NULL”, “3D SECURE”, “SURNAME”, “CARDHOLDER”, ”UNKNOWN”</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника </td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td>IPv4 адреса відправника</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>Індекс відправника</td><td>string (50)</td><td>Ні</td><td> 49000</td></tr></tbody></table>

**Вихідні параметри:**

| Параметр          | Опис                                                       | Формат даних | Приклад                                                                                                                                                                             |
| ----------------- | ---------------------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| hppOrderId        | Id замовлення                                              | string       | 37d9304-0368-11ed-b939-0242ac120002                                                                                                                                                 |
| merchantRequestId | унікальний ідентифікатор мерчанта                          | string       | 64d9304-0368-11ed-b939-0242ac1221458                                                                                                                                                |
| hppPayType        | тип оплати                                                 | string       | PURCHASE                                                                                                                                                                            |
| paymentMethods    | методи оплати                                              | enum         | CARD                                                                                                                                                                                |
| orderStatus       | статус замовлення                                          | string       | SUCCESS, FAIL, PENDING, REQUIRED\_3DS, CANCELED, PARTIAL\_REFUND                                                                                                                    |
| coinAmount        | сума замовлення в копійках                                 | long         | 2000                                                                                                                                                                                |
| merchantId        | Id мерчанту згенерований в Єкомі                           | string       | 37d9304-0368-11ed-b939-0242ac120002                                                                                                                                                 |
| expiredOrderDate  | дата та час дії замовлення                                 | string       | 2024-09-05 18:35:18.210+03:00                                                                                                                                                       |
| redirectUrl       | посилання на перенаправлення клієнта на платіжку сторінку  | string       | [http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp\_id=1728551936236-DAfCP7wrKT](http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=1728551936236-DAfCP7wrKT)        |
| createDate        | дата та час створення замовлення                           | string       | 2024-09-05 18:35:18.210+03:00                                                                                                                                                       |
| statusUrl         | url для редіректу на сторінку статусу                      | string       | [http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp\_id=1728551936236-DAfCP7wrKT](http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=1728551936236-DAfCP7wrKT) |

**Приклад тіла запиту**

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "hppPayType": "PURCHASE",
    "failUrl": "https://example.com/fail",
    "successUrl": "https://example.com/success",
    "merchantRequestId": "137d9304-0368-11ed-b939-0241ac220104",
    "statusPageType": "STATUS_PAGE",
    "paymentMethods": [
        "CARD"
    ],
    "customerData": {
        "senderCustomerId": "Id ",
        "senderEmail": "aaaa@gmail.com",
        "senderMiddleName": "s",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStret",
        "senderCity": "senderCity",
        "senderIp": "255.255.244.255",
        "senderBirthday": "22081989",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555557777",
        "senderPhone": "380957388888"
    },
    "coinAmount": 1000,
    "purpose": "Payment for Order №123456",
    "language": "uk",
    "notificationUrl": "https://example.com/notify"
}
```

**Приклад тіла відповіді**

```json
{
    "coinAmount": 1000,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "statusUrl": "http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=1728551936236-DAfCP7wrKT",
    "hppOrderId": "1728551936236-DAfCP7wrKT",
    "redirectUrl": "http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=1728551936236-DAfCP7wrKT",
    "hppPayType": "PURCHASE",
    "merchantRequestId": "137d9304-0368-11ed-b939-0241ac220104",
    "orderStatus": "PENDING",
    "paymentMethods": [
        "CARD"
    ],
    "createDate": "2024-10-10 12:18:56.19+03:00",
    "expiredOrderDate": "2024-10-10 12:33:56.23+03:00"
}
```
