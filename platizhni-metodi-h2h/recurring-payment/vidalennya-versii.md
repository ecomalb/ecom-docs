---
description: POST /ecom/jws/scheduled_payments/plan/version/delete_v1
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

# Видалення версіі

Видаляти можна **тільки останню версію** плану.

Версія видалена → всі платежі цієї версії у статусі WAITING - видалені

#### Вхідні параметри:

| **Параметр** | **Опис**  | **Формат даних** | **Обовʼязковість** | **Приклад**                          |
| ------------ | --------- | ---------------- | ------------------ | ------------------------------------ |
| planId       | Id плану  | uuid             | так                | a9562240-10ca-42d7-8d90-bbd1ace3dc5a |
| versionId    | Id версіі | int              | так                | 4                                    |

#### Вихідні параметри:

| **Параметр**  | **Опис**      | **Формат даних** | **Приклад**                          |
| ------------- | ------------- | ---------------- | ------------------------------------ |
| planId        | Id плану      | uuid             | a9562240-10ca-42d7-8d90-bbd1ace3dc5a |
| versionId     | Id версіі     | int              | 4                                    |
| versionStatus | статус версіі | string           | DELETED                              |

#### Приклад запиту&#x20;

```json
{
   "versionId":"4",
   "planId":"{{planId}}"
}
```

#### Приклад відповіді&#x20;

```json
{
    "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
    "versionId": 4,
    "versionStatus": "DELETED"
}
```
