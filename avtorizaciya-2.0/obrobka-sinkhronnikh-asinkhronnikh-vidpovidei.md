---
description: Всі відповіді асинхронні та синхронні будуть підписані.
---

# Обробка синхронних/асинхронних відповідей

## Структура відповіді

Усі відповіді сервісу передаються **у форматі JWS (JSON Web Signature)**&#x20;

Це гарантує:

* **цілісність** даних — повідомлення не було змінено під час передачі;
* **автентичність** джерела — запит дійсно надійшов від авторизованого сервісу.

Повідомлення JWS має вигляд:

```
<base64Url(header)>.<base64Url(payload)>.<base64Url(signature)>
```

### **Кодування Header і Payload**

Обидві частини (`header`, `payload`) **не шифруються**, а лише **кодуються у формат Base64Url**.\
Тобто, їх можна декодувати для перегляду змісту, але змінювати — ні (це зламає підпис).

> **Параметр `Signature`** забезпечує гарантію, що навіть якщо хтось змінить одне поле у `payload`, підпис стане невалідним.

#### **Приклад вигляду закодованих даних:**&#x20;

{% tabs %}
{% tab title="Закодована частина header" %}
```
eyJhbGciOiJFUzI1NiIsImtpZCI6IjYwMjE3ZDU2LTJkMzYtNDhlMy1hYmU4LTVjMDBiNDJjYTg4NSJ9
```
{% endtab %}

