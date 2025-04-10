---
description: '{{url}}/ecom/execute_request/payments/v1/create/verification'
---

# Запит верифікації картки Крок 1

**Вхідні параметри:**

<table><thead><tr><th width="157.31610107421875">Параметр</th><th width="182.54296875">Опиc</th><th width="184.169677734375">Формат даних</th><th width="73.22216796875">Обов'язковість</th><th width="249.9949951171875">Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>encryptedCardNumber</td><td>номер карти зашифрований в JWE за допомогою публічного платіжного ключа</td><td>string</td><td>Так</td><td>5573670000000304 (розшифрований вигляд)</td></tr><tr><td>desiredThreeDSMode</td><td>ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string (50)</td><td>Так</td><td><p>За замовчуванням SHOULD</p><p>Можливі значення:</p><ul><li>MUST - мерчант вимагає проведення платежу з 3DS</li><li>MUST_NOT - примусова операція без 3DS</li><li>SHOULD - якщо картка підтримує 3DS, то робимо перевірку</li></ul></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>resultRedirectUrl</td><td>Url для редиректа клієнта після проходження 3DS аутентифікації</td><td>string (1000)</td><td>Ні</td><td><a href="https://support.google.com/"><img src="https://support.google.com/favicon.ico" alt="">Google Help</a></td></tr><tr><td>customerData</td><td>об'єкт з customer даними </td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>не може містити “NULL”, “3D SECURE”, “SURNAME”, “CARDHOLDER”, ”UNKNOWN”</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника </td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td>IP адреса відправника</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>Індекс відправника</td><td>string (50)</td><td>Ні</td><td> 49000</td></tr></tbody></table>

**Вихідні параметри:**

| Параметр                | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                    | тип транзакції                                                           | string       | Purchase                                                                                                                                                                                               |
| rrn                     | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                 | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                 | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount              | сума платежу                                                             | int          | 2000                                                                                                                                                                                                   |
| merchantId              | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId             | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId         | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName            | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode            | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                  | статус транзакціі                                                        | string       | SUСCESS FAIL PENDING REQUIRED\_3DS DESIRED\_THREEDS\_MODE\_ERROR                                                                                                                                       |
| transactionType         | тип транзакції у цифровому значенні                                      | string       | 35                                                                                                                                                                                                     |
| merchantRequestId       | Id запиту мерчанта                                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency     | валюта платежу                                                           | string       | 980                                                                                                                                                                                                    |
| merchantCommission      | сума комісії                                                             | string       | 2                                                                                                                                                                                                      |
| createDateTime          | дата створення платежу                                                   | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime    | дата модифікаціі платежу                                                 | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode              | код відповіді                                                            | string       | 0                                                                                                                                                                                                      |
| responseCode            | деталі відповіді                                                         | string       | 0                                                                                                                                                                                                      |
| description             | опис відповіді                                                           | string       | approved                                                                                                                                                                                               |
| bankCode                | назва банку емітента                                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem           | назва мпс емітента                                                       | string       | MasterCard                                                                                                                                                                                             |
| productType             | тип продукту термінала                                                   | string       | PURCHASE                                                                                                                                                                                               |
| notificationUrl         | url, на який відправлено CallBack                                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType      | тип оплати                                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption  | ознака криптування данних CallBack                                       | string       | true/false Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані                                                                                                     |
| cardNumberMask          | маскований номер карти                                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode      | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.     | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode             | параметр який вказує, використовувася 3DS у покупці чи ні                | string       | MUST- проводимо оплату з 3DS MUST\_NOT- проводимо оплату без 3DS                                                                                                                                       |
| statusThreeDs           | статус проведення 3DS                                                    | string       | Y - успіший 3ds N - не успішний 3ds                                                                                                                                                                    |
| threeDSServerTransId    | Id транзакціі в системі 3ds                                              | string       | 8a811df4-91e0-436b-a9ac-9b0772c96f28                                                                                                                                                                   |
| acsTransId              | Id транзакціі в системі ACS                                              | string       | 3e17fabb-71e6-498e-8794-ef8c95c5ba6f                                                                                                                                                                   |
| dsTransId               | Id транзакціі згенерований  Directory Server                             | string       | 12ebc556-82d3-4e35-9fb8-77ac18b050ea                                                                                                                                                                   |
| eci                     | Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції | string       | 02                                                                                                                                                                                                     |
| processingMerchantId    | Id мерчанту в ПЦ                                                         | string       | AE100000                                                                                                                                                                                               |
| processingTerminalId    | Id терміналу в ПЦ                                                        | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl          | url для редиректа клієнта на сторінку емітента для проходження 3DS       | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                 | під тип транзакціі                                                       | enum         | Можливі значення: NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається                                                                                          |
| senderCustomerId        | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName         | ім'я відправника                                                         | string       | Іваненко                                                                                                                                                                                               |
| senderLastName          | прізвище відправника                                                     | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName        | по-батькові відправника                                                  | string       | Іванович                                                                                                                                                                                               |
| senderEmail             | пошта відправника                                                        | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| senderCountry           | країна відправника                                                       | string       | Україна                                                                                                                                                                                                |
| senderRegion            | область відправника                                                      | string       | Київська                                                                                                                                                                                               |
| senderCity              | місто відправника                                                        | string       | Київ                                                                                                                                                                                                   |
| senderStreet            | вулиця відправника                                                       | string       | Січових стрільців                                                                                                                                                                                      |
| senderAdditionalAddress | додаткові дані адреси відправника (поверх, номер дому, квартира)         | string       | 23                                                                                                                                                                                                     |
| senderItn               | іпн відправника                                                          | string       | 123456789                                                                                                                                                                                              |
| senderPassport          | паспорт відправника                                                      | string       | АН123456                                                                                                                                                                                               |
| senderIp                | ip адреса відправника                                                    | string       | 123.12.12.12                                                                                                                                                                                           |
| senderPhone             | номер телефону відправника                                               | string       | 380630000000                                                                                                                                                                                           |
| senderBirthday          | день народження відправника                                              | string       | 31.12.2000                                                                                                                                                                                             |
| senderGender            | гендер відправника                                                       | string       | M                                                                                                                                                                                                      |
| senderZipCode           | індекс відправника                                                       | string       | 12000                                                                                                                                                                                                  |
| senderBankCode          | назва банку емітента відправника                                         | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| senderPaymentSystem     | назва мпс емітента відправника                                           | string       | MasterCard                                                                                                                                                                                             |
| senderCardNumberMask    | маскований номер карти відправника                                       | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |

