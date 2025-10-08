---
description: '{{url}}/ecom/execute_request/payments/v1/completion'
---

# Запит проведення Completion

#### **Вхідні параметри:**

<table data-full-width="true"><thead><tr><th>Параметр</th><th>Опис</th><th width="154">Формат даних</th><th width="149">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string (36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>originalOperationId</td><td>ідентифікатор  операції преавторизаціі. </td><td>string</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>coinAmount</td><td>сума повернення в копійках</td><td>string</td><td>Так</td><td>2500</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00 </td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr></tbody></table>

#### **Вихідні параметри**

| Параметр               | Опис                                                        | Формат даних | Приклад                                                                                                      |
| ---------------------- | ----------------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------ |
| type                   | тип транзакції                                              | string       | COMPLETION                                                                                                   |
| rrn                    | rrn номер транзакції в МПС                                  | string       | 2554256963                                                                                                   |
| purpose                | призначення платежу                                         | string       | За товар                                                                                                     |
| comment                | коментар                                                    | string       | тест                                                                                                         |
| coinAmount             | сума платежу                                                | int          | 2000                                                                                                         |
| merchantId             | Id мерчанту                                                 | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                         |
| operationId            | Id транзакціі                                               | string       | 1712844596346b9F-WwrWZpq                                                                                     |
| ecomOperationId        | Id транзакціі в системі Ecom                                | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                         |
| merchantName           | найменування торговця                                       | string       | KB test terminal                                                                                             |
| approvalCode           | код авторизаціі                                             | string       | 39203                                                                                                        |
| status                 | статус транзакціі                                           | string       | <p>SUСCESS<br>FAIL<br>PENDING</p>                                                                            |
| transactionType        | тип транзакції у цифровому значенні                         | string       | 196                                                                                                          |
| merchantRequestId      | Id запиту мерчанта                                          | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                         |
| transactionCurrency    | валюта платежу                                              | string       | 980                                                                                                          |
| createDateTime         | дата створення платежу                                      | string       | 2024.09.19 15:29:25.675                                                                                      |
| modificationDateTime   | дата модифікаціі платежу                                    | string       | 2024.09.19 15:29:25.675                                                                                      |
| actionCode             | код відповіді                                               | string       | 0                                                                                                            |
| responseCode           | деталі відповіді                                            | string       | 0                                                                                                            |
| description            | опис відповіді                                              | string       | approved                                                                                                     |
| processingMerchantId   | Id мерчанту в ПЦ                                            | string       | AE100000                                                                                                     |
| processingTerminalId   | Id терміналу в ПЦ                                           | string       | AE100000                                                                                                     |
| bankCode               | назва банку емітента                                        | string       | BANK\_ALLIANCE                                                                                               |
| paymentSystem          | назва мпс емітента                                          | string       | MasterCard                                                                                                   |
| productType            | тип продукту термінала                                      | string       | PURCHASE                                                                                                     |
| notificationUrl        | url, на який відправлено CallBack                           | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                    |
| paymentServiceType     | тип оплати                                                  | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                  |
| notificationEncryption | ознака криптування данних CallBack                          | string       | <p>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p> |
| preauthOperationId     | id преавторизаціі                                           | string       | 1712843529623cHAHkmt-G5u                                                                                     |
| preauthCoinAmount      | Сума преавторизаціі                                         | int          | 100                                                                                                          |
| preauthEcomOperationId | id в системі Еком під яким створено операцію преавторизацію | string       | c25ee1cb-a052-439b-b075-bcb632615b11                                                                         |
| rrnPreauth             | rrn номер преавторизаціі в МПС                              | string       | 123456789                                                                                                    |

#### Приклад тіла запиту&#x20;

```json
{
"merchantRequestId":"137d9304-0368-11ed-b939-0242ac120002",
"originalOperationId":"17594943825392XRyx8EeK6e",
"merchantId":"137d9304-0368-11ed-b939-0242ac120002",
"coinAmount":"2500", 
"notificationUrl": "",
"date": "2022-11-11 11:58:41.56+00:00"
}

```

#### Приклад тіла відповіді

```json
{
   "type":"COMPLETION",
   "rrn":"527612892256",
   "purpose":"AAAAfasfsfsfAAAAfasAA",
   "comment":"AAAAfasfsfsfAAAAf",
   "coinAmount":100,
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "operationId":"17594944974293A5xR2LzpAQ",
   "ecomOperationId":"9ee1923c-11ce-4ac2-9917-899d499ff3d8",
   "status":"SUCCESS",
   "transactionType":196,
   "merchantRequestId":"e582be0c-aa5c-4991-95a3-ff3d5f53a1c6",
   "transactionCurrency":"980",
   "creationDateTime":"2025.10.03 15:28:17.399",
   "modificationDateTime":"2025.10.03 15:28:17.399",
   "transactionResponseInfo":{
      "actionCode":"0",
      "responseCode":"00",
      "description":"Операція успішна"
   },
   "productType":"PURCHASE",
   "notificationUrl":"https://webhook.site/95b1ded7-b86f-46cb-a771-c70f1f913d57",
   "paymentServiceType":"CARD",
   "notificationEncryption":false,
   "processingTerminalId":"AE001001",
   "processingMerchantId":"AE001001",
   "creatorSystem":"H2H",
   "rrnPreauth":"527612892256",
   "preauthOperationId":"17594943825392XRyx8EeK6e",
   "preauthCoinAmount":100,
   "preauthEcomOperationId":"f1a166ce-a19e-46e2-bd7c-2dc90acd1041"
}
```
