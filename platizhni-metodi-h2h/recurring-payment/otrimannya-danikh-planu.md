---
description: POST /ecom/jws/scheduled_payments/plan/get_v1
---

# Отримання даних плану

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр** | **Опис** | **Формат даних** | **Обовʼязковість** | **Приклад**                             |
| ------------ | -------- | ---------------- | ------------------ | --------------------------------------- |
| planId       | Id плану | uuid             | так                | `164a8363-a4b8-47c1-884a-dd5c5e42d564`  |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Приклад</strong></td></tr><tr><td>merchantId</td><td>id мерчанта в ecom</td><td> uuid(36)</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>plan</td><td>обʼєкт з даними плану</td><td>object</td><td> </td></tr><tr><td>plan.name</td><td>Назва підписки, що відображається мерчанту та/або користувачу</td><td>string</td><td>Premium subscription</td></tr><tr><td>plan.description</td><td>Опис підписки</td><td>string</td><td>Monthly premium access</td></tr><tr><td>plan.status</td><td>Поточний статус підписки</td><td>string</td><td>ACTIVE</td></tr><tr><td>plan.categorySubcategoryIndicator</td><td>Категрія та саб ктегорія</td><td>enum</td><td>C103</td></tr><tr><td>plan.createdAt</td><td>Дата та час створення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>plan.updatedAt</td><td>Дата та час останнього оновлення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>plan.deletedAt</td><td>Дата та час видалення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>versions</td><td>обʼєкт з версіями</td><td>object</td><td> </td></tr><tr><td>versions.versionId</td><td>Номер версії плану</td><td>int</td><td>1</td></tr><tr><td>versions.appliesDateTimeFrom</td><td>зміна застосовується з</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>versions.appliesDateTimeTo</td><td>застосовується до..</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>versions.rules</td><td>Набір правил білінгу для версії</td><td>object</td><td> </td></tr><tr><td>versions.rules.createdAt</td><td>Дата та час створення версіі</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>versions.rules.paymentNumberFrom</td><td>початковий номер платіжа з якого почина діяти дане правило</td><td>int</td><td>1</td></tr><tr><td>versions.rules.paymentNumberTo</td><td>останній номер платіжа для якого ще працює правило</td><td>int</td><td>1</td></tr><tr><td>versions.rules.intervalValue</td><td>значення через скільки буде наступний платіж</td><td>int</td><td>12</td></tr><tr><td>versions.rules.intervalUnit</td><td>значення через скільки буде наступний платіж</td><td>string</td><td>DAY, WEEK, MONTH</td></tr><tr><td>versions.rules.coinAmount</td><td>Сума списання за один білінг-інтервал</td><td>long</td><td>2000</td></tr><tr><td>versions.rules.currency</td><td>Валюта підписки</td><td>string</td><td>980</td></tr></tbody></table>

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
        "categorySubcategoryIndicator": "C102",
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
    }
}
```
