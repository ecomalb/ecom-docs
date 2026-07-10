---
description: POST /ecom/jws/scheduled_payments/payments/scheduled/search_v1
---

# Отримання даних по платежам

Отримання списку запланованих/виконаних рекурентних платежів із можливістю фільтрації по плану, статусу та датах створення.

#### Вхідні параметри&#x20;

| **Параметр**     | **Опис**                                                                                                                                                             | **Формат даних** | **Приклад**                          | **Обовʼязковість** |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ | ------------------ |
| merchantId       | id мерчанта                                                                                                                                                          |  uuid(36)        | 137d9304-0368-11ed-b939-0242ac120002 | так                |
| **filters**      | Список фільтрів.                                                                                                                                                     | array            |                                      |                    |
| filters.operator | <p></p><p>Оператор для фільтрування.</p><ul><li>IN </li><li>GTE </li><li>LTE </li><li>EQUALS  </li><li>LIKE – фільтр LIKE передається без параметра field.</li></ul> | string           | `EQUALS`                             |                    |
| filters.value    | Значення для параметра, назва параметра вказується в `field`                                                                                                         | string           | `FAIL`                               |                    |
| filters.field    | Параметр, для якого застосовується фільтр                                                                                                                            | string           | `state`                              |                    |

#### Параметри, які доступні для фільтраціі <a href="#parametri-yaki-dostupni-dlya-filracii-inlinecard" id="parametri-yaki-dostupni-dlya-filracii-inlinecard"></a>

| **Параметр**               | **Опис**                | **Формат даних** | **Обовʼязковість** | **Приклад**                          |
| -------------------------- | ----------------------- | ---------------- | ------------------ | ------------------------------------ |
| id                         | Id платежу              | uuid             |                    |                                      |
| orderId                    | Id підписки             | string           | ні                 |  1783610230256tRdmRqfsGJj            |
| planId                     | id плану                | string           | ні                 | a9562240-10ca-42d7-8d90-bbd1ace3dc5a |
| status                     | статус платежу          | string           | ні                 | WAITING                              |
| <p>executionAt</p><p> </p> | дата проведення платежу | TIMESTAMPZ       | ні                 | 2024.09.19 15:29:25.675              |

#### Вихідні параметри: <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Приклад</strong></td></tr><tr><td>currentPage</td><td> </td><td> </td><td> </td></tr><tr><td>payments</td><td>обʼєкт операціі</td><td>object</td><td> </td></tr><tr><td>id</td><td>Id операціі </td><td>uuid</td><td>13c06c89-936c-4d7c-8164-0baabc35cb06</td></tr><tr><td>planId</td><td>Id плану</td><td>string</td><td>a9562240-10ca-42d7-8d90-bbd1ace3dc5a</td></tr><tr><td>planName</td><td>Назва підписки</td><td>string</td><td>Premium subscription</td></tr><tr><td>versionId</td><td>Id версіі</td><td>int</td><td> 4</td></tr><tr><td>versionStatus</td><td>статус версіі</td><td>string</td><td> <code>ACTIVE</code></td></tr><tr><td>paymentNumber</td><td>номер платежу по плану, номер платежу в рамках ордеру</td><td>int</td><td> 3</td></tr><tr><td>status</td><td>статус платежу</td><td>string</td><td><code>WAITING</code></td></tr><tr><td>orderId</td><td>Id підписки</td><td>string</td><td>1783610230256tRdmRqfsGJj</td></tr><tr><td>executionAt</td><td>дата виконання проведення</td><td>TIMESTAMPZ</td><td>2026-08-12 18:17:49.89+03:00</td></tr><tr><td>retryExecutionAt</td><td>наступна дата ретраю</td><td>TIMESTAMPZ</td><td>2026-08-12 18:17:49.89+03:00</td></tr><tr><td>retryNumber</td><td>кількість ретраїв</td><td>int</td><td> 2</td></tr><tr><td>coinAmount</td><td>сума платежу</td><td>long</td><td> 2000</td></tr><tr><td>currency</td><td>валюта платежу</td><td>string</td><td> 980</td></tr><tr><td>recurringTransactionType</td><td>Індикатор транзакції:</td><td>string</td><td><ul><li><strong>O</strong> – Перша транзакція</li><li><strong>C</strong> – Наступна CIT-транзакція</li><li><strong>M</strong> – Наступна MIT-транзакція</li></ul></td></tr><tr><td>categorySubcategoryIndicator</td><td>категорія підписки</td><td>string</td><td>M103</td></tr></tbody></table>

#### Приклад запиту&#x20;

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "filters":[
      {
         "operator":"EQUALS",
         "value":"{{planId}}",
         "field":"planId"
      }
   ]
}
```

#### Приклад відповіді

```json
{
  "currentPage": 0,
  "payments": [
    {
      "id": "f9c67467-aade-4af6-9c11-25677dc654b1",
      "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
      "planName": "Тест 2",
      "versionId": 1,
      "versionStatus": "ACTIVE",
      "paymentNumber": 4,
      "status": "WAITING",
      "coinAmount": 100,
      "currency": "980",
      "executionAt": "2026-07-12 18:17:49.89+03:00",
      "recurringTransactionType": "M",
      "categorySubcategoryIndicator": "M102",
      "orderId": "1783610230256tRdmRqfsGJj"
    },
    {
      "id": "f43432e4-6f4f-4ed9-b433-97993c34b365",
      "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
      "planName": "тест 2",
      "versionId": 1,
      "versionStatus": "ACTIVE",
      "paymentNumber": 3,
      "status": "WAITING",
      "coinAmount": 100,
      "currency": "980",
      "executionAt": "2026-07-11 18:17:49.89+03:00",
      "recurringTransactionType": "M",
      "categorySubcategoryIndicator": "M102",
      "orderId": "1783610230256tRdmRqfsGJj"
    },
    {
      "id": "bac1571f-8200-4b32-9736-c45aa6eb3afc",
      "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
      "planName": "тест 2",
      "versionId": 1,
      "versionStatus": "ACTIVE",
      "paymentNumber": 3,
      "status": "WAITING",
      "coinAmount": 100,
      "currency": "980",
      "executionAt": "2026-07-11 18:12:55.74+03:00",
      "recurringTransactionType": "M",
      "categorySubcategoryIndicator": "M102",
      "orderId": "1783609541721181tI5zJ3ad"
    },
    {
      "id": "ef8a7b40-e361-474c-a162-87c217c652cc",
      "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
      "planName": "тест 2",
      "versionId": 1,
      "versionStatus": "ACTIVE",
      "paymentNumber": 3,
      "status": "WAITING",
      "coinAmount": 100,
      "currency": "980",
      "executionAt": "2026-07-11 18:01:06.89+03:00",
      "recurringTransactionType": "M",
      "categorySubcategoryIndicator": "M102",
      "orderId": "1783608520205P81ch623POH"
    },
    {
      "id": "1ff757b0-aa91-4cc2-a8b0-f20609d40b04",
      "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
      "planName": "тест 2",
      "versionId": 1,
      "versionStatus": "ACTIVE",
      "paymentNumber": 2,
      "status": "WAITING",
      "coinAmount": 100,
      "currency": "980",
      "executionAt": "2026-07-10 18:17:49.89+03:00",
      "recurringTransactionType": "M",
      "categorySubcategoryIndicator": "M102",
      "orderId": "1783610230256tRdmRqfsGJj"
    }
  ]
}
```
