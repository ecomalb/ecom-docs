---
description: '{{url}}/ecom/execute_request/token/v1/get'
---

# Запит отримання даних токену

**Вхідні параметри:**&#x20;

| Параметр | Опис      | Формат даних | Обовʼязковість | Приклад                   |
| -------- | --------- | ------------ | -------------- | ------------------------- |
| token    | Id токену | string       | Так            | SRrSBe5DOb7lrZ\_FS46fihty |

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
    "token": "SRrSBe5DOb7lrZ_FS46fihty"
}
```

**Приклад тіла відповіді**&#x20;

```json
{
    "result": [
        {
            "token": "-SRrSBe5DOb7lrZ_FS46fihty",
            "status": "ACTIVE",
            "maskedPan": "523244••••••0177",
            "customerId": "senderCustomerId",
            "merchantId": "137d9304-0368-11ed-b939-0242ac120002"
        }
    ]
}
```
