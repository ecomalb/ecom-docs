---
description: '{{url}}/ecom/execute_request/payments/v1/create/preauth'
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Запит проведення Preauth Крок 1

**Вхідні параметри:**

<table><thead><tr><th width="157.31610107421875">Параметр</th><th width="224.6995849609375">Опиc</th><th width="88.4488525390625">Формат даних</th><th width="237.325927734375">Обов'язковість</th><th width="249.9949951171875">Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>encryptedCardNumber</td><td>номер карти зашифрований в JWE за допомогою публічного платіжного ключа</td><td>string</td><td>Так, якщо paymentMethodType = CARD</td><td>5573670000000304 (розшифрований вигляд)</td></tr><tr><td>typeToken</td><td>ознака створення токену та його тип для paymentMethodType = CARD</td><td>string</td><td>Ні, по замовчуванню NO_TOKEN</td><td><ul><li>NO_TOKEN,</li><li>TOKEN_PER_CUSTOMER - токен створюється для конкретного клієнта (customer) </li></ul></td></tr><tr><td>token</td><td>токен картки</td><td>string</td><td>Так, якщо paymentMethodType = TOKEN</td><td>TRXjqdJDr-4nA0jkSGfDFoe2</td></tr><tr><td>cvv</td><td>зашифрованний cvv</td><td>string</td><td>Так, якщо paymentMethodType = TOKEN</td><td>{{cvv}}</td></tr><tr><td>paymentToken</td><td>оплата по закриптованному токену aPay</td><td>object</td><td>Так, якщо paymentMethodType = APPLE_PAY_ENCRYPTED</td><td>{{paymentToken}}</td></tr><tr><td>paymentDataEncrypted</td><td>оплата по розкриптованному токену aPay або gPay</td><td>object</td><td>Так, якщо paymentMethodType = APPLE_PAY_DECRYPTED або GOOGLE_PAY_DECRYPTED</td><td>{{paymentDataEncrypted}}</td></tr><tr><td>googlePayPaymentData</td><td>оплата по закриптованному токену gPay</td><td>object</td><td>Так, якщо paymentMethodType = GOOGLE_PAY_ENCRYPTED</td><td>{{googlePayPaymentData}}</td></tr><tr><td>environment</td><td>середовище</td><td>string</td><td>Так, GOOGLE_PAY_ENCRYPTED</td><td>TEST/PRODUCTION</td></tr><tr><td>coinAmount</td><td>сума платежу в копійках </td><td>string</td><td><p>Ні, якщо paymentMethodType =</p><p>APPLE_PAY_ENCRYPTED</p><p>APPLE_PAY_DECRYPTED</p></td><td>2000</td></tr><tr><td>paymentMethodType</td><td>ознака, що визначає тип платіжного методу, через який здійснюється <strong>Preauth</strong>.</td><td>enum</td><td>Так, якщо параметр не вказано то по замовчванні CARD</td><td><p></p><ol start="1"><li>CARD - по номеру карти з послідуючою генерацією токену в нашій системі</li><li>TOKEN - по токену згенерованному в нашій системі</li><li>APPLE_PAY_ENCRYPTED</li><li>APPLE_PAY_DECRYPTED</li><li>GOOGLE_PAY_ENCRYPTED</li><li>GOOGLE_PAY_DECRYPTED</li></ol></td></tr><tr><td>txnType</td><td><p>під тип транзакціі</p><p>Параметр вказан - введення cvv та його перевірка не відбувається</p><p>Параметр НЕ вказан - введення cvv та його перевірка відбувається</p></td><td>enum</td><td>Ні</td><td>Можливі значення: NONCVV/noncvv</td></tr><tr><td>desiredThreeDSMode</td><td>ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string (50)</td><td>Так</td><td><p>За замовчуванням SHOULD</p><p>Можливі значення:</p><ul><li>MUST - мерчант вимагає проведення платежу з 3DS</li><li>MUST_NOT - примусова операція без 3DS</li><li>SHOULD - якщо картка підтримує 3DS, то робимо перевірку</li></ul></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (255)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>preAuthExpDate</td><td><p>Дата та час закінчення дії преавторизації.</p><p>Цей параметр визначає момент, до якого преавторизована сума залишається заблокованою на картці клієнта. Після настання вказаної дати система автоматично виконає реверс по операції, якщо вона не була завершена раніше. </p><ul><li>Значення має бути <strong>не менше ніж на 2 години пізніше</strong> від дати створення операції </li><li>Значення має бути <strong>не більше ніж на 28 днів пізніше</strong> від дати, переданої в запиті</li></ul></td><td><p></p><p>string</p></td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>resultRedirectUrl</td><td>Url для редиректа клієнта після проходження 3DS аутентифікації</td><td>string (1000)</td><td>Ні</td><td><a href="https://support.google.com/"><img src="https://support.google.com/favicon.ico" alt="">Google Help</a></td></tr><tr><td>customerData</td><td>об'єкт з customer даними </td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td>string (30)</td><td><p>Ні </p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>не може містити “NULL”, “3D SECURE”, “SURNAME”, “CARDHOLDER”, ”UNKNOWN”</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td>string (30)</td><td><p>Ні</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>не може містити “NULL”, “3D SECURE”, “SURNAME”, “CARDHOLDER”, ”UNKNOWN”</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td>string (30)</td><td><p>Ні </p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>не може містити “NULL”, “3D SECURE”, “SURNAME”, “CARDHOLDER”, ”UNKNOWN”</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника </td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td><code class="expression">space.vars.senderIP_description</code></td><td>string (50)</td><td>Ні</td><td><code class="expression">space.vars.senderIP_example</code></td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>Індекс відправника</td><td>string (50)</td><td>Ні</td><td> 49000</td></tr></tbody></table>

