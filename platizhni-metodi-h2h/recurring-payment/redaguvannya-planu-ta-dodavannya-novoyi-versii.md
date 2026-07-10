---
description: POST /ecom/jws/scheduled_payments/plan/update_v1
---

# Редагування плану та додавання нової версіі

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Обовʼязковість</strong></td><td><strong>Приклад</strong></td></tr><tr><td>merchantId</td><td>id мерчанта в ecom</td><td> uuid(36)</td><td>так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>planId</td><td>Унікальний ідентифікатор створеної підписки</td><td>uuid</td><td>так</td><td> </td></tr><tr><td><strong>Параметри плану, які редагуються</strong></td><td></td><td></td><td></td><td></td></tr><tr><td>name</td><td>Назва підписки, що відображається мерчанту та/або користувачу</td><td>string (150)</td><td>ні</td><td>Premium subscription</td></tr><tr><td>description</td><td>Опис підписки</td><td>string (255)</td><td>ні</td><td>Monthly premium access</td></tr><tr><td><strong>Параметри нової версіі</strong></td><td></td><td></td><td></td><td></td></tr><tr><td>rules</td><td>масив з правилами</td><td>array</td><td>так, якщо необхідно додати нову версію</td><td> </td></tr><tr><td>rules.paymentNumberFrom</td><td>початковий номер платіжа з якого почина діяти дане правило</td><td>int</td><td> так</td><td> 1</td></tr><tr><td>rules.paymentNumberTo</td><td>останній номер платіжа для якого ще працює правило</td><td>int</td><td>так </td><td> 1</td></tr><tr><td>rules.intervalValue</td><td>значення через скільки буде наступний платіж</td><td>int</td><td>так </td><td>12</td></tr><tr><td>rules.intervalUnit</td><td>значення через скільки буде наступний платіж</td><td>string</td><td> так</td><td> DAY, WEEK, MONTH</td></tr><tr><td>rules.coinAmount</td><td>Сума списання за один білінг-інтервал</td><td>long</td><td>так </td><td>2000</td></tr><tr><td>rules.currency</td><td>Валюта підписки</td><td>string</td><td> так</td><td>980</td></tr><tr><td>appliesDateTimeFrom</td><td>зміна версії застосовується з</td><td>TIMESTAMPZ</td><td><p>ні, якщо параметр не передається то зміни застосовуються одразу</p><ul><li>appliesDateTimeFrom нової версіі = appliesDateTimeTo старої версіі</li><li>appliesDateTimeFrom нової версіі не може бути більшим за appliesDateTimeTo старої версіі</li><li>якщо appliesDateTimeFrom нової версіі мерньший чим appliesDateTimeTo старої версіі, то відбудеться оновлення appliesDateTimeTo старої версії датою appliesDateTimeFrom новох версіі</li></ul></td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>appliesDateTimeTo</td><td><p>версія застосовується до..</p><p>після цієї дати видаляться всі заплановані платежі по цьому плану</p></td><td>TIMESTAMPZ</td><td>ні, якщо параметр не передається то позамовчуванню на 1 рік вперед</td><td>2026-02-26 11:23:45.12+02:00</td></tr></tbody></table>

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Приклад</strong></td></tr><tr><td>planId</td><td>Унікальний ідентифікатор створеної підписки</td><td>uuid</td><td> </td></tr><tr><td>versionId</td><td>Id версіі</td><td>int</td><td>1</td></tr><tr><td>merchantId</td><td>Ідентифікатор мерчанта</td><td>uuid</td><td> </td></tr><tr><td>name</td><td>Назва підписки</td><td>string</td><td>Premium subscription</td></tr><tr><td>description</td><td>Опис підписки</td><td>string</td><td>Monthly premium access</td></tr><tr><td>rules.paymentNumberFrom</td><td>початковий номер платіжа з якого почина діяти дане правило</td><td>integer</td><td>1</td></tr><tr><td>rules.paymentNumberTo</td><td>останній номер платіжа для якого ще працює правило</td><td>integer</td><td>1</td></tr><tr><td>rules.intervalValue</td><td>Значення білінг-інтервалу</td><td>integer</td><td>1</td></tr><tr><td>rules.intervalUnit</td><td>Одиниця білінг-інтервалу</td><td>string</td><td>MONTH</td></tr><tr><td>rules.coinAmount</td><td>сума</td><td>long</td><td>10</td></tr><tr><td>rules.currency</td><td>валюта</td><td>string</td><td>980</td></tr><tr><td>appliesDateTimeFrom</td><td>зміна застосовується з</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>appliesDateTimeTo</td><td>зміна застосовується до</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>createdAt</td><td>Дата та час створення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>updatedAt</td><td>Дата та час останнього оновлення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr></tbody></table>