{% tab title="Розкодована частина header" %}
```json
{
"alg": "ES256",
"kid": "60217d56-2d36-48e3-abe8-5c00b42ca885"
} 
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Закодована частина payload" %}
```
eyJ0eXBlIjoiQUNDT1VOVF8yX0NBUkQiLCJycm4iOiI1MzE3MTU5MzczMDUiLCJwdXJwb3NlIjoi0LfQsCDRgtC-0LLQsNGAIiwiY29pbkFtb3VudCI6MTAsIm1lcmNoYW50SWQiOiIxMzdkOTMwNC0wMzY4LTExZWQtYjkzOS0wMjQyYWMxMjAwMDIiLCJvcGVyYXRpb25JZCI6IjE3NjMwNDY5NjQyODl5R2pEZDJ1RVBrWSIsImVjb21PcGVyYXRpb25JZCI6ImQ1Y2RlYzg0LWNkYzUtNDVjMi1hZmEyLWQ4MWJmZDc5ZmU2MSIsInN0YXR1cyI6IlNVQ0NFU1MiLCJ0cmFuc2FjdGlvblR5cGUiOjQ2LCJtZXJjaGFudFJlcXVlc3RJZCI6IjA0MDIyNjVkLWMwYzYtNDNlYi05NDhlLTAyMzEwYzMzMWEzMyIsInRyYW5zYWN0aW9uQ3VycmVuY3kiOiI5ODAiLCJtZXJjaGFudENvbW1pc3Npb24iOjAsImNyZWF0aW9uRGF0ZVRpbWUiOiIyMDI1LjExLjEzIDE3OjE2OjA0LjIyNyIsIm1vZGlmaWNhdGlvbkRhdGVUaW1lIjoiMjAyNS4xMS4xMyAxNzoxNjowNC4yMjciLCJ0cmFuc2FjdGlvblJlc3BvbnNlSW5mbyI6eyJhY3Rpb25Db2RlIjoiMCIsInJlc3BvbnNlQ29kZSI6IjAwIiwiZGVzY3JpcHRpb24iOiLQntC_0LXRgNCw0YbRltGPINGD0YHQv9GW0YjQvdCwIn0sInByb2R1Y3RUeXBlIjoiQTJDIiwibm90aWZpY2F0aW9uVXJsIjoiaHR0cHM6Ly93ZWJob29rLnNpdGUvNDExNjM0ZjQtNmMxNy00ODYyLTg4NTYtZDA2NGY3ZjIxMzVhIiwicGF5bWVudFNlcnZpY2VUeXBlIjoiQ0FSRCIsIm5vdGlmaWNhdGlvbkVuY3J5cHRpb24iOmZhbHNlLCJub3RpZmljYXRpb25TaWduYXR1cmUiOnRydWUsInByb2Nlc3NpbmdUZXJtaW5hbElkIjoiQUUwMDEwMDQiLCJwcm9jZXNzaW5nTWVyY2hhbnRJZCI6IkFFMDAxMDA0IiwiY3JlYXRvclN5c3RlbSI6IkgySCIsImJhbGFuY2VBbW91bnRBZnRlciI6OTkwMTAxOTY5NDQ5MTMsInNlbmRlckN1c3RvbWVySWQiOiIwMDAwMDAiLCJzZW5kZXJGaXJzdE5hbWUiOiJzZW5kZXJGaXJzdE5zZW5kZXJGaXJzdE5hbWVzZW4iLCJzZW5kZXJMYXN0TmFtZSI6InNlbmRlckxhc3ROYW1lc2VuZGVyTGFzdE5hbWVzZSIsInNlbmRlck1pZGRsZU5hbWUiOiJzZW5kZXJNaWRkbGVOYW1lc2VuZGVyTWlkZGxlTmEiLCJzZW5kZXJDb3VudHJ5IjoiODA0Iiwic2VuZGVyUmVnaW9uIjoic2VuZGVyX3JlZ2lvbiIsInNlbmRlckNpdHkiOiJzZW5kZXJfY2l0eSIsInNlbmRlclN0cmVldCI6InNlbmRlcl9zdHJlZXQiLCJzZW5kZXJBZGRpdGlvbmFsQWRkcmVzcyI6Ik4gNiIsInNlbmRlckl0biI6IjEyMzQ1Iiwic2VuZGVyUGFzc3BvcnQiOiIxMjM0NSIsInNlbmRlcklwIjoiMTY1LjIyMi44Ny4yMjQiLCJzZW5kZXJQaG9uZSI6IjM4MDk2NzU0MjM0NCIsInNlbmRlckJpcnRoZGF5IjoiMTIxMjIwMDAiLCJzZW5kZXJHZW5kZXIiOiJNYWxlIiwic2VuZGVyWmlwQ29kZSI6IjEyMzQ1IiwicmVjaXBpZW50Q3VzdG9tZXJJZCI6IjEyMzQ1NjciLCJyZWNpcGllbnRGaXJzdE5hbWUiOiJyZWNpcGllbnRGaXJzdE5yZWNpcGllbnRGaXJzdE4iLCJyZWNpcGllbnRMYXN0TmFtZSI6InJlY2lwaWVudExhc3N0TnJlY2lwaWVudExhc3N0TiIsInJlY2lwaWVudE1pZGRsZU5hbWUiOiJyZWNpcGllbnRNaWRkbGVOYW1lcmVjaXBpZW50TWkiLCJyZWNpcGllbnRFbWFpbCI6InLRhNGEQGdtYWlsLmNvbSIsInJlY2lwaWVudENvdW50cnkiOiI4MDQiLCJyZWNpcGllbnRSZWdpb24iOiJyZXNfcmVnIiwicmVjaXBpZW50Q2l0eSI6InJlc19kbmlwcm8iLCJyZWNpcGllbnRTdHJlZXQiOiJyZXNfc3RyZWV0IiwicmVjaXBpZW50QWRkaXRpb25hbEFkZHJlc3MiOiJyZXNfYWRkcmVzIiwicmVjaXBpZW50SXRuIjoiMTIzNDU2Nzg5MCIsInJlY2lwaWVudFBhc3Nwb3J0IjoicmVzX3Bhc3BvcnQiLCJyZWNpcGllbnRJcCI6IjE2NS4yMjIuODcuMjI0IiwicmVjaXBpZW50UGhvbmUiOiIzODA5Njc1NDIzNDQiLCJyZWNpcGllbnRCaXJ0aGRheSI6IjEyMTIyMDAwIiwicmVjaXBpZW50R2VuZGVyIjoiRmVtYWxlIiwicmVjaXBpZW50WmlwQ29kZSI6Ijc3Nzc3In0
```
{% endtab %}

{% tab title="Розкодована частина payload" %}
{% code expandable="true" %}
```json
{
  "type": "ACCOUNT_2_CARD",
  "rrn": "531715937305",
  "purpose": "за товар",
  "coinAmount": 10,
  "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
  "operationId": "1763046964289yGjDd2uEPkY",
  "ecomOperationId": "d5cdec84-cdc5-45c2-afa2-d81bfd79fe61",
  "status": "SUCCESS",
  "transactionType": 46,
  "merchantRequestId": "0402265d-c0c6-43eb-948e-02310c331a33",
  "transactionCurrency": "980",
  "merchantCommission": 0,
  "creationDateTime": "2025.11.13 17:16:04.227",
  "modificationDateTime": "2025.11.13 17:16:04.227",
  "transactionResponseInfo": {
    "actionCode": "0",
    "responseCode": "00",
    "description": "Операція успішна"
  },
  "productType": "A2C",
  "notificationUrl": "https://webhook.site/411634f4-6c17-4862-8856-d064f7f2135a",
  "paymentServiceType": "CARD",
  "notificationEncryption": false,
  "notificationSignature": true,
  "processingTerminalId": "AE001004",
  "processingMerchantId": "AE001004",
  "creatorSystem": "H2H",
  "balanceAmountAfter": 99010196944913,
  "senderCustomerId": "000000",
  "senderFirstName": "senderFirstNsenderFirstNamesen",
  "senderLastName": "senderLastNamesenderLastNamese",
  "senderMiddleName": "senderMiddleNamesenderMiddleNa",
  "senderCountry": "804",
  "senderRegion": "sender_region",
  "senderCity": "sender_city",
  "senderStreet": "sender_street",
  "senderAdditionalAddress": "N 6",
  "senderItn": "12345",
  "senderPassport": "12345",
  "senderIp": "165.222.87.224",
  "senderPhone": "380967542344",
  "senderBirthday": "12122000",
  "senderGender": "Male",
  "senderZipCode": "12345",
  "recipientCustomerId": "1234567",
  "recipientFirstName": "recipientFirstNrecipientFirstN",
  "recipientLastName": "recipientLasstNrecipientLasstN",
  "recipientMiddleName": "recipientMiddleNamerecipientMi",
  "recipientEmail": "rфф@gmail.com",
  "recipientCountry": "804",
  "recipientRegion": "res_reg",
  "recipientCity": "res_dnipro",
  "recipientStreet": "res_street",
  "recipientAdditionalAddress": "res_addres",
  "recipientItn": "1234567890",
  "recipientPassport": "res_pasport",
  "recipientIp": "165.222.87.224",
  "recipientPhone": "380967542344",
  "recipientBirthday": "12122000",
  "recipientGender": "Female",
  "recipientZipCode": "77777"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## **Перевірка підпису**

Параметр `kid` (Key ID) у JWS Header визначає, **який саме публічний ключ** слід використовувати для перевірки підпису.

У разі, якщо ключова пара оновлюється, сервер формує відповіді з новим `kid`.\
Клієнт має:

1. Отримати новий `kid` з header JWS;
2. Виконати запит на [`/ecom/keys/public_key/get_v1`](https://docs.merchant.alb.ua/avtorizaciya-2.0/obrobka-sinkhronnikh-asinkhronnikh-vidpovidei#post-ecom-keys-public_key-get_v1) для отримання відповідного публічного ключа;
3. Використати цей ключ для перевірки підпису наступних повідомлень.

Для перевірки підпису, потрібно розкодувати частину `header`  де буде знаходитись параметр `kid` .&#x20;



{% openapi-operation spec="GetPublicKeyJWS" path="/ecom/keys/public_key/get_v1" method="post" %}
[OpenAPI GetPublicKeyJWS](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/52a92546b62fc6f18792744303c1d4a50893fffbe7eddee69a0b878a5a279a6c.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251211%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251211T111827Z&X-Amz-Expires=172800&X-Amz-Signature=da34b48bf92658f69d849b45547f37cabccd3ea025a2aa8e38e2ed6ded8a139f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