**Приклад тіла запиту**

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac1200",
    "merchantRequestId": "8c1f4b28-5b96-4b0e-bdc6-1d1cc2f2c42a",
    "encryptedCardNumber": "",
    "merchantComment": "",
    "comment": "",
    "purpose": "",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "desiredThreeDSMode": "MUST",
    "notificationUrl": "https://webhook.site/739593ac-8e50-48fd-a6c4-0422f9487a6e",
    "notificationEncryption": false,
    "date": "2025-04-03 14:55:14.00+00:00",
    "customerData": {
        "senderCustomerId": "senderCustomerId",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "55.555.44",
        "senderBirthday": "senderBirthday",
        "senderGender": "senderGender",
        "senderZipCode": "senderZipCode",
        "senderPassport": "senderPassport",
        "senderItn": "senderItn",
        "senderPhone": "senderPhone"
    }
}
```

**Приклад тіла відповіді без 3DS**

```json
{
    "type": "VERIFICATION",
    "purpose": "",
    "comment": "",
    "coinAmount": 0,
    "merchantId": "137d9304-0368-11ed-b939-0242ac1200",
    "operationId": "17436921182614gyGFwqQKlb",
    "ecomOperationId": "71baa5d2-d685-4f1e-9b44-3b1e747855dc",
    "status": "PENDING",
    "transactionType": 215,
    "merchantRequestId": "8c1f4b28-5b96-4b0e-bdc6-1d1cc2f2c42a",
    "transactionCurrency": "980",
    "creationDateTime": "2025.04.03 17:55:18.214",
    "modificationDateTime": "2025.04.03 17:55:18.214",
    "transactionResponseInfo": {},
    "productType": "PURCHASE",
    "notificationUrl": "https://webhook.site/739593ac-8e50-48fd-a6c4-0422f9487a6e",
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "processingTerminalId": "AE001001",
    "processingMerchantId": "AE001001",
    "creatorSystem": "H2H",
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "threeDSServerTransId": "6c187d07-e46e-4683-930c-8e8312433130",
    "senderCustomerId": "1234",
    "senderFirstName": "senderFirstName",
    "senderLastName": "senderLastName",
    "senderMiddleName": "senderMiddleName",
    "senderEmail": "aaaa@gmail.com",
    "senderCountry": "804",
    "senderRegion": "senderRegion",
    "senderCity": "senderCity",
    "senderStreet": "senderStreet",
    "senderAdditionalAddress": "senderAdditionalAddress",
    "senderItn": "5555555",
    "senderPassport": "passport",
    "senderIp": "55.555.44",
    "senderPhone": "5555",
    "senderBirthday": "20000110",
    "senderGender": "Female",
    "senderZipCode": "12345"
}
```

**Приклад тіла відповіді з 3DS**

```json
{
    "type": "VERIFICATION",
    "purpose": "",
    "comment": "",
    "coinAmount": 0,
    "merchantId": "137d9304-0368-11ed-b939-0242ac1200",
    "operationId": "17436921182614gyGFwqQKlb",
    "ecomOperationId": "71baa5d2-d685-4f1e-9b44-3b1e747855dc",
    "status": "REQUIRED_3DS",
    "transactionType": 215,
    "merchantRequestId": "8c1f4b28-5b96-4b0e-bdc6-1d1cc2f2c42a",
    "transactionCurrency": "980",
    "creationDateTime": "2025.04.03 17:55:18.214",
    "modificationDateTime": "2025.04.03 17:55:18.214",
    "transactionResponseInfo": {},
    "productType": "PURCHASE",
    "notificationUrl": "https://webhook.site/739593ac-8e50-48fd-a6c4-0422f9487a6e",
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "processingTerminalId": "AE001001",
    "processingMerchantId": "AE001001",
    "creatorSystem": "H2H",
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "threeDSServerTransId": "6c187d07-e46e-4683-930c-8e8312433130",
    "senderCustomerId": "1234",
    "senderFirstName": "senderFirstName",
    "senderLastName": "senderLastName",
    "senderMiddleName": "senderMiddleName",
    "senderEmail": "aaaa@gmail.com",
    "senderCountry": "804",
    "senderRegion": "senderRegion",
    "senderCity": "senderCity",
    "senderStreet": "senderStreet",
    "senderAdditionalAddress": "senderAdditionalAddress",
    "senderItn": "5555555",
    "senderPassport": "passport",
    "senderIp": "55.555.44",
    "senderPhone": "5555",
    "senderBirthday": "20000110",
    "senderGender": "Female",
    "senderZipCode": "12345"
}
```