**Вихідні параметри:**

| Параметр                | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                    | тип транзакції                                                           | string       | PREAUTH                                                                                                                                                                                                |
| rrn                     | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                 | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                 | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount              | сума платежу в копійках                                                  | int          | 2000                                                                                                                                                                                                   |
| merchantId              | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId             | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId         | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName            | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode            | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                  | статус транзакціі                                                        | string       | SUСCESS FAIL PENDING REQUIRED\_3DS DESIRED\_THREEDS\_MODE\_ERROR                                                                                                                                       |
| transactionType         | тип транзакції у цифровому значенні                                      | string       | 195                                                                                                                                                                                                    |
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
| senderIp                | <code class="expression">space.vars.senderIP_description</code>          | string       | <code class="expression">space.vars.senderIP_example</code>                                                                                                                                            |
| senderPhone             | номер телефону відправника                                               | string       | 380630000000                                                                                                                                                                                           |
| senderBirthday          | день народження відправника                                              | string       | 31.12.2000                                                                                                                                                                                             |
| senderGender            | гендер відправника                                                       | string       | M                                                                                                                                                                                                      |
| senderZipCode           | індекс відправника                                                       | string       | 12000                                                                                                                                                                                                  |
| senderBankCode          | назва банку емітента відправника                                         | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| senderPaymentSystem     | назва мпс емітента відправника                                           | string       | MasterCard                                                                                                                                                                                             |
| senderCardNumberMask    | маскований номер карти відправника                                       | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| preAuthExpDate          | Дата та час закінчення дії преавторизації.                               | string       | 2025.10.07 14:27:00.000                                                                                                                                                                                |

#### Приклад тіла запиту paymentMethodType = CARD

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "merchantRequestId": "{{$guid}}",
    "encryptedCardNumber": "{{encryptedPanT}}",
    "coinAmount": 1000,
    "desiredThreeDSMode": "MUST_NOT",
    "notificationUrl": "https://webhook.site/5ec0db94-bce6-41a2-9216-08de60ab7822",
    "notificationEncryption": true,
    "date": "{{currentdateT}}.00+02:00",
    "preAuthExpDate": "2026-07-17 19:19:26.00+02:00",
    "merchantComment": "mezzzmezzzme",
    "comment": "AAAAfasfsfsfAAAAf",
    "purpose": "AAAAfasfsfsfAAAAfasAA",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "customerData": {
        "senderCustomerId": "1234",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "2001:0db8:85a3:0000:0000:8a2e:0370:7334",
        "senderBirthday": "20000110",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555555",
        "senderPhone": "5555"
    }
}
```

#### Приклад тіла запиту paymentMethodType = TOKEN

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "merchantRequestId": "{{$guid}}",
    "coinAmount": 100,
    "paymentMethodType":"TOKEN",
    "token":"TRXjqdJDr-4nA0jkSGfDFoe2",
    "cvv":"{{cvv}}",
    "desiredThreeDSMode": "MUST_NOT",
    "notificationUrl": "https://webhook.site/ff6d19be-b232-4dc8-928e-326db6bff10b",
    "date": "{{currentdateT}}.00+03:00",
    "preAuthExpDate": "2026-07-15 12:35:26.00+00:00",
    "merchantComment": "mezzzmezzzme",
    "comment": "AAAAfasfsfsfAAAAf",
    "purpose": "AAAAfasfsfsfAAAAfasAA",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "customerData": {
        "senderCustomerId": "tesChokan102726t",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "2001:0db8:85a3:0000:0000:8a2e:0370:7334",
        "senderBirthday": "20000110",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555555",
        "senderPhone": "5555"
    }
}
```

