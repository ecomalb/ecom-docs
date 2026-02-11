---
description: '{{url}}/ecom/jws/payments/apple_pay/purchase_v3'
---

# Запит проведення платежу Крок 1

### Вхідні параметри частини payload JWS :

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="272">Формат даних</th><th width="71">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>Об’єкт paymentData, який необхідно закриптувати платіжним ключем</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td>applicationPrimaryAccountNumber</td><td>номер рахунку картки, з якої фінансується ця транзакція</td><td>string</td><td>Так</td><td>4420642424203999</td></tr><tr><td>applicationExpirationDate</td><td>Термін дії картки у форматі YYMMDD</td><td>string</td><td>Так</td><td>261001</td></tr><tr><td>currencyCode</td><td>Цифровий код валюти ISO 4217</td><td>string</td><td>Так</td><td>980</td></tr><tr><td>transactionAmount</td><td>сума платежу в копійках</td><td>string</td><td>Так</td><td>2000</td></tr><tr><td>cardholderName</td><td>Ім'я власника картки</td><td>string</td><td>Ні</td><td>Іванченко Петро</td></tr><tr><td>deviceManufacturerIdentifier</td><td>Hex-encoded device manufacturer identifier</td><td>string</td><td>Так</td><td>1</td></tr><tr><td>paymentDataType</td><td> </td><td>string</td><td>Так</td><td>3DSecure</td></tr><tr><td>paymentData</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td>onlinePaymentCryptogram</td><td>Криптограма платежу у форматі Base64</td><td>string</td><td>Так</td><td>AVn0rK8BiDxN2D/w2j8LMAABAAA=</td></tr><tr><td>eciIndicator</td><td>ECI indicator</td><td>string(1)</td><td>Ні</td><td>7</td></tr><tr><td>Додаткові дані для проведення платежу</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>desiredThreeDSMode</td><td>Ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string (50)</td><td>Так</td><td>За замовчуванням SHOULD</td></tr><tr><td>resultRedirectUrl</td><td>Url для редиректа клієнта після проходження 3DS аутентифікації</td><td>string (1000)</td><td>Ні</td><td><a href="https://support.google.com/"><img src="https://support.google.com/favicon.ico" alt="">Google Help</a></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td><a href="https://merchant.notification_url/">https://merchant.notification_url</a></td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>customerData</td><td>об'єкт з customer даними</td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td><code class="expression">space.vars.senderIP_description</code></td><td>string (50)</td><td>Ні</td><td><code class="expression">space.vars.senderIP_example</code></td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>індекс відправника</td><td>string (50)</td><td>Ні</td><td>49000</td></tr></tbody></table>

### Вихідні параметри частини payload JWS :

| Параметр               | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| ---------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                   | тип транзакції                                                           | string       | Purchase                                                                                                                                                                                               |
| rrn                    | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount             | сума платежу в копійках                                                  | int          | 2000                                                                                                                                                                                                   |
| merchantId             | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId            | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId        | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName           | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode           | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                 | статус транзакціі                                                        | string       | SUСCESS FAIL PENDING REQUIRED\_3DS DESIRED\_THREEDS\_MODE\_ERROR                                                                                                                                       |
| transactionType        | тип транзакції у цифровому значенні                                      | string       | 35                                                                                                                                                                                                     |
| merchantRequestId      | Id запиту мерчанта                                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency    | валюта платежу                                                           | string       | 980                                                                                                                                                                                                    |
| merchantCommission     | сума комісії                                                             | string       | 2                                                                                                                                                                                                      |
| createDateTime         | дата створення платежу                                                   | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime   | дата модифікаціі платежу                                                 | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode             | код відповіді                                                            | string       | 0                                                                                                                                                                                                      |
| responseCode           | деталі відповіді                                                         | string       | 0                                                                                                                                                                                                      |
| description            | опис відповіді                                                           | string       | approved                                                                                                                                                                                               |
| bankCode               | назва банку емітента                                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem          | назва мпс емітента                                                       | string       | MasterCard                                                                                                                                                                                             |
| productType            | тип продукту термінала                                                   | string       | PURCHASE                                                                                                                                                                                               |
| notificationUrl        | url, на який відправлено CallBack                                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType     | тип оплати                                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption | ознака криптування данних CallBack                                       | string       | true/false Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані                                                                                                     |
| cardNumberMask         | маскований номер карти                                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode     | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.     | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode            | параметр який вказує, використовувася 3DS у покупці чи ні                | string       | MUST- проводимо оплату з 3DS MUST\_NOT- проводимо оплату без 3DS                                                                                                                                       |
| statusThreeDs          | статус проведення 3DS                                                    | string       | Y - успіший 3ds N - не успішний 3ds                                                                                                                                                                    |
| threeDSServerTransId   | Id транзакціі в системі 3ds                                              | string       | b6c35fdb-28c1-454d-a2f3-51098c26bda4                                                                                                                                                                   |
| acsTransId             | Id транзакціі в системі ACS                                              | string       | 3e17fabb-71e6-498e-8794-ef8c95c5ba6f                                                                                                                                                                   |
| dsTransId              | Id транзакціі згенерований Directory Server                              | string       | 12ebc556-82d3-4e35-9fb8-77ac18b050ea                                                                                                                                                                   |
| eci                    | Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції | string       | 02                                                                                                                                                                                                     |
| processingMerchantId   | Id мерчанту в ПЦ                                                         | string       | AE100000                                                                                                                                                                                               |
| processingTerminalId   | Id терміналу в ПЦ                                                        | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl         | url для редиректа клієнта на сторінку емітента для проходження 3DS       | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                | під тип транзакціі                                                       | enum         | Можливі значення: NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається                                                                                          |
| senderCustomerId       | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName        | прізвище відправника                                                     | string       | Іваненко                                                                                                                                                                                               |
| senderLastName         | ім'я відправника                                                         | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName       | по-батькові відправника                                                  | string       | Іванович                                                                                                                                                                                               |
| senderEmail            | пошта відправника                                                        | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| senderCountry          | країна відправника                                                       | string       | Україна                                                                                                                                                                                                |



