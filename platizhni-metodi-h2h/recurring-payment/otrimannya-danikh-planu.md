---
description: POST /ecom/jws/scheduled_payments/plan/get_v1
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
  anchors:
    visible: true
---

# Отримання даних плану

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр** | **Опис** | **Формат даних** | **Обовʼязковість** | **Приклад**                             |
| ------------ | -------- | ---------------- | ------------------ | --------------------------------------- |
| planId       | Id плану | uuid             | так                | `164a8363-a4b8-47c1-884a-dd5c5e42d564`  |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**                      | **Опис**                                                                                                                              | **Формат даних** | **Приклад**                          |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------ |
| merchantId                        | id мерчанта в ecom                                                                                                                    |  uuid(36)        | 137d9304-0368-11ed-b939-0242ac120002 |
| plan                              | обʼєкт з даними плану                                                                                                                 | object           |                                      |
| plan.name                         | назва підписки, що відображається мерчанту та/або користувачу                                                                         | string           | Premium subscription                 |
| plan.description                  | опис підписки                                                                                                                         | string           | Monthly premium access               |
| plan.status                       | <p>поточний статус підписки<br><a href="https://alliancedigital.atlassian.net/wiki/spaces/ECOMM1/pages/986939430">plan_status</a></p> | string           | ACTIVE                               |
| plan.categorySubcategoryIndicator | категрія та саб ктегорія                                                                                                              | enum             | C103                                 |
| plan.createdAt                    | дата та час створення плану                                                                                                           | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00         |
| plan.updatedAt                    | дата та час останнього оновлення плану                                                                                                | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00         |
| plan.deletedAt                    | дата та час видалення плану                                                                                                           | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00         |
| versions                          | обʼєкт з версіями                                                                                                                     | object           |                                      |
| versions.versionId                | номер версії плану                                                                                                                    | int              | 1                                    |
| versions.appliesDateTimeFrom      | зміна застосовується з                                                                                                                | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00         |
| versions.appliesDateTimeTo        | застосовується до..                                                                                                                   | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00         |
| versions.rules                    | набір правил білінгу для версії                                                                                                       | object           |                                      |
| versions.rules.createdAt          | дата та час створення версіі                                                                                                          | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00         |
| versions.rules.paymentNumberFrom  | початковий номер платіжа з якого почина діяти дане правило                                                                            | int              | 1                                    |
| versions.rules.paymentNumberTo    | останній номер платіжа для якого ще працює правило                                                                                    | int              | 1                                    |
| versions.rules.intervalValue      | значення через скільки буде наступний платіж                                                                                          | int              | 12                                   |
| versions.rules.intervalUnit       | значення через скільки буде наступний платіж                                                                                          | string           | DAY, WEEK, MONTH                     |
| versions.rules.coinAmount         | сума списання за один білінг-інтервал                                                                                                 | long             | 2000                                 |
| versions.rules.currency           | валюта підписки                                                                                                                       | string           | 980                                  |
| subscriptionStatistics            | обʼєкт                                                                                                                                | object           |                                      |
| subscriptionStatistics.pending    | кількість зі статусом pending                                                                                                         | int              |  4                                   |
| subscriptionStatistics.success    | кількість зі статусом success                                                                                                         | int              | 36                                   |
| subscriptionStatistics.fail       | кількість зі статусом fail                                                                                                            | int              | 5                                    |
| subscriptionStatistics.canceled   | кількість зі статусом canceled                                                                                                        | int              | 7                                    |

#### Приклад запиту <a href="#priklad-zapitu" id="priklad-zapitu"></a>

```json
{ 
 "planId":"164a8363-a4b8-47c1-884a-dd5c5e42d564" 
}
```

#### Приклад відповіді: <a href="#priklad-vidpovidi" id="priklad-vidpovidi"></a>

```json
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "plan": {
        "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
        "name": "",
        "description": "Installment plan123543521",
        "status": "ACTIVE",
        "categorySubcategoryIndicator": "C103",
        "createdAt": "2026-07-09 17:12:00.14+03:00",
        "updatedAt": "2026-07-10 13:36:25.01+03:00"
    },
    "versions": {
        "1": {
            "versionId": 1,
            "appliesDateTimeFrom": "2026-07-09 17:12:00.14+03:00",
            "appliesDateTimeTo": "2026-08-23 12:46:00.52+03:00",
            "rules": {
                "1": {
                    "paymentNumberFrom": 1,
                    "paymentNumberTo": 5,
                    "intervalValue": 1,
                    "intervalUnit": "DAY",
                    "coinAmount": 100,
                    "currency": "980"
                },
                "2": {
                    "paymentNumberFrom": 6,
                    "paymentNumberTo": 10,
                    "intervalValue": 1,
                    "intervalUnit": "MONTH",
                    "coinAmount": 8000,
                    "currency": "980"
                }
            }
        },
        "2": {
            "versionId": 2,
            "appliesDateTimeFrom": "2026-08-23 12:46:00.52+03:00",
            "appliesDateTimeTo": "2026-08-24 12:46:00.52+03:00",
            "rules": {
                "1": {
                    "paymentNumberFrom": 1,
                    "paymentNumberTo": 3,
                    "intervalValue": 1,
                    "intervalUnit": "DAY",
                    "coinAmount": 205,
                    "currency": "980"
                },
                "2": {
                    "paymentNumberFrom": 4,
                    "paymentNumberTo": 6,
                    "intervalValue": 1,
                    "intervalUnit": "MONTH",
                    "coinAmount": 8000,
                    "currency": "980"
                }
            }
        },
        "3": {
            "versionId": 3,
            "appliesDateTimeFrom": "2026-08-24 12:46:00.52+03:00",
            "appliesDateTimeTo": "2026-10-18 13:46:00.52+03:00",
            "rules": {
                "1": {
                    "paymentNumberFrom": 1,
                    "paymentNumberTo": 3,
                    "intervalValue": 1,
                    "intervalUnit": "DAY",
                    "coinAmount": 205,
                    "currency": "980"
                },
                "2": {
                    "paymentNumberFrom": 4,
                    "paymentNumberTo": 6,
                    "intervalValue": 1,
                    "intervalUnit": "MONTH",
                    "coinAmount": 8000,
                    "currency": "980"
                }
            }
        },
        "4": {
            "versionId": 4,
            "appliesDateTimeFrom": "2026-10-18 13:46:00.52+03:00",
            "appliesDateTimeTo": "2026-12-18 12:46:00.52+02:00",
            "rules": {
                "1": {
                    "paymentNumberFrom": 1,
                    "paymentNumberTo": 3,
                    "intervalValue": 1,
                    "intervalUnit": "DAY",
                    "coinAmount": 205,
                    "currency": "980"
                },
                "2": {
                    "paymentNumberFrom": 4,
                    "paymentNumberTo": 6,
                    "intervalValue": 1,
                    "intervalUnit": "MONTH",
                    "coinAmount": 8000,
                    "currency": "980"
                }
            }
        }
    },
  "subscriptionStatistics": {
    "pending": 1,
    "success": 0,
    "fail": 0,
    "canceled": 0
  }
}
```
