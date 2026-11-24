---
description: '{{url}}/ecom/jws/payments/preauth/completion_v1'
---

# Запит проведення Completion

#### **Вхідні параметри:**

<table data-full-width="true"><thead><tr><th>Параметр</th><th>Опис</th><th width="154">Формат даних</th><th width="149">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string (36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>originalOperationId</td><td>ідентифікатор операції преавторизаціі.</td><td>string</td><td>Так</td><td>17853174998663DNdLakuczP</td></tr><tr><td>coinAmount</td><td>Сума списання під час підтвердження PREAUTH, у копійках.</td><td>string</td><td>Так</td><td>2500</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (255)</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255)</p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>customerData</td><td>Об'єкт даних платника</td><td>object</td><td>Ні (весь об'єкт необов'язковий)</td><td>—</td></tr><tr><td>customerData.senderCustomerId</td><td>ID клієнта відправника</td><td>string (255)</td><td>Ні</td><td>1258728c1</td></tr><tr><td>customerData.senderFirstName</td><td>Ім'я відправника</td><td>string (30)</td><td>Ні</td><td>Іван</td></tr><tr><td>customerData.senderLastName</td><td>Прізвище відправника</td><td>string (30)</td><td>Ні</td><td>Іваненко</td></tr><tr><td>customerData.senderMiddleName</td><td>По-батькові відправника</td><td>string (30)</td><td>Ні</td><td>Іванович</td></tr><tr><td>customerData.senderEmail</td><td>Пошта відправника</td><td>string (256)</td><td>Ні</td><td>mail@gmail.com</td></tr><tr><td>customerData.senderCountry</td><td>Країна відправника (ISO 3166)</td><td>string (3)</td><td>Ні</td><td>804</td></tr><tr><td>customerData.senderRegion</td><td>Область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>customerData.senderCity</td><td>Місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>customerData.senderStreet</td><td>Вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>customerData.senderAdditionalAddress</td><td>Додаткові дані адреси</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>customerData.senderItn</td><td>ІПН відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>customerData.senderPassport</td><td>Паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>customerData.senderIp</td><td>IP-адреса відправника</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>customerData.senderPhone</td><td>Телефон відправника</td><td>string (50)</td><td>Ні</td><td>380630000000</td></tr><tr><td>customerData.senderBirthday</td><td>День народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>customerData.senderGender</td><td>Стать відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>customerData.senderZipCode</td><td>Поштовий індекс</td><td>string (50)</td><td>Ні</td><td>49000</td></tr></tbody></table>

#### **Вихідні параметри**

