---
description: '{{url}}/ecom/jws/payments/purchase/token_3ds_v1'
---

# Запит проведення платежу по токену 3DS Крок 2

### Вхідні параметри частини payload JWS :

<table data-full-width="true"><thead><tr><th>Параметр</th><th width="208">Опис</th><th width="153">Формат даних</th><th width="173">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>operationId</td><td>Ід операції, який отримали на 1 кроці</td><td>string</td><td>Так</td><td>1697008393082nW0c1jr6KVv</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00 </td></tr><tr><td>browserInfo</td><td>об’єкт за даними браузера </td><td>object</td><td>Так, якщо операція потребує 3DS</td><td><br></td></tr><tr><td>browserAcceptHeader</td><td>Http заголовок запиту </td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9</td></tr><tr><td>browserUserAgent</td><td>програмний елемент браузера, що позначає систему, що користується нею</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36</td></tr><tr><td>browserLanguage</td><td>мова браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>en-US,en</td></tr><tr><td>browserColorDepth</td><td>значення глибини кольору екрана у браузері</td><td>string</td><td>Так, якщо операція потребує 3DS  </td><td>24</td></tr><tr><td>browserScreenHeight</td><td>висота області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>800</td></tr><tr><td>browserScreenWidth</td><td>широта області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>1280</td></tr><tr><td>browserTZ</td><td>Timezone браузера </td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>-180</td></tr></tbody></table>

### Вихідні параметри частини payload JWS :

| Параметр                | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                    | тип транзакції                                                           | string       | Purchase                                                                                                                                                                                               |
| rrn                     | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                 | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                 | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount              | сума платежу в копійках                                                  | int          | 2000                                                                                                                                                                                                   |
| merchantId              | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId             | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId         | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName            | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode            | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                  | статус транзакціі                                                        | string       | <p>SUСCESS<br>FAIL<br>PENDING<br>REQUIRED_3DS<br>DESIRED_THREEDS_MODE_ERROR</p>                                                                                                                        |
| transactionType         | тип транзакції у цифровому значенні                                      | string       | 35                                                                                                                                                                                                     |
| merchantRequestId       | Id запиту мерчанта                                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency     | валюта платежу                                                           | string       | 980                                                                                                                                                                                                    |
| merchantCommission      | сума комісії                                                             | string       | 2                                                                                                                                                                                                      |
| creationDateTime        | дата створення платежу                                                   | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime    | дата модифікаціі платежу                                                 | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode              | код відповіді                                                            | string       | 0                                                                                                                                                                                                      |
| responseCode            | деталі відповіді                                                         | string       | 0                                                                                                                                                                                                      |
| description             | опис відповіді                                                           | string       | approved                                                                                                                                                                                               |
| bankCode                | назва банку емітента                                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem           | назва мпс емітента                                                       | string       | MasterCard                                                                                                                                                                                             |
| productType             | тип продукту термінала                                                   | string       | PURCHASE                                                                                                                                                                                               |
| notificationUrl         | url, на який відправлено CallBack                                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType      | тип оплати                                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption  | ознака криптування данних CallBack                                       | string       | <p>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p>                                                                                           |
| cardNumberMask          | маскований номер карти                                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode      | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.     | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode             | параметр який вказує, використовувася 3DS у покупці чи ні                | string       | <p>MUST- проводимо оплату з 3DS<br>MUST_NOT- проводимо оплату без 3DS</p>                                                                                                                              |
| statusThreeDs           | статус проведення 3DS                                                    | string       | <p>Y - успіший 3ds<br>N - не успішний 3ds</p>                                                                                                                                                          |
| threeDSServerTransId    | Id транзакціі в системі 3ds                                              | string       | b6c35fdb-28c1-454d-a2f3-51098c26bda4                                                                                                                                                                   |
| acsTransId              | Id транзакціі в системі ACS                                              | string       | 3e17fabb-71e6-498e-8794-ef8c95c5ba6f                                                                                                                                                                   |
| dsTransId               | Id транзакціі згенерований Directory Server                              | string       | 12ebc556-82d3-4e35-9fb8-77ac18b050ea                                                                                                                                                                   |
| eci                     | Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції | string       | 02                                                                                                                                                                                                     |
| processingMerchantId    | Id мерчанту в ПЦ                                                         | string       | AE100000                                                                                                                                                                                               |
| processingTerminalId    | Id терміналу в ПЦ                                                        | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl          | url для редиректа клієнта на сторінку емітента для проходження 3DS       | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                 | під тип транзакціі                                                       | enum         | <p>Можливі значення:<br>NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається</p>                                                                                |
| senderCustomerId        | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName         | ім'я відправника                                                         | string       | Іваненко                                                                                                                                                                                               |
| senderLastName          | прізвище відправника                                                     | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName        | по-батькові відправника                                                  | string       | Іванович                                                                                                                                                                                               |
| senderEmail             | пошта відправника                                                        | string       | mail@gmail.com                                                                                                                                                                                         |
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
| externalCardToken       | id токену                                                                | string       | tmkEYenZSa8FV03aawVXxbep                                                                                                                                                                               |

### Приклади :&#x20;

<details>

<summary>JWS Payload — тіло запиту перед підписанням</summary>

```
{
    "operationId": "{{operationIdT}}",
    "browserInfo": {
        "browserAcceptHeader": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
        "browserUserAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36",
        "browserLanguage": "en-US,en",
        "browserColorDepth": "24",
        "browserScreenHeight": "800",
        "browserScreenWidth": "1280",
        "browserTZ": "-180"
    },
    "date": "{{currentdateT}}.00+00:00"
}

```

</details>



<details>

<summary>JWS Payload — тіло відповіді перед підписанням</summary>

```
{
    "type": "PURCHASE",
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
    "transactionType": 35,
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
    "notificationUrl": "https://webhook.site/6e35c4af-9af9-4212-9aa4-6a79ed6d7a0d",
    "paymentServiceType": "CARD",
    "notificationEncryption": true,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "0ce5cc44-2698-4a2c-969a-3155bad68b6e",
    "redirect3dsUrl": "https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1712822536063CdDIRi8hhjq",
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
    "senderCardNumberMask": null,
    "externalCardToken": "tmkEYenZSa8FV03aawVXxbep"
}
```

</details>
