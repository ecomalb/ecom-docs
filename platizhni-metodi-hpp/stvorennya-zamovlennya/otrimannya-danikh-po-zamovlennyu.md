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
| coinAmount        | сума замовлення в копійках                                 | long         | 2000                                                                                                                                                                                |
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

**Приклад відповіді**

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

**Вихідні параметри для зовнішнього А2А платежу**

```json
{
    "coinAmount": 100,
    "ecomOrderId": "c6c4fe06-8d26-4c04-ae4a-a97b1bf03676",
    "statusUrl": null,
    "merchantId": "7437c8e2-0ed1-449c-bbb5-cdf27447bf0a",
    "hppOrderId": "1781086744398g0HxVBDHeuY",
    "redirectUrl": "",
    "hppPayType": "A2A",
    "notificationUrl": "https://webhook.site/...",
    "merchantRequestId": "e3a815a9-6084-4047-b9a1-04b9466fdfc2",
    "expiredOrderDate": "2026-06-11 13:19:04.40+03:00",
    "orderStatus": "SUCCESS",
    "paymentMethods": [
        "CARD",
        "APPLE_PAY",
        "GOOGLE_PAY"
    ],
    "createDate": "2026-06-10 13:19:04.34+03:00",
    "operations": [
        {
            "type": "ACCOUNT_2_ACCOUNT",
            "purpose": "Payment for Order №1234565555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555",
            "coinAmount": 1054,
            "merchantId": "7437c8e2-0ed1-449c-bbb5-cdf27447bf0a",
            "operationId": "1781086765946c5WS7nTkPp7",
            "ecomOperationId": "ae54e521-199f-4c9e-b222-f03aed229dc5",
            "merchantName": "ФОП тест",
            "status": "SUCCESS",
            "transactionType": 54,
            "transactionCurrency": "980",
            "creationDateTime": "2026.06.10 13:19:29.126",
            "modificationDateTime": "2026.06.10 13:19:29.126",
            "transactionResponseInfo": {},
            "bankCode": "BANK_ALLIANCE",
            "paymentServiceType": "ACCOUNT",
            "notificationEncryption": false,
            "notificationSignature": false,
            "hppOrderId": "1781086744398g0HxVBDHeuY",
            "creatorSystem": "HPP",
            "merchantComment": "Сплата рахунку від 10.06.2026, за послугою на сайті https://test.ua/, акаунт Id",
            "senderBankCode": "BANK_ALLIANCE",
            "recipientBankCode": "BANK_ALLIANCE",
            "senderCountry": "804",
            "senderCity": "Іaws - Юыяєї'ь .?,/-'*_()",
            "senderStreet": "Мальвіна - Vict'рыя 12345юєїяуь3435",
            "senderAccount": "UA923004650000025702103000001",
            "senderFirstName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderLastName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderGender": "Female",
            "senderCustomerId": "Id",
            "senderMiddleName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderEmail": "aq@",
            "senderRegion": "Київ",
            "senderAdditionalAddress": "aqavbnmwreyuio іюяєео'жуї эыжъвб .,/-_+=`1234098(ff)#![]*^ 1122121222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222",
            "senderItn": "5555557777",
            "senderPassport": "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis,",
            "senderIp": "2001:0db8:3333:4444:5555:6666:7777:8888",
            "senderPhone": "380634387596",
            "senderBirthday": "10.01.2000",
            "senderZipCode": "111111111111111111111111111111111111111111111141",
            "recipientAccount": "UA703001190000026201132371001",
            "recipientFirstName": "Бондар Діана",
            "repeatedPayment": false
        },
        {
            "type": "ACCOUNT_2_ACCOUNT",
            "purpose": "Payment for Order №1234565555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555",
            "coinAmount": 1054,
            "merchantId": "7437c8e2-0ed1-449c-bbb5-cdf27447bf0a",
            "operationId": "17810867949584kKGyq3xM_m",
            "ecomOperationId": "86e6f8ec-3327-4967-9ae7-b7d3f323383d",
            "merchantName": "ФОП тест",
            "status": "SUCCESS",
            "transactionType": 54,
            "transactionCurrency": "980",
            "creationDateTime": "2026.06.10 13:19:57.502",
            "modificationDateTime": "2026.06.10 13:19:57.502",
            "transactionResponseInfo": {},
            "bankCode": "BANK_ALLIANCE",
            "paymentServiceType": "ACCOUNT",
            "notificationEncryption": false,
            "notificationSignature": false,
            "hppOrderId": "1781086744398g0HxVBDHeuY",
            "creatorSystem": "HPP",
            "merchantComment": "Сплата рахунку від 10.06.2026, за послугою на сайті https://test.ua/, акаунт Id",
            "senderBankCode": "BANK_ALLIANCE",
            "recipientBankCode": "BANK_ALLIANCE",
            "senderCountry": "804",
            "senderCity": "Іaws - Юыяєї'ь .?,/-'*_()",
            "senderStreet": "Мальвіна - Vict'рыя 12345юєїяуь3435",
            "senderAccount": "UA923004650000025702103000001",
            "senderFirstName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderLastName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderGender": "Female",
            "senderCustomerId": "Id",
            "senderMiddleName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderEmail": "aq@",
            "senderRegion": "Київ",
            "senderAdditionalAddress": "aqavbnmwreyuio іюяєео'жуї эыжъвб .,/-_+=`1234098(ff)#![]*^ 1122121222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222",
            "senderItn": "5555557777",
            "senderPassport": "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis,",
            "senderIp": "2001:0db8:3333:4444:5555:6666:7777:8888",
            "senderPhone": "380634387596",
            "senderBirthday": "10.01.2000",
            "senderZipCode": "111111111111111111111111111111111111111111111141",
            "recipientAccount": "UA703001190000026201132371001",
            "recipientFirstName": "Бондар Діана",
            "repeatedPayment": true
        },
        {
            "type": "ACCOUNT_2_ACCOUNT",
            "purpose": "Payment for Order №1234565555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555",
            "coinAmount": 1054,
            "merchantId": "7437c8e2-0ed1-449c-bbb5-cdf27447bf0a",
            "operationId": "1781087135534y6rEDmNtaNK",
            "ecomOperationId": "00756075-3334-46a4-9e80-225800138934",
            "merchantName": "ФОП тест",
            "status": "SUCCESS",
            "transactionType": 54,
            "transactionCurrency": "980",
            "creationDateTime": "2026.06.10 13:25:38.844",
            "modificationDateTime": "2026.06.10 13:25:38.844",
            "transactionResponseInfo": {},
            "bankCode": "BANK_ALLIANCE",
            "paymentServiceType": "ACCOUNT",
            "notificationEncryption": false,
            "notificationSignature": false,
            "hppOrderId": "1781086744398g0HxVBDHeuY",
            "creatorSystem": "HPP",
            "merchantComment": "Сплата рахунку від 10.06.2026, за послугою на сайті https://test.ua/, акаунт Id",
            "senderBankCode": "BANK_ALLIANCE",
            "recipientBankCode": "BANK_ALLIANCE",
            "senderCountry": "804",
            "senderCity": "Іaws - Юыяєї'ь .?,/-'*_()",
            "senderStreet": "Мальвіна - Vict'рыя 12345юєїяуь3435",
            "senderAccount": "UA923004650000025702103000001",
            "senderFirstName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderLastName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderGender": "Female",
            "senderCustomerId": "Id",
            "senderMiddleName": "Іваaws - Ювяєї'ь 1234 Куицьйкф",
            "senderEmail": "aq@",
            "senderRegion": "Київ",
            "senderAdditionalAddress": "aqavbnmwreyuio іюяєео'жуї эыжъвб .,/-_+=`1234098(ff)#![]*^ 1122121222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222",
            "senderItn": "5555557777",
            "senderPassport": "Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis,",
            "senderIp": "2001:0db8:3333:4444:5555:6666:7777:8888",
            "senderPhone": "380634387596",
            "senderBirthday": "10.01.2000",
            "senderZipCode": "111111111111111111111111111111111111111111111141",
            "recipientAccount": "UA703001190000026201132371001",
            "recipientFirstName": "Бондар Діана",
            "repeatedPayment": true
        }
    ]
}
```
