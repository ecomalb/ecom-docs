---
description: '{{url}}/ecom/jws/payments/execute/card_to_account_v1'
---

# Запит проведення C2A Крок 2

### **Вхідні параметри** ч**астини payload JWS :**

<table data-full-width="true"><thead><tr><th>Параметр</th><th>Опис</th><th width="142">Формат даних</th><th width="184">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>operationId</td><td>Ід операції, який отримали на 1 кроці</td><td>string</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>encryptedCardData</td><td><p></p><p>термін дії карти та cvv2 зашифровані в JWE. Перші 4 символи ExpDate, наступні 3 символи cvv</p><p></p><ul><li>Якщо в параметр <code>TxnType</code> передається <code>"NONCVV\noncvv"</code> тоді у параметрі <code>ecnryptedCardData</code> потрібно передати лише <strong>YYMM</strong> без <strong>CVV</strong></li><li>У іншому випадку якщо в <code>TxnType</code> нічого не педеається, тоді у параметрі <code>encryptedCardData</code> піотрбно обов'язкового передавати у форматі <strong>YYMMCVV</strong></li></ul></td><td>string</td><td>Так</td><td>2503111 (розшифрований вигляд)</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00 </td></tr><tr><td>browserInfo</td><td>об’єкт за даними браузера </td><td>object</td><td>Так, якщо операція потребує 3DS</td><td><br></td></tr><tr><td>browserAcceptHeader</td><td>Http заголовок запиту </td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9</td></tr><tr><td>browserUserAgent</td><td>програмний елемент браузера, що позначає систему, що користується нею</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36</td></tr><tr><td>browserLanguage</td><td>мова браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>en-US,en</td></tr><tr><td>browserColorDepth</td><td>значення глибини кольору екрана у браузері</td><td>string</td><td>Так, якщо операція потребує 3DS  </td><td>24</td></tr><tr><td>browserScreenHeight</td><td>висота області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>800</td></tr><tr><td>browserScreenWidth</td><td>широта області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>1280</td></tr><tr><td>browserTZ</td><td>Timezone браузера </td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>-180</td></tr></tbody></table>

### **Вихідні параметри** ч**астини payload JWS :**

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
| recipientIp                | <code class="expression">space.vars.recipientIP_desctiption</code>       | string       | <code class="expression">space.vars.recipientIP_example</code>                                                                                                                                         |
| recipientPhone             | номер телефону отримувача                                                | string       | 380630000000                                                                                                                                                                                           |
| recipientBirthday          | день народження отримувача                                               | string       | 31.12.2000                                                                                                                                                                                             |
| recipientGender            | гендер отримувача                                                        | string       | M                                                                                                                                                                                                      |
| recipientZipCode           | індекс отримувача                                                        | string       | 12000                                                                                                                                                                                                  |
| recipientBankCode          | назва банку емітента отримувача                                          | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| recipientPaymentSystem     | назва мпс емітента отримувача                                            | string       | MasterCard                                                                                                                                                                                             |
| recipientCardNumberMask    | маскований номер карти отримувача                                        | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| externalCardToken          | id токену                                                                | string       | tmkEYenZSa8FV03aawVXxbep                                                                                                                                                                               |



### Приклади : <a href="#prikladi" id="prikladi"></a>

<details>

<summary>ExpandJWS Payload — тіло запиту перед підписанням</summary>

```json
{
    "operationId": "{{operationIdT}}",
    "encryptedCardData": "{{encryptedDateAndSecurityT}}",
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

<summary>ExpandJWS Payload — тіло відповіді перед підписанням без 3дс</summary>

```json
{
    "type": "CARD_2_ACCOUNT",
    "rrn": "410208187342",
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": 1010,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712823122106xnUK8T9Z9d8",
    "ecomOperationId": "a4842af1-ab80-4685-9cef-0d97aedbb99f",
    "merchantName": null,
    "approvalCode": null,
    "status": "SUCCESS",
    "transactionType": 62,
    "merchantRequestId": "0d7a190d-9cfc-4b01-9615-e207ebe8b23b",
    "transactionCurrency": "980",
    "merchantCommission": 67,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": "Операція успішна"
    },
    "bankCode": null,
    "paymentSystem": null,
    "productType": "C2A",
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "senderCardNumberMask": null,
    "desiredThreeDSMode": "MUST_NOT",
    "threeDSMode": "MUST_NOT",
    "statusThreeDs": null,
    "threeDSServerTransId": null,
    "redirect3dsUrl": null,
    "recipientAccount": null,
    "senderCustomerId": null,
    "senderFirstName": "FirstName",
    "senderLastName": "Name",
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": "Ukraine",
    "senderRegion": null,
    "senderCity": "City",
    "senderStreet": "Str.",
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
    "recipientZipCode": null,
    "externalCardToken": "tmkEYenZSa8FV03aawVXxbep"
}
```



</details>

<details>

<summary>ExpandJWS Payload — тіло відповіді перед підписанням з 3дс</summary>

```json
{
    "type": "CARD_2_ACCOUNT",
    "rrn": null,
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": 1010,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712823334404zicRAYWIAm1",
    "ecomOperationId": "412ac336-aac5-43b5-8d35-b57ffa9d53ff",
    "merchantName": null,
    "approvalCode": null,
    "status": "REQUIRED_3DS",
    "transactionType": 62,
    "merchantRequestId": "60cb4f84-add5-48c6-984f-7b20a6b50c75",
    "transactionCurrency": "980",
    "merchantCommission": 67,
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
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "senderCardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "db259063-61ba-4681-a7e9-65fbbebead2d",
    "redirect3dsUrl": "https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1712823334404zicRAYWIAm1",
    "recipientAccount": null,
    "senderCustomerId": null,
    "senderFirstName": "FirstName",
    "senderLastName": "Name",
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": "Ukraine",
    "senderRegion": null,
    "senderCity": "City",
    "senderStreet": "Str.",
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
    "recipientZipCode": null,
    "externalCardToken": "tmkEYenZSa8FV03aawVXxbep"
}
```



</details>
