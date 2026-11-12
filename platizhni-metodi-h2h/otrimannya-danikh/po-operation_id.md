---
description: '{{url}}/ecom/execute_request/payments/v1/operations'
---

# по OPERATION\_ID

**Вихідні параметри:**

<table><thead><tr><th width="129">Параметр</th><th width="130">Опис</th><th width="141">Формат даних</th><th width="132">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>id</td><td>Id транзакціі</td><td>string</td><td>Так</td><td>1712844596346b9F-WwrWZpq</td></tr></tbody></table>

#### **Вихідні параметри**

| Параметр                | Опис                                                                                                               | Формат даних | Приклад                                                                                                                               |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| type                    | Тип транзакції                                                                                                     | string       | PURCHASE, CARD\_2\_ACCOUNT, ACCOUNT\_2\_CARD, REFUND                                                                                  |
| rrn                     | RRN — номер транзакції в МПС                                                                                       | string       | 123456789012                                                                                                                          |
| purpose                 | Призначення платежу                                                                                                | string       | Test payment for Order №123                                                                                                           |
| comment                 | Коментар до платежу                                                                                                | string       | тест                                                                                                                                  |
| coinAmount              | Сума платежу в копійках                                                                                            | int          | 4530                                                                                                                                  |
| merchantId              | ID мерчанта                                                                                                        | string       | TEST\_MERCHANT\_001                                                                                                                   |
| operationId             | ID транзакції                                                                                                      | string       | TEST\_OPERATION\_001                                                                                                                  |
| ecomOperationId         | ID транзакції в системі Ecom                                                                                       | string       | TEST\_ECOM\_OPERATION\_001                                                                                                            |
| merchantName            | Найменування торговця                                                                                              | string       | Test Merchant                                                                                                                         |
| merchantRequestId       | ID запиту мерчанта, переданого під час створення платежу                                                           | string       | TEST\_REQUEST\_001                                                                                                                    |
| approvalCode            | Код авторизації транзакції                                                                                         | string       | 123456                                                                                                                                |
| status                  | Статус транзакції                                                                                                  | string       | SUCCESS, FAIL, PENDING, REQUIRED\_3DS, DESIRED\_THREEDS\_MODE\_ERROR                                                                  |
| transactionType         | Тип транзакції у цифровому значенні                                                                                | int          | 35                                                                                                                                    |
| transactionCurrency     | Код валюти платежу відповідно до ISO 4217                                                                          | string       | 980                                                                                                                                   |
| creationDateTime        | Дата та час створення платежу                                                                                      | string       | 2026.11.11 17:03:50.127                                                                                                               |
| modificationDateTime    | Дата та час останньої модифікації платежу                                                                          | string       | 2026.11.11 17:05:02.672                                                                                                               |
| transactionResponseInfo | Об'єкт з інформацією про відповідь процесингу                                                                      | object       | —                                                                                                                                     |
| actionCode              | Код відповіді процесингу                                                                                           | string       | 0                                                                                                                                     |
| responseCode            | Код результату обробки транзакції                                                                                  | string       | 00                                                                                                                                    |
| description             | Опис результату обробки транзакції                                                                                 | string       | approved                                                                                                                              |
| bankCode                | Код/назва банку-емітента картки                                                                                    | string       | TEST\_BANK                                                                                                                            |
| paymentSystem           | Назва платіжної системи емітента                                                                                   | string       | VISA                                                                                                                                  |
| paymentServiceType      | Тип платіжного сервісу, використаного для оплати                                                                   | string       | CARD, APPLE\_PAY, GOOGLE\_PAY                                                                                                         |
| notificationUrl         | URL, на який надсилається Callback щодо операції                                                                   | string       | [https://test.merchant.com/callback](https://test.merchant.com/callback?utm_source=chatgpt.com)                                       |
| notificationEncryption  | Ознака шифрування даних Callback. Якщо параметр не переданий або має значення `false`, дані Callback не шифруються | boolean      | false                                                                                                                                 |
| notificationSignature   | Ознака використання підпису Callback                                                                               | boolean      | true                                                                                                                                  |
| hppOrderId              | ID замовлення HPP, у межах якого створено операцію                                                                 | string       | TEST\_HPP\_ORDER\_001                                                                                                                 |
| processingTerminalId    | ID терміналу в процесинговому центрі                                                                               | string       | TEST\_TERMINAL\_001                                                                                                                   |
| processingMerchantId    | ID мерчанта в процесинговому центрі                                                                                | string       | TEST\_PROCESSING\_MERCHANT\_001                                                                                                       |
| creatorSystem           | Назва системи, з якої було створено операцію                                                                       | string       | HPP                                                                                                                                   |
| sourceAmount            | Початкова сума платежу до конвертації в копійках                                                                   | int          | 100                                                                                                                                   |
| sourceCurrencyCode      | Код початкової валюти платежу до конвертації відповідно до ISO 4217                                                | string       | 840                                                                                                                                   |
| conversionRate          | Курс конвертації початкової валюти платежу у валюту операції                                                       | string       | 45.3000                                                                                                                               |
| cardNumberMask          | Маскований номер картки платника                                                                                   | string       | 411111\*\*\*\*\*\*1111                                                                                                                |
| desiredThreeDSMode      | Бажаний режим використання 3DS, переданий мерчантом                                                                | string       | MUST, SHOULD, MUST\_NOT                                                                                                               |
| threeDSMode             | Фактичний режим проведення платежу з використанням 3DS                                                             | string       | MUST, MUST\_NOT                                                                                                                       |
| acsTransId              | ID транзакції в системі ACS                                                                                        | string       | TEST\_ACS\_TRANS\_ID\_001                                                                                                             |
| dsTransId               | ID транзакції, згенерований Directory Server                                                                       | string       | TEST\_DS\_TRANS\_ID\_001                                                                                                              |
| eci                     | Electronic Commerce Indicator — код, що визначає рівень безпеки транзакції                                         | string       | 05                                                                                                                                    |
| statusThreeDs           | Статус проходження 3DS                                                                                             | string       | Y — успішний, N — неуспішний                                                                                                          |
| threeDSServerTransId    | ID транзакції в системі 3DS Server                                                                                 | string       | TEST\_3DS\_SERVER\_TRANS\_ID\_001                                                                                                     |
| senderCustomerId        | ID клієнта-відправника                                                                                             | string       | TEST\_CUSTOMER\_001                                                                                                                   |
| senderFirstName         | Ім'я відправника                                                                                                   | string       | Test                                                                                                                                  |
| senderLastName          | Прізвище відправника                                                                                               | string       | User                                                                                                                                  |
| senderMiddleName        | По батькові відправника                                                                                            | string       | Testovich                                                                                                                             |
| senderEmail             | Електронна пошта відправника                                                                                       | string       | test@example.com                                                                                                                      |
| senderCountry           | Код країни відправника                                                                                             | string       | 804                                                                                                                                   |
| senderRegion            | Область відправника                                                                                                | string       | Kyiv Region                                                                                                                           |
| senderCity              | Місто відправника                                                                                                  | string       | Kyiv                                                                                                                                  |
| senderStreet            | Вулиця відправника                                                                                                 | string       | Test Street                                                                                                                           |
| senderAdditionalAddress | Додаткові дані адреси відправника (поверх, номер будинку, квартира)                                                | string       | Building 1, Apartment 10                                                                                                              |
| senderItn               | ІПН відправника                                                                                                    | string       | 0000000000                                                                                                                            |
| senderPassport          | Паспортні дані відправника                                                                                         | string       | TEST123456                                                                                                                            |
| senderIp                | IPv4 або IPv6 адреса відправника                                                                                   | string       | 192.0.2.1                                                                                                                             |
| senderPhone             | Номер телефону відправника                                                                                         | string       | +380501234567                                                                                                                         |
| senderBirthday          | Дата народження відправника                                                                                        | string       | 1990-01-01                                                                                                                            |
| senderGender            | Гендер відправника                                                                                                 | string       | Female                                                                                                                                |
| senderZipCode           | Поштовий індекс відправника                                                                                        | string       | 01001                                                                                                                                 |
| senderPaymentSystem     | Назва платіжної системи картки відправника                                                                         | string       | VISA                                                                                                                                  |
| senderCardNumberMask    | Маскований номер картки відправника                                                                                | string       | 411111\*\*\*\*\*\*1111                                                                                                                |
| senderBankCode          | Код/назва банку-емітента картки відправника                                                                        | string       | TEST\_BANK                                                                                                                            |
| receiptUrl              | URL квитанції за операцією                                                                                         | string       | [https://test.merchant.com/receipt/TEST\_OPERATION\_001](https://test.merchant.com/receipt/TEST_OPERATION_001?utm_source=chatgpt.com) |

#### Приклад тіла запиту&#x20;

```json
{
	"id": "16849296265235MUp5dm2pxD"
}
```

#### Приклад тіла відповіді для PURCHASE

```json
{
   "type":"PURCHASE",
   "rrn":"123456789012",
   "purpose":"Test payment for Order №123",
   "coinAmount":4530,
   "merchantId":"TEST_MERCHANT_001",
   "operationId":"TEST_OPERATION_001",
   "ecomOperationId":"TEST_ECOM_OPERATION_001",
   "merchantName":"Test Merchant",
   "approvalCode":"123456",
   "status":"SUCCESS",
   "transactionType":35,
   "transactionCurrency":"980",
   "creationDateTime":"2026.11.11 17:03:50.127",
   "modificationDateTime":"2026.11.11 17:05:02.672",
   "transactionResponseInfo":{
      "actionCode":"0",
      "responseCode":"00",
      "description":"approved"
   },
   "bankCode":"TEST_BANK",
   "paymentSystem":"VISA",
   "paymentServiceType":"CARD",
   "notificationEncryption":false,
   "notificationSignature":true,
   "hppOrderId":"TEST_HPP_ORDER_001",
   "processingTerminalId":"TEST_TERMINAL_001",
   "processingMerchantId":"TEST_PROCESSING_MERCHANT_001",
   "creatorSystem":"HPP",
   "sourceAmount":100,
   "sourceCurrencyCode":"840",
   "conversionRate":"45.3000",
   "cardNumberMask":"411111******1111",
   "desiredThreeDSMode":"SHOULD",
   "threeDSMode":"MUST",
   "acsTransId":"TEST_ACS_TRANS_ID_001",
   "dsTransId":"TEST_DS_TRANS_ID_001",
   "eci":"05",
   "statusThreeDs":"Y",
   "threeDSServerTransId":"TEST_3DS_SERVER_TRANS_ID_001",
   "senderCustomerId":"TEST_CUSTOMER_001",
   "senderFirstName":"Test",
   "senderLastName":"User",
   "senderMiddleName":"Testovich",
   "senderEmail":"test@example.com",
   "senderCountry":"804",
   "senderRegion":"Kyiv Region",
   "senderCity":"Kyiv",
   "senderStreet":"Test Street",
   "senderAdditionalAddress":"Building 1, Apartment 10",
   "senderItn":"0000000000",
   "senderPassport":"TEST123456",
   "senderIp":"192.0.2.1",
   "senderPhone":"+380501234567",
   "senderBirthday":"1990-01-01",
   "senderGender":"Female",
   "senderZipCode":"01001",
   "senderPaymentSystem":"VISA",
   "senderCardNumberMask":"411111******1111",
   "senderBankCode":"TEST_BANK",
   "receiptUrl":"https://test.merchant.com/receipt/TEST_OPERATION_001"
}
```

#### Приклад тіла відповіді для А2С

```json
{
    "type": "ACCOUNT_2_CARD",
    "rrn": "314412161279",
    "purpose": "test",
    "comment": "за товар",
    "merchantId": "467c8a10-c705-11ed-afa1-0242ac120002",
    "operationId": "16849296265235MUp5dm2pxD",
    "merchantName": null,
    "approvalCode": null,
    "status": "SUCCESS",
    "transactionType": 46,
    "merchantRequestId": "65d5dd3e-a07e-424f-adde-b608205a82ee",
    "transactionCurrency": "980",
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo":{
      "actionCode":"0",
      "responseCode":"00",
      "description":"approved"
   },
    "senderCity": "Kyiv",
    "senderStreet": "L.Ukrainki01",
    "senderCountry": "840",
    "senderAccount": "UA12305299260022119999",
    "senderLastName": "Petrenko",
    "senderFirstName": "Petro",
    "recipientCity": "Kyiv",
    "recipientStreet": "T. Shevchenka, 11",
    "recipientCountry": "840",
    "recipientLastName": "TestLastName",
    "recipientFirstName": "TestFirstname",
    "recipientCardNumberMask": "537541******7190",
    "coinAmount": 120,
    "merchantCommission": null
}

```

#### Приклад тіла відповіді для Refund

```json
{
    "type": "REFUND",
    "rrn": null,
    "purpose": null,
    "comment": null,
    "coinAmount": 100,
    "merchantId": "467c8a10-c705-11ed-afa1-0242ac120002",
    "operationId": "1698132724973lPTqsaiELlg",
    "merchantName": null,
    "approvalCode": null,
    "status": "SUCCESS",
    "transactionType": 76,
    "merchantRequestId": "269498bf-c581-48f5-8294-b3b504cb0642",
    "transactionCurrency": "980",
    "merchantCommission": null,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": null
    },
    "rrnOriginal": null,
    "originalOperationId": "1698060925854-0zLY-_uCnL",
    "originalCoinAmount": 0,
    "cardNumberMask": "516874••••••4924"
}

```
