---
description: POST {{url}}/ecom/execute_request/merchant/ecom_balance/v1/get
---

# Отримання балансу

#### **Вихідні параметри:**

<table data-full-width="true"><thead><tr><th>Параметр</th><th width="234">Опис</th><th width="160.50000000000003">Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantId</td><td>Id мерчанта</td><td>string</td><td>235d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>balanceAmount</td><td>Сума на балансі</td><td>string</td><td>47</td></tr><tr><td>balanceLimit</td><td>Сума овердрафт ліміту для мерчанта</td><td>string</td><td>0</td></tr><tr><td>totalAmount</td><td>Загальна сума</td><td>string</td><td>47</td></tr></tbody></table>

#### Приклад тіла запиту

```json
{ }
```

#### Приклад тіла відповіді&#x20;

```json
{
    "merchantId": "235d9304-0368-11ed-b939-0242ac120002",
    "balanceAmount": 47,
    "balanceLimit": 0,
    "totalAmount": 47
}
```