#### Приклад тіла запиту paymentMethodType = APPLE\_PAY\_ENCRYPTED

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "merchantRequestId": "{{$guid}}",
    "coinAmount": 100,
    "paymentMethodType":"APPLE_PAY_ENCRYPTED",
    "paymentToken": {
            "transactionIdentifier": "aebd938f2f9b060f59a640bc1919942d65adb05e3713af2102313465a2d68b17",
            "paymentData": {
                "data": "MDvMS5yxQwWCY2ZBQc1HTAUwXLcbaKIu+l8WYNs5K+avUHFjL7K1m3AXexbczirtsPuQJzUp6GEW7YM72LHIQzZElyCjEmbn08kJdju9htcC/q5bTeqsThOZNvVukbYsFIe1nVm+00kuWA4wxD+eHWqm2OIFovTbN4tRbPq3BBnwPOsc383Wo47mJOr4q3qFQGbPnoZWfHN9dMlTVWA6XP4MNzd46VPuPyGt6uOHcS4XDXWG4ma14y81FvCHWetszIfYnkFCdwN6MPIBff83alMbK4kX9+Kcb0+gev1aVuI+v4uwU39rQmuARnmL9SnCWRQcY2Aap7B2dfgXr4cNqvqmhzwm4v+I4udipM5THWk9jKCW1YWemLCcjY5YI35u6hkT1HGufrM+MBZNYQ==",
                "signature": "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",
                "header": {
                    "publicKeyHash": "3RA+IEMm3t+ZfpjWNxfVXsjRVamcUTGwXdp181xWCYk=",
                    "ephemeralPublicKey": "MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAE+s48S0xnNbMihR97GBCn3gTJAPpB7h4h3Hw6Ga1uZ9W9phPhQbBc/OAvgF7uCh6Tqpr91adOKIDWtRZzDQFerw==",
                    "transactionId": "aebd928f2f8b060f59a640bc1919942d65adb05e3713af2102313465a2d68b17"
                },
                "version": "EC_v1"
            },
            "paymentMethod": {
                "type": "credit",
                "displayName": "MasterCard 6702",
                "network": "MasterCard"
            }
        },
    "desiredThreeDSMode": "MUST",
    "notificationUrl": "https://webhook.site/ff6d19be-b232-4dc8-928e-326db6bff10b",
    "date": "{{currentdateT}}.00+03:00",
    "preAuthExpDate": "2026-07-15 12:35:26.00+00:00",
    "merchantComment": "mezzzmezzzme",
    "comment": "AAAAfasfsfsfAAAAf",
    "purpose": "AAAAfasfsfsfAAAAfasAA",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "customerData": {
        "senderCustomerId": "tesChokan102726t",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "2001:0db8:85a3:0000:0000:8a2e:0370:7334",
        "senderBirthday": "20000110",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555555",
        "senderPhone": "5555"
    }
}
```

#### Приклад тіла запиту paymentMethodType = APPLE\_PAY\_DECRYPTED

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "merchantRequestId": "{{$guid}}",
    "coinAmount": 100,
    "paymentMethodType":"APPLE_PAY_DECRYPTED",
    "paymentDataEncrypted":"{{encryptedPaymentData}}",
    "desiredThreeDSMode": "MUST",
    "notificationUrl": "https://webhook.site/ff6d19be-b232-4dc8-928e-326db6bff10b",
    "date": "{{currentdateT}}.00+03:00",
    "preAuthExpDate": "2026-07-15 12:35:26.00+00:00",
    "merchantComment": "mezzzmezzzme",
    "comment": "AAAAfasfsfsfAAAAf",
    "purpose": "AAAAfasfsfsfAAAAfasAA",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "customerData": {
        "senderCustomerId": "tesChokan102726t",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "2001:0db8:85a3:0000:0000:8a2e:0370:7334",
        "senderBirthday": "20000110",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555555",
        "senderPhone": "5555"
    }
}
```

