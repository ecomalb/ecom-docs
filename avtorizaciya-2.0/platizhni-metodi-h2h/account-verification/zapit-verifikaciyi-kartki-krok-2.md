---
description: '{{url}}/ecom/jws/payments/execute/verification_v1'
---

# Запит верифікації картки Крок 2

### Вхідні параметри частини payload JWS :

<table data-full-width="true"><thead><tr><th>Параметр</th><th width="208">Опис</th><th width="153">Формат даних</th><th width="173">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>operationId</td><td>Ід операції, який отримали на 1 кроці</td><td>string</td><td>Так</td><td>1697008393082nW0c1jr6KVv</td></tr><tr><td>encryptedCardData</td><td>термін дії карти та cvv2 зашифровані в JWE. Перші 4 символи ExpDate, наступні 3 символи cvv</td><td>string</td><td>Так</td><td>2503111 (розшифрований вигляд, у форматі YYMMCVV) </td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00 </td></tr><tr><td>browserInfo</td><td>об’єкт за даними браузера </td><td>object</td><td>Так, якщо операція потребує 3DS</td><td><br></td></tr><tr><td>browserAcceptHeader</td><td>Http заголовок запиту </td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9</td></tr><tr><td>browserUserAgent</td><td>програмний елемент браузера, що позначає систему, що користується нею</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36</td></tr><tr><td>browserLanguage</td><td>мова браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>en-US,en</td></tr><tr><td>browserColorDepth</td><td>значення глибини кольору екрана у браузері</td><td>string</td><td>Так, якщо операція потребує 3DS  </td><td>24</td></tr><tr><td>browserScreenHeight</td><td>висота області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>800</td></tr><tr><td>browserScreenWidth</td><td>широта області перегляду вікна браузера</td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>1280</td></tr><tr><td>browserTZ</td><td>Timezone браузера </td><td>string</td><td>Так, якщо операція потребує 3DS </td><td>-180</td></tr></tbody></table>

### Вихідні параметри частини payload JWS :

<table><thead><tr><th width="187.9300537109375">Параметр</th><th>Опис</th><th>Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>type</td><td>тип транзакції</td><td>string</td><td>Purchase</td></tr><tr><td>rrn</td><td>rrn номер транзакції в МПС</td><td>string</td><td>2554256963</td></tr><tr><td>purpose</td><td>призначення платежу</td><td>string</td><td>За товар</td></tr><tr><td>comment</td><td>коментар</td><td>string</td><td>тест</td></tr><tr><td>coinAmount</td><td>сума платежу</td><td>int</td><td>2000</td></tr><tr><td>merchantId</td><td>Id мерчанту</td><td>string</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>operationId</td><td>Id транзакціі</td><td>string</td><td>1712844596346b9F-WwrWZpq</td></tr><tr><td>ecomOperationId</td><td>Id транзакціі в системі Ecom</td><td>string</td><td>8c3303e9-7396-43b8-af4e-31d9facdde9b</td></tr><tr><td>merchantName</td><td>найменування торговця</td><td>string</td><td>KB test terminal</td></tr><tr><td>approvalCode</td><td>код авторизаціі</td><td>string</td><td>39203</td></tr><tr><td>status</td><td>статус транзакціі</td><td>string</td><td>SUСCESS<br>FAIL<br>PENDING<br>REQUIRED_3DS<br>DESIRED_THREEDS_MODE_ERROR</td></tr><tr><td>transactionType</td><td>тип транзакції у цифровому значенні</td><td>string</td><td>35</td></tr><tr><td>merchantRequestId</td><td>Id запиту мерчанта</td><td>string</td><td>72837906-f526-4aef-8d11-58d80b44cb75</td></tr><tr><td>transactionCurrency</td><td>валюта платежу</td><td>string</td><td>980</td></tr><tr><td>merchantCommission</td><td>сума комісії</td><td>string</td><td>2</td></tr><tr><td>creationDateTime</td><td>дата створення платежу</td><td>string</td><td>2024.09.19 15:29:25.675</td></tr><tr><td>modificationDateTime</td><td>дата модифікаціі платежу</td><td>string</td><td>2024.09.19 15:29:25.675</td></tr><tr><td>actionCode</td><td>код відповіді</td><td>string</td><td>0</td></tr><tr><td>responseCode</td><td>деталі відповіді</td><td>string</td><td>0</td></tr><tr><td>description</td><td>опис відповіді</td><td>string</td><td>approved</td></tr><tr><td>bankCode</td><td>назва банку емітента</td><td>string</td><td>BANK_ALLIANCE</td></tr><tr><td>paymentSystem</td><td>назва мпс емітента</td><td>string</td><td>MasterCard</td></tr><tr><td>productType</td><td>тип продукту термінала</td><td>string</td><td>PURCHASE</td></tr><tr><td>notificationUrl</td><td>url, на який відправлено CallBack</td><td>string</td><td><a href="https://merchant.notification_url/">https://merchant.notification_url/</a></td></tr><tr><td>paymentServiceType</td><td>тип оплати</td><td>string</td><td>CARD/APPLE_PAY/GOOGLE_PAY</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</td></tr><tr><td>cardNumberMask</td><td>маскований номер карти</td><td>string</td><td>5573********0304</td></tr><tr><td>desiredThreeDSMode</td><td>ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string</td><td>MUST/SHOULD/MUST_NOT</td></tr><tr><td>threeDSMode</td><td>параметр який вказує, використовувася 3DS у покупці чи ні</td><td>string</td><td>MUST- проводимо оплату з 3DS<br>MUST_NOT- проводимо оплату без 3DS</td></tr><tr><td>statusThreeDs</td><td>статус проведення 3DS</td><td>string</td><td>Y - успіший 3ds<br>N - не успішний 3ds</td></tr><tr><td>threeDSServerTransId</td><td>Id транзакціі в системі 3ds</td><td>string</td><td>b6c35fdb-28c1-454d-a2f3-51098c26bda4</td></tr><tr><td>acsTransId</td><td>Id транзакціі в системі ACS</td><td>string</td><td>3e17fabb-71e6-498e-8794-ef8c95c5ba6f</td></tr><tr><td>dsTransId</td><td>Id транзакціі згенерований Directory Server</td><td>string</td><td>12ebc556-82d3-4e35-9fb8-77ac18b050ea</td></tr><tr><td>eci</td><td>Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції</td><td>string</td><td>02</td></tr><tr><td>processingMerchantId</td><td>Id мерчанту в ПЦ</td><td>string</td><td>AE100000</td></tr><tr><td>processingTerminalId</td><td>Id терміналу в ПЦ</td><td>string</td><td>AE100000</td></tr><tr><td>redirect3dsUrl</td><td>url для редиректа клієнта на сторінку емітента для проходження 3DS</td><td>string</td><td><a href="https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA">https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA</a></td></tr><tr><td>txnType</td><td>під тип транзакціі</td><td>enum</td><td>Можливі значення:<br>NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається</td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td>string</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td>string</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td>string</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника</td><td>string</td><td>mail@gmail.com</td></tr><tr><td>senderCountry</td><td>країна відправника</td><td>string</td><td>Україна</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string</td><td>Київська</td></tr><tr><td>senderCity</td><td>місто відправника</td><td>string</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string</td><td>АН123456</td></tr><tr><td>senderIp</td><td><code class="expression">space.vars.senderIP_description</code></td><td>string</td><td><code class="expression">space.vars.senderIP_example</code></td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>гендер відправника</td><td>string</td><td>M</td></tr><tr><td>senderZipCode</td><td>індекс відправника</td><td>string</td><td>12000</td></tr><tr><td>senderBankCode</td><td>назва банку емітента відправника</td><td>string</td><td>BANK_ALLIANCE</td></tr><tr><td>senderPaymentSystem</td><td>назва мпс емітента відправника</td><td>string</td><td>MasterCard</td></tr><tr><td>senderCardNumberMask</td><td>маскований номер карти відправника</td><td>string</td><td>5573********0304</td></tr><tr><td>externalCardToken</td><td>id токену</td><td>string</td><td>tmkEYenZSa8FV03aawVXxbep</td></tr></tbody></table>

