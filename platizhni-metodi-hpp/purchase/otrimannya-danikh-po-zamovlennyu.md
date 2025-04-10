---
description: '{{url}}/ecom/execute_request/hpp/v1/operations'
---

# Отримання даних по замовленню

**Вхідні параметри:**&#x20;

| Параметр   | Опис          | Формат даних | Обов'язковість | Приклад                    |
| ---------- | ------------- | ------------ | -------------- | -------------------------- |
| hppOrderId | Id замовлення | string       | Так            | 1727703854455xVnw\_4\_NpkJ |

**Вихідні параметри:**

| Параметр          | Опис                                                       | Формат даних | Приклад                                                                                                                                                                             |
| ----------------- | ---------------------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| coinAmount        | сума замовлення                                            | long         | 2000                                                                                                                                                                                |
| ecomOrderId       | Id замовлення в системі єком                               | string       | c64a6676-925d-4054-ab21-91face1a05b9                                                                                                                                                |
| statusUrl         | url для редіректу на сторінку статусу                      | string       | [http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp\_id=17285615314160DOA6pa1E8F](http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=17285615314160DOA6pa1E8F) |
| merchantId        | Id мерчанта в системі єком                                 | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                |
| hppOrderId        | Id замовлення                                              | string       | 1727703854455xVnw\_4\_NpkJ                                                                                                                                                          |
| redirectUrl       | посилання на перенаправлення клієнта на платіжку сторінку  | string       | [http://pgi-ecom-release.develop.bankalliance.ua/?hpp\_id=17285615314160DOA6pa1E8F](http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=17285615314160DOA6pa1E8F)               |
| hppPayType        | тип оплати                                                 | enum         | PURCHASE                                                                                                                                                                            |
| notificationUrl   | url, на який буде відправлено CallBack                     | string       | [https://example.com/notify](https://example.com/notify)                                                                                                                            |
| merchantRequestId | унікальний ідентифікатор мерчанта                          | string       | 137d04-0318-11ed-b939-0241ac120104                                                                                                                                                  |
| expiredOrderDate  | дата та час дії замовлення                                 | string       | 2024-10-10 15:13:51.41+03:00                                                                                                                                                        |
| orderStatus       | статус замовлення                                          | string       | PENDING                                                                                                                                                                             |
| paymentMethods    | методи оплати                                              | enum         | CARD                                                                                                                                                                                |
| createDate        | дата та час створення замовлення                           | string       | 2024-10-10 14:58:51.36+03:00                                                                                                                                                        |
| operations        | об'єкт з даними по операціі                                | object       |                                                                                                                                                                                     |

**Приклад запиту**&#x20;

```json
{
    "hppOrderId": "1727703854455xVnw_4_NpkJ"
}
```

**Приклад выдповіді**

```json
{
    "coinAmount": 1000,
    "ecomOrderId": "d49e66c3-eae6-4e0c-bd4c-76ee16f1ea65",
    "statusUrl": "https://pgi-status-ecom.develop.bankalliance.ua/?hpp_id=1729673735773zTmfRBLPRgE",
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "hppOrderId": "1729673735773zTmfRBLPRgE",
    "redirectUrl": "https://pgi-ecom.develop.bankalliance.ua/?hpp_id=1729673735773zTmfRBLPRgE",
    "hppPayType": "PURCHASE",
    "notificationUrl": "https://example.com/notify",
    "merchantRequestId": "417382d3-bc5a-4b7b-a84e-fe5ab5210ec9",
    "expiredOrderDate": "2024-10-23 12:10:35.76+03:00",
    "orderStatus": "SUCCESS",
    "paymentMethods": [
        "CARD"
    ],
    "createDate": "2024-10-23 11:55:36.41+03:00",
    "operations": [
        {
            "type": "PURCHASE",
            "rrn": "429708466097",
            "purpose": "Payment for Order №123456",
            "coinAmount": 1000,
            "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
            "operationId": "1729673813027T0LkeMDxpar",
            "ecomOperationId": "ecb27e94-742f-4fcc-b906-e3f1a209c5b1",
            "merchantName": "KB test terminal",
            "approvalCode": "060628",
            "status": "SUCCESS",
            "transactionType": 35,
            "transactionCurrency": "980",
            "merchantCommission": 0,
            "transactionCreateDateTime": "2024.10.23 11:56",
            "transactionModificationDateTime": "2024.10.23 12:26",
            "creationDateTime": "2024.10.23 11:56:54.483",
            "modificationDateTime": "2024.10.23 12:26:59.131",
            "processingDateTime": "2024.10.23 11:56:54.000",
            "transactionResponseInfo": {
                "actionCode": "0",
                "responseCode": "00",
                "description": "approved"
            },
            "bankCode": "BANK_ALLIANCE",
            "paymentSystem": "MasterCard",
            "paymentServiceType": "CARD",
            "notificationEncryption": false,
            "cardNumberMask": "537593••••••0141",
            "desiredThreeDSMode": "SHOULD",
            "threeDSMode": "MUST",
            "threeDSServerTransId": "c76c9f92-5619-4be6-8521-e15a79bce534",
            "senderCustomerId": "Id ",
            "senderMiddleName": "s",
            "senderEmail": "aaaa@gmail.com",
            "senderCountry": "804",
            "senderRegion": "senderRegion",
            "senderCity": "senderCity",
            "senderStreet": "senderStret",
            "senderAdditionalAddress": "senderAdditionalAddress",
            "senderItn": "5555557777",
            "senderPassport": "passport",
            "senderIp": "255.255.244.255",
            "senderPhone": "380957388888",
            "senderBirthday": "22081989",
            "senderGender": "Female",
            "senderZipCode": "12345",
            "senderBankCode": "BANK_ALLIANCE",
            "senderPaymentSystem": "MasterCard",
            "senderCardNumberMask": "537593••••••0141"
        },
        {
            "type": "REFUND",
            "coinAmount": 10,
            "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
            "ecomOperationId": "4627004b-806c-4ee3-9000-a764cd61981d",
            "status": "FAIL",
            "transactionType": 76,
            "merchantRequestId": "12d76d6e-e753-4216-8fa0-3ed9bb29573b",
            "transactionCurrency": "980",
            "transactionCreateDateTime": "2024.10.24 12:52",
            "transactionModificationDateTime": "2024.10.24 12:52",
            "creationDateTime": "2024.10.24 12:52:41.242",
            "modificationDateTime": "2024.10.24 12:52:41.926",
            "transactionResponseInfo": {},
            "productType": "PURCHASE",
            "errorDetails": "b_security_time_in_request_not_correct",
            "notificationUrl": "https://test.refund.com",
            "notificationEncryption": false,
            "rrnOriginal": "429708466097",
            "originalOperationId": "1729673813027T0LkeMDxpar",
            "originalCoinAmount": 1000,
            "originalEcomOperationId": "ecb27e94-742f-4fcc-b906-e3f1a209c5b1"
        }
    ]
}
```
