---
description: >-
  Для відправки Callback буде виконаний Post запит на notificationUrl який був
  вказаний в запиті на проведення платежу. Шифрування Callback регулюється
  параметром notificationEncryption
---

# Callback

* Якщо статус отримання Callback не 200 ОК, відбувається перевідправка Callback через 5 сек, потім через 30 сек, потім через 5 хв, потім через 30 хв, через 1 годину
* Якщо статус отримання Callback не 200 ОК для 1-го разу, а для 2-го разу 200 ОК, то перевідправка Callback більше не виконується&#x20;



#### **Вхідні параметри**

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="141">Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>type</td><td>тип транзакції</td><td>string</td><td>Purchase, CARD_2_ACCOUNT, ACCOUNT_2_CARD,REFUND</td></tr><tr><td>rrn</td><td>rrn номер транзакції в МПС</td><td>string</td><td>2554256963</td></tr><tr><td>purpose</td><td>призначення платежу</td><td>string</td><td>За товар</td></tr><tr><td>comment</td><td>коментар</td><td>string</td><td>тест</td></tr><tr><td>coinAmount</td><td>сума платежу</td><td>int</td><td>2000</td></tr><tr><td>merchantId</td><td>Id мерчанту</td><td>string</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>operationId</td><td>Id транзакціі</td><td>string</td><td>1712844596346b9F-WwrWZpq</td></tr><tr><td>ecomOperationId</td><td>Id транзакціі в системі Ecom</td><td>string</td><td>8c3303e9-7396-43b8-af4e-31d9facdde9b</td></tr><tr><td>merchantName</td><td>найменування торговця</td><td>string</td><td>KB test terminal</td></tr><tr><td>approvalCode</td><td>код авторизаціі</td><td>string</td><td>39203</td></tr><tr><td>status</td><td>статус транзакціі</td><td>string</td><td>SUСCESS<br>FAIL<br>PENDING<br>REQUIRED_3DS<br>DESIRED_THREEDS_MODE_ERROR</td></tr><tr><td>transactionType</td><td>тип транзакції у цифровому значенні</td><td>string</td><td>35</td></tr><tr><td>merchantRequestId</td><td>Id запиту мерчанта</td><td>string</td><td>72837906-f526-4aef-8d11-58d80b44cb75</td></tr><tr><td>transactionCurrency</td><td>валюта платежу</td><td>string</td><td>980</td></tr><tr><td>merchantCommission</td><td>сума комісії</td><td>string</td><td>2</td></tr><tr><td>createDateTime</td><td>дата створення платежу</td><td>string</td><td>2024.09.19 15:29:25.675</td></tr><tr><td>modificationDateTime</td><td>дата модифікаціі платежу</td><td>string</td><td>2024.09.19 15:29:25.675</td></tr><tr><td>actionCode</td><td>код відповіді</td><td>string</td><td>0</td></tr><tr><td>responseCode</td><td>деталі відповіді</td><td>string</td><td>0</td></tr><tr><td>description</td><td>опис відповіді</td><td>string</td><td>approved</td></tr><tr><td>bankCode</td><td>назва банку емітента</td><td>string</td><td>BANK_ALLIANCE</td></tr><tr><td>paymentSystem</td><td>назва мпс емітента</td><td>string</td><td>MasterCard</td></tr><tr><td>productType</td><td>тип продукту термінала</td><td>string</td><td>PURCHASE</td></tr><tr><td>notificationUrl</td><td>url, на який відправлено CallBack</td><td>string</td><td><a href="https://merchant.notification_url/">https://merchant.notification_url/</a></td></tr><tr><td>paymentServiceType</td><td>тип оплати</td><td>string</td><td>CARD/APPLE_PAY/GOOGLE_PAY</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</td></tr><tr><td>cardNumberMask</td><td>маскований номер карти</td><td>string</td><td>5573********0304</td></tr><tr><td>desiredThreeDSMode</td><td>ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string</td><td>MUST/SHOULD/MUST_NOT</td></tr><tr><td>threeDSMode</td><td>параметр який вказує, використовувася 3DS у покупці чи ні</td><td>string</td><td>MUST- проводимо оплату з 3DS<br>MUST_NOT- проводимо оплату без 3DS</td></tr><tr><td>statusThreeDs</td><td>статус проведення 3DS</td><td>string</td><td>Y - успіший 3ds<br>N - не успішний 3ds</td></tr><tr><td>threeDSServerTransId</td><td>Id транзакціі в системі 3ds</td><td>string</td><td>b6c35fdb-28c1-454d-a2f3-51098c26bda4</td></tr><tr><td>acsTransId</td><td>Id транзакціі в системі ACS</td><td>string</td><td>3e17fabb-71e6-498e-8794-ef8c95c5ba6f</td></tr><tr><td>dsTransId</td><td>Id транзакціі згенерований Directory Server</td><td>string</td><td>12ebc556-82d3-4e35-9fb8-77ac18b050ea</td></tr><tr><td>eci</td><td>Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції</td><td>string</td><td>02</td></tr><tr><td>processingMerchantId</td><td>Id мерчанту в ПЦ</td><td>string</td><td>AE100000</td></tr><tr><td>processingTerminalId</td><td>Id терміналу в ПЦ</td><td>string</td><td>AE100000</td></tr><tr><td>redirect3dsUrl</td><td>url для редиректа клієнта на сторінку емітента для проходження 3DS</td><td>string</td><td><a href="https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA">https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA</a></td></tr><tr><td>txnType</td><td>під тип транзакціі</td><td>enum</td><td>Можливі значення:<br>NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається</td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>прізвище відправника</td><td>string</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>ім'я відправника</td><td>string</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td>string</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника</td><td>string</td><td>mail@gmail.com</td></tr><tr><td>senderCountry</td><td>країна відправника</td><td>string</td><td>Україна</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string</td><td>Київська</td></tr><tr><td>senderCity</td><td>місто відправника</td><td>string</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string</td><td>АН123456</td></tr><tr><td>senderIp</td><td>ip адреса відправника</td><td>string</td><td>123.12.12.12</td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>гендер відправника</td><td>string</td><td>M</td></tr><tr><td>senderZipCode</td><td>індекс відправника</td><td>string</td><td>12000</td></tr><tr><td>senderBankCode</td><td>назва банку емітента відправника</td><td>string</td><td>BANK_ALLIANCE</td></tr><tr><td>senderPaymentSystem</td><td>назва мпс емітента відправника</td><td>string</td><td>MasterCard</td></tr><tr><td>senderCardNumberMask</td><td>маскований номер карти відправника</td><td>string</td><td>5573********0304</td></tr><tr><td>recipientCustomerId</td><td>Id клієнта відправника</td><td>string</td><td>1258728c1</td></tr><tr><td>recipientFirstName</td><td>прізвище отримувача</td><td>string</td><td>Іваненко</td></tr><tr><td>recipientLastName</td><td>ім'я отримувача</td><td>string</td><td>Іван</td></tr><tr><td>recipientMiddleName</td><td>по-батькові отримувача</td><td>string</td><td>Іванович</td></tr><tr><td>recipientEmail</td><td>пошта отримувача</td><td>string</td><td>mail@gmail.com</td></tr><tr><td>recipientCountry</td><td>країна отримувача</td><td>string</td><td>Україна</td></tr><tr><td>recipientRegion</td><td>область отримувача</td><td>string</td><td>Київська</td></tr><tr><td>recipientCity</td><td>місто отримувача</td><td>string</td><td>Київ</td></tr><tr><td>recipientStreet</td><td>вулиця отримувача</td><td>string</td><td>Січових стрільців</td></tr><tr><td>recipientAdditionalAddress</td><td>додаткові дані адреси отримувача (поверх, номер дому, квартира)</td><td>string</td><td>23</td></tr><tr><td>recipientItn</td><td>іпн отримувача</td><td>string</td><td>123456789</td></tr><tr><td>recipientPassport</td><td>паспорт отримувача</td><td>string</td><td>АН123456</td></tr><tr><td>recipientIp</td><td>ip адреса отримувача</td><td>string</td><td>123.12.12.12</td></tr><tr><td>recipientPhone</td><td>номер телефону отримувача</td><td>string</td><td>380630000000</td></tr><tr><td>recipientBirthday</td><td>день народження отримувача</td><td>string</td><td>31.12.2000</td></tr><tr><td>recipientGender</td><td>гендер отримувача</td><td>string</td><td>M</td></tr><tr><td>recipientZipCode</td><td>індекс отримувача</td><td>string</td><td>12000</td></tr><tr><td>recipientBankCode</td><td>назва банку емітента отримувача</td><td>string</td><td>BANK_ALLIANCE</td></tr><tr><td>recipientPaymentSystem</td><td>назва мпс емітента отримувача</td><td>string</td><td>MasterCard</td></tr><tr><td>recipientCardNumberMask</td><td>маскований номер карти отримувача</td><td>string</td><td>5573********0304</td></tr><tr><td>originalOperationId</td><td>id під яким створено оригінальну операцію</td><td>string</td><td>1712843529623cHAHkmt-G5u</td></tr><tr><td>originalCoinAmount</td><td>Сума оригінального платежу</td><td>int</td><td>100</td></tr><tr><td>originalEcomOperationId</td><td>id в системі Еком під яким створено оригінальну операцію</td><td>string</td><td>c25ee1cb-a052-439b-b075-bcb632615b11</td></tr><tr><td>rrnOriginal</td><td>rrn номер оригінальної транзакції в МПС</td><td>string</td><td>123456789</td></tr></tbody></table>

