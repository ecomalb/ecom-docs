---
description: '{{url}}/ecom/execute_request/payments/v3/refund'
---

# REFUND

Повернення застосовується у разі необхідності повернути кошти клієнту по успішно здійсненій операції Платежу. В результаті даної операції кошти будуть повернені на ту карту, з якої проводився розрахунок по оригінальній операції.

#### **Вхідні параметри:**

<table data-full-width="true"><thead><tr><th>Параметр</th><th>Опис</th><th width="154">Формат даних</th><th width="149">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string (36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>operationId</td><td>ідентифікатор платіжної операції згенерований КБ по якій проводиться повернення</td><td>string</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>coinAmount</td><td>сума повернення в копійках</td><td>string</td><td>Так</td><td>2500</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00 </td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>НІ</td><td>merchant Comment id 1258728c1</td></tr></tbody></table>

#### **Вихідні параметри**

| Параметр                | Опис                                                     | Формат даних | Приклад                                                                                                      |
| ----------------------- | -------------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------ |
| type                    | тип транзакції                                           | string       | REFUND                                                                                                       |
| rrn                     | rrn номер транзакції в МПС                               | string       | 2554256963                                                                                                   |
| purpose                 | призначення платежу                                      | string       | За товар                                                                                                     |
| comment                 | коментар                                                 | string       | тест                                                                                                         |
| coinAmount              | сума платежу                                             | int          | 2000                                                                                                         |
| merchantId              | Id мерчанту                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                         |
| operationId             | Id транзакціі                                            | string       | 1712844596346b9F-WwrWZpq                                                                                     |
| ecomOperationId         | Id транзакціі в системі Ecom                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                         |
| merchantName            | найменування торговця                                    | string       | KB test terminal                                                                                             |
| approvalCode            | код авторизаціі                                          | string       | 39203                                                                                                        |
| status                  | статус транзакціі                                        | string       | <p>SUСCESS<br>FAIL<br>PENDING<br>REQUIRED_3DS<br>DESIRED_THREEDS_MODE_ERROR</p>                              |
| transactionType         | тип транзакції у цифровому значенні                      | string       | 76                                                                                                           |
| merchantRequestId       | Id запиту мерчанта                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                         |
| transactionCurrency     | валюта платежу                                           | string       | 980                                                                                                          |
| merchantCommission      | сума комісії                                             | string       | 2                                                                                                            |
| createDateTime          | дата створення платежу                                   | string       | 2024.09.19 15:29:25.675                                                                                      |
| modificationDateTime    | дата модифікаціі платежу                                 | string       | 2024.09.19 15:29:25.675                                                                                      |
| actionCode              | код відповіді                                            | string       | 0                                                                                                            |
| responseCode            | деталі відповіді                                         | string       | 0                                                                                                            |
| description             | опис відповіді                                           | string       | approved                                                                                                     |
| processingMerchantId    | Id мерчанту в ПЦ                                         | string       | AE100000                                                                                                     |
| processingTerminalId    | Id терміналу в ПЦ                                        | string       | AE100000                                                                                                     |
| bankCode                | назва банку емітента                                     | string       | BANK\_ALLIANCE                                                                                               |
| paymentSystem           | назва мпс емітента                                       | string       | MasterCard                                                                                                   |
| productType             | тип продукту термінала                                   | string       | PURCHASE                                                                                                     |
| notificationUrl         | url, на який відправлено CallBack                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                    |
| paymentServiceType      | тип оплати                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                  |
| notificationEncryption  | ознака криптування данних CallBack                       | string       | <p>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p> |
| originalOperationId     | id під яким створено оригінальну операцію                | string       | 1712843529623cHAHkmt-G5u                                                                                     |
| originalCoinAmount      | Сума оригінального платежу                               | int          | 100                                                                                                          |
| originalEcomOperationId | id в системі Еком під яким створено оригінальну операцію | string       | c25ee1cb-a052-439b-b075-bcb632615b11                                                                         |
| rrnOriginal             | rrn номер оригінальної транзакції в МПС                  | string       | 123456789                                                                                                    |

#### Приклад тіла запиту&#x20;

```json
{
"merchantRequestId":"137d9304-0368-11ed-b939-0242ac120002",
"operationId":"137d9304-0368-11ed-b939-0242ac120002",
"merchantId":"137d9304-0368-11ed-b939-0242ac120002",
"coinAmount":"2500", 
"notificationUrl": "",
"date": "2022-11-11 11:58:41.56+00:00"
}

```

#### Приклад тіла відповіді

```json
{
    "type": "REFUND",
    "rrn": "410213187861",
    "purpose": null,
    "comment": null,
    "coinAmount": 100,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712843529623cHAHkmt-G5u",
    "ecomOperationId": "3af2de3a-035d-44c4-9f63-d3c899687d34",
    "merchantName": null,
    "approvalCode": null,
    "status": "PENDING",
    "transactionType": 76,
    "merchantRequestId": "21f8ab16-3d4e-4ece-a3f5-ecb406c394ff",
    "transactionCurrency": "980",
    "merchantCommission": null,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": "Операція успішна"
    },
    "bankCode": null,
    "paymentSystem": null,
    "productType": "PURCHASE",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": null,
    "notificationEncryption": false,
    "rrnOriginal": "410213187861",
    "originalOperationId": "1712843529623cHAHkmt-G5u",
    "originalCoinAmount": 100,
    "cardNumberMask": null,
    "originalEcomOperationId": "c25ee1cb-a052-439b-b075-bcb632615b11"
}

```
