---
description: POST /ecom/jws/scheduled_payments/plan/search_v1
---

# Отримання всіх плані

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр**     | **Опис**                                                                                                                                                      | **Формат даних** | **Обовʼязковість** | **Приклад**                          |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------------ | ------------------------------------ |
| merchantId       | id мерчанта в ecom                                                                                                                                            |  uuid(36)        | так                | 137d9304-0368-11ed-b939-0242ac120002 |
| **filters**      |                                                                                                                                                               |                  |                    |                                      |
| filters.operator | <p>Оператор для фільтрування.</p><ul><li>IN </li><li>GTE </li><li>LTE </li><li>EQUALS  </li><li>LIKE – фільтр LIKE передається без параметра field.</li></ul> | string           |  ні                | `EQUALS`                             |
| filters.value    | Значення для параметра, назва параметра вказується в `field`                                                                                                  | string           |  ні                | `FAIL`                               |
| filters.field    | Параметр, для якого застосовується фільтр                                                                                                                     | string           |  ні                | `state`                              |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Приклад</strong></td></tr><tr><td>currentPage</td><td>Поточна сторінка</td><td> </td><td>integer</td></tr><tr><td>plans</td><td>обʼєкт з даними плану</td><td>object</td><td> </td></tr><tr><td>plans.planId</td><td>Id плану</td><td>uuid</td><td> </td></tr><tr><td>plans.name</td><td>Назва підписки, що відображається мерчанту та/або користувачу</td><td>string</td><td>Premium subscription</td></tr><tr><td>plans.description</td><td>Опис підписки</td><td>string</td><td>Monthly premium access</td></tr><tr><td>plans.status</td><td>Поточний статус плану</td><td>string</td><td>ACTIVE</td></tr><tr><td>plans.categorySubcategoryIndicator</td><td>Категрія та саб ктегорія</td><td>enum</td><td>C103</td></tr><tr><td>plans.createdAt</td><td>Дата та час створення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>plans.updatedAt</td><td>Дата та час останнього оновлення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr><tr><td>plans.deletedAt</td><td>Дата та час видалення плану</td><td>TIMESTAMPZ</td><td>2026-02-26 11:23:45.12+02:00</td></tr></tbody></table>

#### Приклад запиту&#x20;

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "filters":[
      {
         "operator":"EQUALS",
         "value":"ACTIVE",
         "field":"status"
      }
   ]
}
```

#### Приклад запиту&#x20;

```json
{
    "currentPage": 0,
    "plans": [
        {
            "planId": "5f058ead-597a-41ca-8efe-e98a87c31ba3",
            "name": "ке",
            "description": "Installment plan for electronics category",
            "status": "ACTIVE",
            "categorySubcategoryIndicator": "C101",
            "createdAt": "2026-03-20 12:58:11.75+02:00",
            "updatedAt": "2026-06-11 17:11:30.06+03:00"
        },
        {
            "planId": "aaf0c861-db75-4062-99f7-ae323983b594",
            "name": "AqaTest Updated recurring plan name 709664",
            "description": "AqaTest Updated recurring plan description 184735",
            "status": "ACTIVE",
            "categorySubcategoryIndicator": "C101",
            "createdAt": "2026-03-22 22:58:49.30+02:00",
            "updatedAt": "2026-07-07 17:38:47.77+03:00"
        }
    ]
}
```