#### Приклад тіла запиту

```json
{
   "type":"CARD_2_ACCOUNT",
   "rrn":"401613120895",
   "purpose":"purpose",
   "comment":null,
   "coinAmount":1010,
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "operationId":"1705411028563HDJi1gScHJT",
   "merchantName":"KB test terminal",
   "approvalCode":"058669",
   "status":"SUCCESS",
   "transactionType":62,
   "merchantRequestId":"d6ca07a8-dc4d-425c-8fa8-4512fe852b3e",
   "transactionCurrency":"980",
   "merchantCommission":0,
   "createDateTime": "2024.09.19 15:29:25.675",
   "modificationDateTime": "2024.09.19 15:29:25.675",
   "transactionResponseInfo":{
      "actionCode":"0",
      "responseCode":"00",
      "description":"approved"
   },
   "bankCode":"BANK_ALLIANCE",
   "paymentSystem":"MasterCard",
   "productType":"C2A",
   "notificationUrl":"://webhook.site/db36dec8-c6fa-4ed5-8726-8d9c583c0103",
   "senderCity":"MISTO KYIV",
   "senderStreet":"VUL. MOSKOVSKA, BUD. 32/2, KV. 178",
   "senderCountry":"804",
   "recipientAccount":"_",
   "senderLastName":"TESTOVA",
   "senderFirstName":"IRYNA",
   "senderCardNumberMask":"523244••••••0177",
   "desiredThreeDSMode":"MUST_NOT",
   "threeDSMode":"MUST_NOT",
   "statusThreeDs":null,
   "threeDSServerTransID":null,
   "redirect3dsUrl":null
}

```

Приклад відповіді&#x20;

```http
HTTP 200 OK
```