#### Приклад запиту редагування параметрів плану

```json
{
   "merchantId":"{{merchantId}}",
   "planId":"{{planId}}",
   "name":"Premium",
   "categorySubcategoryIndicator":"C103",
   "description":"Installment plan123543521"
}
```

#### Приклад відповіді

```json
{
    "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "name": "Premium",
    "description": "Installment plan123543521",
    "createdAt": "2026-07-09 17:12:00.14+03:00",
    "updatedAt": "2026-07-10 11:36:39.35+03:00"
}
```

#### Приклад запиту редагування параметрів плану та додавання нової версіі

```json
{
   "merchantId":"{{merchantId}}",
   "planId":"{{planId}}",
   "name":"Premium",
   "categorySubcategoryIndicator":"C103",
   "description":"Installment plan123543521",
   "appliesDateTimeFrom":"2026-08-23 12:46:00.52+03:00",
   "appliesDateTimeTo":"2026-09-23 12:46:00.52+03:00",
   "rules":[
      {
         "paymentNumberFrom":1,
         "paymentNumberTo":3,
         "intervalValue":1,
         "intervalUnit":"DAY",
         "coinAmount":205,
         "currency":"980"
      },
      {
         "paymentNumberFrom":4,
         "paymentNumberTo":6,
         "intervalValue":1,
         "intervalUnit":"MONTH",
         "coinAmount":8000,
         "currency":"980"
      }
   ]
}
```

#### Приклад відповіді

```json
{
    "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
    "versionId": 2,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "name": "Premium",
    "description": "Installment plan123543521",
    "rules": [
        {
            "paymentNumberFrom": 1,
            "paymentNumberTo": 3,
            "intervalValue": 1,
            "intervalUnit": "DAY",
            "coinAmount": 205,
            "currency": "980"
        },
        {
            "paymentNumberFrom": 4,
            "paymentNumberTo": 6,
            "intervalValue": 1,
            "intervalUnit": "MONTH",
            "coinAmount": 8000,
            "currency": "980"
        }
    ],
    "appliesDateTimeFrom": "2026-08-23 12:46:00.52+03:00",
    "appliesDateTimeTo": "2026-09-23 12:46:00.52+03:00",
    "createdAt": "2026-07-09 17:12:00.14+03:00",
    "updatedAt": "2026-07-10 11:33:08.87+03:00"
}
```

#### Приклад запиту додавання нової версіі

```json
{
   "merchantId":"{{merchantId}}",
   "planId":"{{planId}}",
   "appliesDateTimeFrom":"2026-08-24 12:46:00.52+03:00",
   "appliesDateTimeTo":"2026-09-23 12:46:00.52+03:00",
   "rules":[
      {
         "paymentNumberFrom":1,
         "paymentNumberTo":3,
         "intervalValue":1,
         "intervalUnit":"DAY",
         "coinAmount":205,
         "currency":"980"
      },
      {
         "paymentNumberFrom":4,
         "paymentNumberTo":6,
         "intervalValue":1,
         "intervalUnit":"MONTH",
         "coinAmount":8000,
         "currency":"980"
      }
   ]
}
```

#### Приклад відповіді

```json
{
    "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
    "versionId": 3,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "name": "Premium",
    "description": "Installment plan123543521",
    "rules": [
        {
            "paymentNumberFrom": 1,
            "paymentNumberTo": 3,
            "intervalValue": 1,
            "intervalUnit": "DAY",
            "coinAmount": 205,
            "currency": "980"
        },
        {
            "paymentNumberFrom": 4,
            "paymentNumberTo": 6,
            "intervalValue": 1,
            "intervalUnit": "MONTH",
            "coinAmount": 8000,
            "currency": "980"
        }
    ],
    "appliesDateTimeFrom": "2026-08-24 12:46:00.52+03:00",
    "appliesDateTimeTo": "2026-09-23 12:46:00.52+03:00",
    "createdAt": "2026-07-09 17:12:00.14+03:00",
    "updatedAt": "2026-07-10 11:40:19.68+03:00"
}
```



####