#### Приклад тіла запиту paymentMethodType = GOOGLE\_PAY\_ENCRYPTED

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "merchantRequestId": "{{$guid}}",
    "coinAmount": 100,
    "paymentMethodType": "GOOGLE_PAY_ENCRYPTED",
    "environment": "TEST",
    "googlePayPaymentData": {
        "apiVersion": 2,
        "apiVersionMinor": 0,
        "paymentMethodData": {
            "description": "Test Card: Visa •••• 1111",
            "info": {
                "assuranceDetails": {
                    "accountVerified": true,
                    "cardHolderAuthenticated": false
                },
                "cardDetails": "1111",
                "cardFundingSource": "CREDIT",
                "cardNetwork": "VISA"
            },
            "tokenizationData": {
                "token": "{\"signature\":\"MEYCIQC+gX+WIL6SvlTP2x7OX70/cCLGjKu1nbve+oxKJiFvZwIhAOFjPso1c03Br6vbSoL0MDGLLpS18yTNpfrP0DpnkkL4\",\"intermediateSigningKey\":{\"signedKey\":\"{\\\"keyValue\\\":\\\"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEIuJ+WGM0VMSE7B3Tgdc3dTZnGCQR3fu0sp5G6yDfHnk73s7nkhBtRVnXV65dgqk3yCBAF3rpqC6dOwL1mhdNTg\\\\u003d\\\\u003d\\\",\\\"keyExpiration\\\":\\\"1784600346590\\\"}\",\"signatures\":[\"MEQCIHMxGwiIbncetYMrRyFMBFsu7zoNGHHzmyFqQGhjqkzlAiBfFmJf1hMfRJFrCG9SMXfIke1u2lKK2drUsU2HSU+WTA\\u003d\\u003d\"]},\"protocolVersion\":\"ECv2\",\"signedMessage\":\"{\\\"encryptedMessage\\\":\\\"O/fT6x63R2cZyjC0Sf+UP7XkOx7+N3aO0t6GY/4FaO7Q1medKWbS99whcrfoWEHTLRXF3JDmqb6Ubq/WebY2LisgyPxp80cQ/tw72fq4GNsiLMUFul9WsjPfvamUlQiFPV7/1yz5a8XpcZw3+MhDZG73yDKTEeRsNiyPPMj7ur2JT/K/zvy0JP7drExZ3x7a5+LLGJMfp9G79LBb/GZw1P//SF7oIT/7XOq7OYJoCfSSX6FQhkzuGzr6o+NR7ZeEm69bBZgSSfeh1yj950hi28TI0XgXPc6STdNjsWs1+DI7pjXwYOfguUfOd364YHBjCbQyVKiCxnhJ12oTqTqgtlTIhSA+pPhzmQ3d6eaTeZ5oTKe1KpoYBd/QcPjFu5lsTeAcQBUJDURIqEef3wIIVInOgI9yeRWJuvj4FGQmH9aG0PxbErRyij5Ym2DaCnziAZGzF6ip3AcA34xR6YykAwtUYa2yTi55WrNT3yl2xz0t4OGmT4XD6b50jrqzf7IrUrHA13nMZ522oytiwiiKWDvBW7poQaWESN0Ysnozr+AD1O3XWlVMNvJ79dDnp5a3jDVx5+xuNLQ2pYm26WYU4HcDZ3dCxfQXe4cmc3DBkzdFU8laUCNIp1rZeA\\\\u003d\\\\u003d\\\",\\\"ephemeralPublicKey\\\":\\\"BFEDoOFurjvz2/nDIg/gnXG1fM4Mr6Dc3aUw67KnMesdf0vRxy6rblHDHtYHwqk+UizLcrMIqrCiyd+zfsxh8Wk\\\\u003d\\\",\\\"tag\\\":\\\"jC5aXNoqqtvvUVhctqc3Qo5Uq/XK9rIHDIZv2LxfEss\\\\u003d\\\"}\"}",
                "type": "PAYMENT_GATEWAY"
            },
            "type": "CARD"
        },
        "merchantInfo": {
            "merchantId": "Iltxpa99j20LCOZ2oU_Hw6SJ",
            "gateway": "timeproject"
        }
    },
    "desiredThreeDSMode": "MUST",
    "notificationUrl": "https://webhook.site/ff6d19be-b232-4dc8-928e-326db6bff10b",
    "date": "{{currentdateT}}.00+03:00",
    "preAuthExpDate": "2026-07-15 12:35:26.00+00:00",
    "merchantComment": "mezzzmezzzme",
    "comment": "AAAAfasfsfsfAAAAf",
    "purpose": "AAAAfasfsfsfAAAAfasAA",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "customerData": {
        "senderCustomerId": "tesChokan102726t",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "2001:0db8:85a3:0000:0000:8a2e:0370:7334",
        "senderBirthday": "20000110",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555555",
        "senderPhone": "5555"
    }
}
```

#### Приклад тіла запиту paymentMethodType = GOOGLE\_PAY\_DECRYPTED

```json
{{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "merchantRequestId": "{{$guid}}",
    "coinAmount": 100,
    "paymentMethodType": "GOOGLE_PAY_DECRYPTED",
    "environment": "TEST",
    "paymentDataEncrypted":"{{encryptedPaymentData}}",
    "desiredThreeDSMode": "MUST",
    "notificationUrl": "https://webhook.site/ff6d19be-b232-4dc8-928e-326db6bff10b",
    "date": "{{currentdateT}}.00+03:00",
    "preAuthExpDate": "2026-07-15 12:35:26.00+00:00",
    "merchantComment": "mezzzmezzzme",
    "comment": "AAAAfasfsfsfAAAAf",
    "purpose": "AAAAfasfsfsfAAAAfasAA",
    "resultRedirectUrl": "https://support.google.com/websearch/answer/463?hl=ru",
    "customerData": {
        "senderCustomerId": "tesChokan102726t",
        "senderLastName": "senderLastName",
        "senderEmail": "aaaa@gmail.com",
        "senderFirstName": "senderFirstName",
        "senderMiddleName": "senderMiddleName",
        "senderRegion": "senderRegion",
        "senderCountry": "804",
        "senderAdditionalAddress": "senderAdditionalAddress",
        "senderStreet": "senderStreet",
        "senderCity": "senderCity",
        "senderIp": "2001:0db8:85a3:0000:0000:8a2e:0370:7334",
        "senderBirthday": "20000110",
        "senderGender": "Female",
        "senderZipCode": "12345",
        "senderPassport": "passport",
        "senderItn": "5555555",
        "senderPhone": "5555"
    }
}
```

**Приклад тіла відповіді без 3DS**

```json
{
    "type": "PREAUTH",
    "rrn": null,
    "purpose": "LLopo",
    "comment": "RRRR",
    "coinAmount": 100,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712822786872mHQm6XSmmKt",
    "ecomOperationId": "2bbd1b87-9a07-41cc-9789-48d8895b3cf1",
    "merchantName": null,
    "approvalCode": null,
    "status": "PENDING",
    "transactionType": 195,
    "merchantRequestId": "e2980c5e-cddc-4ccf-be36-47ef8c73da84",
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
    "preAuthExpDate": "2025-10-07 14:27:00.00+03:00",
    "notificationUrl": "https://webhook.site/6e35c4af-9af9-4212-9aa4-6a79ed6d7a0d",
    "paymentServiceType": "CARD",
    "notificationEncryption": true,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST_NOT",
    "threeDSMode": "MUST_NOT",
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

**Приклад тіла відповіді з 3DS**

```json
{
    "type": "PREAUTH",
    "rrn": null,
    "purpose": "LLopo",
    "comment": "RRRR",
    "coinAmount": 100,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712822536063CdDIRi8hhjq",
    "ecomOperationId": "82da90c3-50b8-4d5b-b357-2cbe55167200",
    "merchantName": null,
    "approvalCode": null,
    "status": "REQUIRED_3DS",
    "transactionType": 195,
    "merchantRequestId": "8aa31389-fe6f-4b40-bb5e-4ecedfefb847",
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
    "preAuthExpDate": "2025-10-07 14:27:00.00+03:00",
    "notificationUrl": "https://webhook.site/6e35c4af-9af9-4212-9aa4-6a79ed6d7a0d",
    "paymentServiceType": "CARD",
    "notificationEncryption": true,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "0ce5cc44-2698-4a2c-969a-3155bad68b6e",
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