### Приклади :

**Приклад об’єкту paymentData**

```json
{
"applicationPrimaryAccountNumber":"{{applePayCardNumber}}",
"applicationExpirationDate":"{{applePayDate}}",
"currencyCode":"980",
"transactionAmount":"100",
"cardholderName":"{{cardholderName}}",
"deviceManufacturerIdentifier":"1255548888hfhhbbk",
"paymentDataType":"3DSecure",
"paymentData":{
"onlinePaymentCryptogram":"AVn0rK8BiDxN2D/w2j8LMAABAAA=",
"eciIndicator":"7"}
}

```

<details>

<summary>JWS Payload — тіло запиту перед підписанням</summary>

```json
{
    "paymentData":  "{{encryptedPaymentData}}",
    "merchantRequestId": "{{requestUUIDT}}",
    "desiredThreeDSMode": "MUST_NOT",
    "notificationUrl": "",
    "resultRedirectUrl": "",
    "purpose": "purpose",
    "comment": "comment",
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "customerData": {
        "senderFirstName": "John",
        "senderLastName": "Doe",
        "senderMiddleName": "Fall",
        "senderEmail": "test@gmail.com",
        "senderCountry": "sender_country",
        "senderRegion": "sender_region",
        "senderCity": "sender_city",
        "senderStreet": "sender_street",
        "senderAdditionalAddress": "N 6",
        "senderItn": "12345",
        "senderPassport": "12345",
        "senderIp": "165.222.87.224",
        "senderPhone": "380967542344",
        "senderBirthday": "12/12/2000",
        "senderGender": "Male",
        "senderZipCode": "12345"
    },
    "date": "{{currentdateT}}.00+00:00"
}

```



</details>



<details>

<summary>JWS Payload — тіло відповіді перед підписанням без 3дс</summary>

```json
{
    "type": "PURCHASE",
    "rrn": null,
    "purpose": "назначение",
    "comment": "тестовыйкомент",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": null,
    "ecomOperationId": "459dc6d9-cbcb-4f80-9e96-7c09562f51d9",
    "merchantName": null,
    "approvalCode": null,
    "status": "PENDING",
    "transactionType": 35,
    "merchantRequestId": "afb51fa6-a2ec-4f02-b2d0-3a6efee611f0",
    "transactionCurrency": "980",
    "merchantCommission": null,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": null
    },
    "bankCode": null,
    "paymentSystem": null,
    "productType": "PURCHASE",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": "APPLE_PAY",
    "notificationEncryption": false,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST_NOT",
    "threeDSMode": null,
    "statusThreeDs": null,
    "threeDSServerTransId": null,
    "redirect3dsUrl": null,
    "txnType": "null",
    "senderCustomerId": null,
    "senderFirstName": null,
    "senderLastName": null,
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": null,
    "senderRegion": null,
    "senderCity": null,
    "senderStreet": null,
    "senderAdditionalAddress": null,
    "senderItn": null,
    "senderPassport": null,
    "senderIp": null,
    "senderPhone": null,
    "senderBirthday": null,
    "senderGender": null,
    "senderZipCode": null,
    "senderBankCode": null,
    "senderPaymentSystem": null,
    "senderCardNumberMask": null
}
```



</details>

<details>

<summary>JWS Payload — тіло відповіді перед підписанням з 3дс</summary>

```json
{
    "type": "PURCHASE",
    "rrn": null,
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712824711120IbbgGHLPNCm",
    "ecomOperationId": "895f15f5-26f7-43cd-8cc1-8f970148425b",
    "merchantName": null,
    "approvalCode": null,
    "status": "REQUIRED_3DS",
    "transactionType": 35,
    "merchantRequestId": "4bf82d10-472d-4ac5-b505-4b7d22ba2686",
    "transactionCurrency": "980",
    "merchantCommission": null,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": null
    },
    "bankCode": null,
    "paymentSystem": null,
    "productType": "PURCHASE",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": "APPLE_PAY",
    "notificationEncryption": false,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "0036703b-839f-4166-a1d8-5fe2f6fb2ea8",
    "redirect3dsUrl": null,
    "txnType": "null",
    "senderCustomerId": null,
    "senderFirstName": null,
    "senderLastName": null,
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": null,
    "senderRegion": null,
    "senderCity": null,
    "senderStreet": null,
    "senderAdditionalAddress": null,
    "senderItn": null,
    "senderPassport": null,
    "senderIp": null,
    "senderPhone": null,
    "senderBirthday": null,
    "senderGender": null,
    "senderZipCode": null,
    "senderBankCode": null,
    "senderPaymentSystem": null,
    "senderCardNumberMask": null
}
```



</details>