| Параметр                             | Опис                                                        | Формат даних | Приклад                                                                                                      |
| ------------------------------------ | ----------------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------ |
| type                                 | тип транзакції                                              | string       | COMPLETION                                                                                                   |
| rrn                                  | rrn номер транзакції в МПС                                  | string       | 2554256963                                                                                                   |
| purpose                              | призначення платежу                                         | string       | За товар                                                                                                     |
| comment                              | коментар                                                    | string       | тест                                                                                                         |
| coinAmount                           | сума платежу                                                | int          | 2000                                                                                                         |
| merchantId                           | Id мерчанту                                                 | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                         |
| operationId                          | Id транзакціі                                               | string       | 1712844596346b9F-WwrWZpq                                                                                     |
| ecomOperationId                      | Id транзакціі в системі Ecom                                | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                         |
| merchantName                         | найменування торговця                                       | string       | KB test terminal                                                                                             |
| approvalCode                         | код авторизаціі                                             | string       | 39203                                                                                                        |
| status                               | статус транзакціі                                           | string       | <p>SUСCESS<br>FAIL<br>PENDING</p>                                                                            |
| transactionType                      | тип транзакції у цифровому значенні                         | number       | 196                                                                                                          |
| merchantRequestId                    | Id запиту мерчанта                                          | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                         |
| transactionCurrency                  | валюта платежу                                              | string       | 980                                                                                                          |
| creationDateTime                     | дата створення платежу                                      | string       | 2024.09.19 15:29:25.675                                                                                      |
| modificationDateTime                 | дата модифікаціі платежу                                    | string       | 2024.09.19 15:29:25.675                                                                                      |
| transactionResponseInfo              | Об’єкт із кодами та описом результату операції.             | object       | Див. вкладені поля нижче.                                                                                    |
| transactionResponseInfo.actionCode   | код відповіді                                               | string       | 0                                                                                                            |
| transactionResponseInfo.responseCode | деталі відповіді                                            | string       | 0                                                                                                            |
| transactionResponseInfo.description  | опис відповіді                                              | string       | approved                                                                                                     |
| processingMerchantId                 | Id мерчанту в ПЦ                                            | string       | AE100000                                                                                                     |
| processingTerminalId                 | Id терміналу в ПЦ                                           | string       | AE100000                                                                                                     |
| bankCode                             | назва банку емітента                                        | string       | BANK\_ALLIANCE                                                                                               |
| paymentSystem                        | назва мпс емітента                                          | string       | MasterCard                                                                                                   |
| productType                          | тип продукту термінала                                      | string       | PURCHASE                                                                                                     |
| notificationUrl                      | url, на який відправлено CallBack                           | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                    |
| paymentServiceType                   | тип оплати                                                  | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                  |
| notificationEncryption               | ознака криптування данних CallBack                          | string       | <p>true/false<br>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p> |
| preauthOperationId                   | id преавторизаціі                                           | string       | 1712843529623cHAHkmt-G5u                                                                                     |
| preauthCoinAmount                    | Сума преавторизаціі                                         | int          | 100                                                                                                          |
| preauthEcomOperationId               | id в системі Еком під яким створено операцію преавторизацію | string       | c25ee1cb-a052-439b-b075-bcb632615b11                                                                         |
| rrnPreauth                           | rrn номер преавторизаціі в МПС                              | string       | 123456789                                                                                                    |
| merchantCommission                   | сума комісії                                                | string       | 2                                                                                                            |
| senderCustomerId                     | ID клієнта відправника                                      | string       | 1258728c1                                                                                                    |
| senderFirstName                      | Ім'я відправника                                            | string       | Іван                                                                                                         |
| senderLastName                       | Прізвище відправника                                        | string       | Іваненко                                                                                                     |
| senderMiddleName                     | По-батькові відправника                                     | string       | Іванович                                                                                                     |
| senderEmail                          | Пошта відправника                                           | string       | mail@gmail.com                                                                                               |
| senderCountry                        | Країна відправника                                          | string       | 804                                                                                                          |
| senderRegion                         | Область відправника                                         | string       | Київська                                                                                                     |
| senderCity                           | Місто відправника                                           | string       | Київ                                                                                                         |
| senderStreet                         | Вулиця відправника                                          | string       | Січових стрільців                                                                                            |
| senderAdditionalAddress              | Додаткові дані адреси                                       | string       | 23                                                                                                           |
| senderItn                            | ІПН відправника                                             | string       | 123456789                                                                                                    |
| senderPassport                       | Паспорт відправника                                         | string       | АН123456                                                                                                     |
| senderIp                             | IP-адреса відправника                                       | string       | 123.12.12.12                                                                                                 |
| senderPhone                          | Телефон відправника                                         | string       | 380630000000                                                                                                 |
| senderBirthday                       | День народження відправника                                 | string       | 31.12.2000                                                                                                   |
| senderGender                         | Стать відправника                                           | string       | Male/Female                                                                                                  |
| senderZipCode                        | Поштовий індекс відправника                                 | string       | 49000                                                                                                        |
| creatorSystem                        | Система, у якій створено операцію.                          | string       | H2H                                                                                                          |

#### Приклад тіла запиту

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
