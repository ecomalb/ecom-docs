---
description: '{{url}}/ecom/execute_request/token/v1/list/by-customer-id'
---

# Запит отримання токену по customerId

**Вхідні параметри:**&#x20;

| Параметр   | Опис       | Формат даних | Обовʼязковість | Приклад |
| ---------- | ---------- | ------------ | -------------- | ------- |
| customerId | Id клієнта | string(255)  | Так            | 12345   |

**Вихідні параметри:**&#x20;

| Параметр   | Опис           | Формат даних | Приклад                              |
| ---------- | -------------- | ------------ | ------------------------------------ |
| customerId | Id клієнта     | string(255)  | 12345                                |
| token      | Id токену      | string       | SRrSBe5DOb7lrZ\_FS46fihty            |
| maskedPan  | маска картки   | string       | 516874\*\*\*\*\*\*7753               |
| merchantId | Id мерчанта    | string       | 137d9304-0368-11ed-b939-0242ac120002 |
| status     | статус токену  | string       | ACTIVE                               |

**Приклад тіла запиту**&#x20;

```json
{
    "customerId": "senderCustomerId"
}
```

**Приклад тіла відповіді**&#x20;

```json
{
    "result": [
        {
            "token": "-s9UCfCNN0YMk4ZOyZX8pWAt",
            "status": "ACTIVE",
            "maskedPan": "523244••••••0177",
            "customerId": "senderCustomerId",
            "merchantId": "137d9304-0368-11ed-b939-0242ac120002"
        }
    ]
}
```
