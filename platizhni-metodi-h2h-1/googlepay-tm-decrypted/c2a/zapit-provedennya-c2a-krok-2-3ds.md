---
description: '{{url}}/ecom/execute_request/payments/v1/google_pay_3ds/card_to_account'
---

# Запит проведення c2a Крок 2 (3DS)

#### Вхідні JSON параметри:

<table data-full-width="true"><thead><tr><th>Параметр</th><th>Опис</th><th width="156">Формат даних</th><th width="171">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>operationId</td><td>Ід операції, який отримали на 1 кроці</td><td>string</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>browserInfo</td><td>об’єкт за даними браузера</td><td>object</td><td>Так, якщо операція потребує 3DS</td><td></td></tr><tr><td>browserAcceptHeader</td><td>Http заголовок запиту</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9</td></tr><tr><td>browserUserAgent</td><td>програмний елемент браузера, що позначає систему, що користується нею</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36</td></tr><tr><td>browserLanguage</td><td>мова браузера</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>en-US,en</td></tr><tr><td>browserColorDepth</td><td>значення глибини кольору екрана у браузері</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>24</td></tr><tr><td>browserScreenHeight</td><td>висота області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>800</td></tr><tr><td>browserScreenWidth</td><td>широта області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>1280</td></tr><tr><td>browserTZ</td><td>Timezone браузера</td><td>string</td><td>Так, якщо операція потребує 3DS</td><td>-180</td></tr></tbody></table>

#### Вихідні параметри

| Параметр                   | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| -------------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                       | тип транзакції                                                           | string       | CARD\_2\_ACCOUNT                                                                                                                                                                                       |
| rrn                        | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                    | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                    | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount                 | сума платежу в копійках                                                  | int          | 2000                                                                                                                                                                                                   |
| merchantId                 | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId                | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId            | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName               | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode               | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                     | статус транзакціі                                                        | string       | <p>SUСCESS<br>FAIL<br>PENDING<br>REQUIRED_3DS<br>DESIRED_THREEDS_MODE_ERROR</p>                                                                                                                        |
| transactionType            | тип транзакції у цифровому значенні                                      | string       | 62                                                                                                                                                                                                     |
| merchantRequestId          | Id запиту мерчанта                                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency        | валюта платежу                                                           | string       | 980                                                                                                                                                                                                    |
| merchantCommission         | сума комісії                                                             | string       | 2                                                                                                                                                                                                      |
| createDateTime             | дата створення платежу                                                   | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime       | дата модифікаціі платежу                                                 | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode                 | код відповіді                                                            | string       | 0                                                                                                                                                                                                      |
| responseCode               | деталі відповіді                                                         | string       | 0                                                                                                                                                                                                      |
| description                | опис відповіді                                                           | string       | approved                                                                                                                                                                                               |
| bankCode                   | назва банку емітента                                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem              | назва мпс емітента                                                       | string       | MasterCard                                                                                                                                                                                             |
| productType                | тип продукту термінала                                                   | string       | C2A                                                                                                                                                                                                    |
| notificationUrl            | url, на який відправлено CallBack                                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType         | тип оплати                                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption     | ознака криптування данних CallBack                                       | string       | <p>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p>                                                                                           |
| cardNumberMask             | маскований номер карти                                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode         | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.     | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode                | параметр який вказує, використовувася 3DS у покупці чи ні                | string       | <p>MUST- проводимо оплату з 3DS<br>MUST_NOT- проводимо оплату без 3DS</p>                                                                                                                              |
| statusThreeDs              | статус проведення 3DS                                                    | string       | <p>Y - успіший 3ds<br>N - не успішний 3ds</p>                                                                                                                                                          |
| threeDSServerTransId       | Id транзакціі в системі 3ds                                              | string       | b6c35fdb-28c1-454d-a2f3-51098c26bda4                                                                                                                                                                   |
| acsTransId                 | Id транзакціі в системі ACS                                              | string       | 3e17fabb-71e6-498e-8794-ef8c95c5ba6f                                                                                                                                                                   |
| dsTransId                  | Id транзакціі згенерований Directory Server                              | string       | 12ebc556-82d3-4e35-9fb8-77ac18b050ea                                                                                                                                                                   |
| eci                        | Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції | string       | 02                                                                                                                                                                                                     |
| processingMerchantId       | Id мерчанту в ПЦ                                                         | string       | AE100000                                                                                                                                                                                               |
| processingTerminalId       | Id терміналу в ПЦ                                                        | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl             | url для редиректа клієнта на сторінку емітента для проходження 3DS       | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                    | під тип транзакціі                                                       | enum         | <p>Можливі значення:<br>NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається</p>                                                                                |
| senderCustomerId           | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName            | ім'я відправника                                                         | string       | Іваненко                                                                                                                                                                                               |
| senderLastName             | прізвище відправника                                                     | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName           | по-батькові відправника                                                  | string       | Іванович                                                                                                                                                                                               |
| senderEmail                | пошта відправника                                                        | string       | mail@gmail.com                                                                                                                                                                                         |
| senderCountry              | країна відправника                                                       | string       | Україна                                                                                                                                                                                                |
| senderRegion               | область відправника                                                      | string       | Київська                                                                                                                                                                                               |
| senderCity                 | місто відправника                                                        | string       | Київ                                                                                                                                                                                                   |
| senderStreet               | вулиця відправника                                                       | string       | Січових стрільців                                                                                                                                                                                      |
| senderAdditionalAddress    | додаткові дані адреси відправника (поверх, номер дому, квартира)         | string       | 23                                                                                                                                                                                                     |
| senderItn                  | іпн відправника                                                          | string       | 123456789                                                                                                                                                                                              |
| senderPassport             | паспорт відправника                                                      | string       | АН123456                                                                                                                                                                                               |
| senderIp                   | <code class="expression">space.vars.senderIP_description</code>          | string       | <code class="expression">space.vars.senderIP_example</code>                                                                                                                                            |
| senderPhone                | номер телефону відправника                                               | string       | 380630000000                                                                                                                                                                                           |
| senderBirthday             | день народження відправника                                              | string       | 31.12.2000                                                                                                                                                                                             |
| senderGender               | гендер відправника                                                       | string       | M                                                                                                                                                                                                      |
| senderZipCode              | індекс відправника                                                       | string       | 12000                                                                                                                                                                                                  |
| senderBankCode             | назва банку емітента відправника                                         | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| senderPaymentSystem        | назва мпс емітента відправника                                           | string       | MasterCard                                                                                                                                                                                             |
| senderCardNumberMask       | маскований номер карти відправника                                       | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| recipientCustomerId        | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| recipientFirstName         | ім'я отримувача                                                          | string       | Іваненко                                                                                                                                                                                               |
| recipientLastName          | прізвище отримувача                                                      | string       | Іван                                                                                                                                                                                                   |
| recipientMiddleName        | по-батькові отримувача                                                   | string       | Іванович                                                                                                                                                                                               |
| recipientEmail             | пошта отримувача                                                         | string       | mail@gmail.com                                                                                                                                                                                         |
| recipientCountry           | країна отримувача                                                        | string       | Україна                                                                                                                                                                                                |
| recipientRegion            | область отримувача                                                       | string       | Київська                                                                                                                                                                                               |
| recipientCity              | місто отримувача                                                         | string       | Київ                                                                                                                                                                                                   |
| recipientStreet            | вулиця отримувача                                                        | string       | Січових стрільців                                                                                                                                                                                      |
| recipientAdditionalAddress | додаткові дані адреси отримувача (поверх, номер дому, квартира)          | string       | 23                                                                                                                                                                                                     |
| recipientItn               | іпн отримувача                                                           | string       | 123456789                                                                                                                                                                                              |
| recipientPassport          | паспорт отримувача                                                       | string       | АН123456                                                                                                                                                                                               |
| recipientIp                | <code class="expression">space.vars.senderIP_description</code>          | string       | <code class="expression">space.vars.senderIP_example</code>                                                                                                                                            |
| recipientPhone             | номер телефону отримувача                                                | string       | 380630000000                                                                                                                                                                                           |
| recipientBirthday          | день народження отримувача                                               | string       | 31.12.2000                                                                                                                                                                                             |
| recipientGender            | гендер отримувача                                                        | string       | M                                                                                                                                                                                                      |
| recipientZipCode           | індекс отримувача                                                        | string       | 12000                                                                                                                                                                                                  |
| recipientBankCode          | назва банку емітента отримувача                                          | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| recipientPaymentSystem     | назва мпс емітента отримувача                                            | string       | MasterCard                                                                                                                                                                                             |
| recipientCardNumberMask    | маскований номер карти отримувача                                        | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |

#### Приклад тіла запиту

```json
{
    "operationId": "1705414311419tEIgRRDZSLm",
    "browserInfo": {
        "browserAcceptHeader":",
        "browserUserAgent": "",
        "browserLanguage": "",
        "browserColorDepth": "",
        "browserScreenHeight": "",
        "browserScreenWidth": "",
        "browserTZ": ""
    },
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "date": "{{currentdateT}}.00+00:00"
}
```

#### Приклад тіла відповіді

```json
{
    "type": "CARD_2_ACCOUNT",
    "rrn": null,
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712843252781OgXAcDp-0Gn",
    "ecomOperationId": "ec2ce45b-9a97-4507-980a-f8249e9ef84f",
    "merchantName": null,
    "approvalCode": null,
    "status": "REQUIRED_3DS",
    "transactionType": 62,
    "merchantRequestId": "a8fec362-b5ed-42c7-b2fd-c89e9d0ec508",
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
    "productType": "C2A",
    "notificationUrl": "https://webhook.site/cbf8c83a-ee1e-47c6-899c-eca5731ff084/mock",
    "paymentServiceType": "GOOGLE_PAY",
    "notificationEncryption": false,
    "senderCardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "b6c35fdb-28c1-454d-a2f3-51098c26bda4",
    "redirect3dsUrl": "https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1712843252781OgXAcDp-0Gn",
    "recipientAccount": null,
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
    "recipientCustomerId": null,
    "recipientFirstName": null,
    "recipientLastName": null,
    "recipientMiddleName": null,
    "recipientEmail": null,
    "recipientCountry": null,
    "recipientRegion": null,
    "recipientCity": null,
    "recipientStreet": null,
    "recipientAdditionalAddress": null,
    "recipientItn": null,
    "recipientPassport": null,
    "recipientIp": null,
    "recipientPhone": null,
    "recipientBirthday": null,
    "recipientGender": null,
    "recipientZipCode": null
}
```