### Приклади :

<details>

<summary>JWS Payload — тіло запиту перед підписанням</summary>

```
{
    "operationId": "{{operationId}}",
    "encryptedCardData": "{{encryptedCardData}}",
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

<summary>JWS Payload — тіло відповіді перед підписанням без 3дс</summary>

```
{
    "type": "VERIFICATION",
    "rrn": "509310723011",
    "purpose": "",
    "comment": "",
    "coinAmount": 0,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120",
    "operationId": "17436771609101HDujgZphks",
    "ecomOperationId": "1c97b778-d8d0-4680-89eb-8015842b45a3",
    "status": "SUCCESS",
    "transactionType": 215,
    "merchantRequestId": "03185335-3a9f-4aad-a3b9-c8b1e6d4051b",
    "transactionCurrency": "980",
    "creationDateTime": "2025.04.03 13:46:00.846",
    "modificationDateTime": "2025.04.03 13:46:01.465",
    "transactionResponseInfo": {
        "actionCode": "0",
        "responseCode": "00",
        "description": "Операція успішна"
    },
    "productType": "PURCHASE",
    "notificationUrl": "test",
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "processingTerminalId": "AE001001",
    "processingMerchantId": "AE001001",
    "creatorSystem": "H2H",
    "desiredThreeDSMode": "MUST_NOT",
    "threeDSMode": "MUST_NOT",
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

</details>

<details>

<summary>JWS Payload — тіло відповіді перед підписанням з 3дс</summary>

```
{
    "type": "VERIFICATION",
    "purpose": "",
    "comment": "",
    "coinAmount": 0,
    "merchantId": "137d9304-0368-11ed-b939-0242ac1200",
    "operationId": "1743677843021zx9DLwCfxz-",
    "ecomOperationId": "d8abe162-99a1-4cb9-8611-8b610cda510b",
    "status": "REQUIRED_3DS",
    "transactionType": 215,
    "merchantRequestId": "f821a5fa-cbfb-4ace-9c2f-83abc799d3a9",
    "transactionCurrency": "980",
    "creationDateTime": "2025.04.03 13:57:22.957",
    "modificationDateTime": "2025.04.03 13:57:23.752",
    "transactionResponseInfo": {},
    "productType": "PURCHASE",
    "notificationUrl": "test",
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "processingTerminalId": "AE001001",
    "processingMerchantId": "AE001001",
    "creatorSystem": "H2H",
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "threeDSServerTransId": "1a85c9f3-c19c-448a-a4bb-04f265b62a28",
    "redirect3dsUrl": "https://api-ecom-preprod.develop.bankalliance.ua/threeDS/getRedirectHtml/1743677843021zx9DLwCfxz-",
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

</details>





