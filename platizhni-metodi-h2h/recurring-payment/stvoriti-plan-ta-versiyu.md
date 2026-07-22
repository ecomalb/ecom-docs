---
description: POST {{url}}/ecom/jws/scheduled_payments/plan/create_v1
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Створити план та версію

**План** — це «шаблон» вашої підписки. Наприклад, «Місячна підписка на преміум-сервіс» або «Щотижнева оплата за обслуговування»

**Версія** — це конкретні умови списання: скільки, як часто, і протягом якого періоду.

**Правила:**

* ✅ Активна версія може бути **тільки одна** у кожний момент часу
* ❌ Суму та інтервал **не можна змінити** після створення — потрібна нова версія
* ✅ Дати дії можна коригувати

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th width="97.159912109375"></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Обовʼязковість</strong></td><td><strong>Приклад</strong></td></tr><tr><td>merchantId</td><td>id мерчанта в ecom</td><td> uuid(36)</td><td>так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>name</td><td>Назва підписки</td><td>string (150)</td><td>так</td><td>Premium subscription</td></tr><tr><td>categorySubcategoryIndicator</td><td>Категрія та саб ктегорія</td><td>enum</td><td>так</td><td>C103</td></tr><tr><td>description</td><td>Додатковий опис підписки</td><td>string (255)</td><td>ні</td><td>Monthly premium access</td></tr><tr><td>rules</td><td>Масив з правилами</td><td>array</td><td>так</td><td> </td></tr><tr><td>rules.paymentNumberFrom</td><td>Початковий номер платіжа з якого почина діяти дане правило</td><td>int</td><td>так</td><td>1</td></tr><tr><td>rules.paymentNumberTo</td><td>Останній номер платіжа для якого ще працює правило</td><td>int</td><td>так</td><td>1</td></tr><tr><td>rules.intervalValue</td><td>Значення через скільки буде наступний платіж</td><td>int</td><td>так</td><td>14</td></tr><tr><td>rules.intervalUnit</td><td>Значення через скільки буде наступний платіж</td><td>string</td><td>так</td><td>DAY, WEEK, MONTH</td></tr><tr><td>rules.coinAmount</td><td>Сума списання за один білінг-інтервал</td><td>long</td><td>так</td><td>2000</td></tr><tr><td>rules.currency</td><td>Валюта підписки</td><td>string</td><td>так</td><td>980</td></tr></tbody></table>

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**            | **Опис**                                                   | **Формат даних** | **Приклад**                  |
| ----------------------- | ---------------------------------------------------------- | ---------------- | ---------------------------- |
| planId                  | Унікальний ідентифікатор створеної підписки                | string           |                              |
| versionId               | Id версіі                                                  | int              | 1                            |
| merchantId              | Ідентифікатор мерчанта                                     | uuid             |                              |
| name                    | Назва підписки                                             | string           | Premium subscription         |
| description             | Опис підписки                                              | string           | Monthly premium access       |
| status                  | <p>Поточний статус підписки<br></p>                        | string           | ACTIVE                       |
| rules                   | масив з правилами                                          | array            |                              |
| rules.paymentNumberFrom | початковий номер платіжа з якого почина діяти дане правило | int              | 1                            |
| rules.paymentNumberTo   | останній номер платіжа для якого ще працює правило         | int              | 1                            |
| rules.intervalValue     | значення через скільки буде наступний платіж               | int              | 14                           |
| rules.intervalUnit      | значення через скільки буде наступний платіж               | string           | DAY, WEEK, MONTH             |
| rules.coinAmount        | Сума списання за один білінг-інтервал                      | long             | 2000                         |
| rules.currency          | Валюта підписки                                            | string           | 980                          |
| appliesDateTimeFrom     | зміна застосовується з                                     | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |
| appliesDateTimeTo       | зміна застосовується до                                    | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |
| createdAt               | Дата та час створення плану                                | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |
| updatedAt               | Дата та час останнього оновлення плану                     | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |

#### Приклад запиту : <a href="#priklad-zapitu" id="priklad-zapitu"></a>

```json
{
   "merchantId":"{{merchantId}}",
   "name":"Premium subscription",
   "categorySubcategoryIndicator":"C103",
   "description":"Monthly premium access",
   "appliesDateTimeFrom":"2026-07-13 13:04:36.467 +0200",
   "appliesDateTimeTo":"2026-07-20 13:04:36.467 +0200",
   "rules":[
      {
         "paymentNumberFrom":1,
         "paymentNumberTo":5,
         "intervalValue":1,
         "intervalUnit":"DAY",
         "coinAmount":100,
         "currency":"980"
      },
      {
         "paymentNumberFrom":6,
         "paymentNumberTo":10,
         "intervalValue":1,
         "intervalUnit":"MONTH",
         "coinAmount":8000,
         "currency":"980"
      }
   ]
}
```

#### Приклад відповіді: <a href="#priklad-vidpovidi" id="priklad-vidpovidi"></a>

```json
{
    "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
    "versionId": 1,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "name": "Premium subscription",
    "description": "Monthly premium access",
    "status": "ACTIVE",
    "rules": [
        {
            "paymentNumberFrom": 1,
            "paymentNumberTo": 5,
            "intervalValue": 1,
            "intervalUnit": "DAY",
            "coinAmount": 100,
            "currency": "980"
        },
        {
            "paymentNumberFrom": 6,
            "paymentNumberTo": 10,
            "intervalValue": 1,
            "intervalUnit": "MONTH",
            "coinAmount": 8000,
            "currency": "980"
        }
    ],
    "appliesDateTimeFrom": "2026-07-09 17:12:00.14+03:00",
    "createdAt": "2026-07-09 17:12:00.14+03:00",
    "updatedAt": "2026-07-09 17:12:00.14+03:00"
}
```
