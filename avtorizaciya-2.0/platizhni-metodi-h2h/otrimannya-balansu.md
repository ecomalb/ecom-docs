---
description: POST {{url}}/ecom/jws/balance/get_v1
---

# Отримання балансу

### Вихідні параметри частини payload JWS :

<table data-full-width="true"><thead><tr><th>Параметр</th><th width="234">Опис</th><th width="160.50000000000003">Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantId</td><td>Id мерчанта</td><td>string</td><td>235d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>balanceAmount</td><td>Сума на балансі</td><td>string</td><td>47</td></tr><tr><td>balanceLimit</td><td>Сума овердрафт ліміту для мерчанта</td><td>string</td><td>0</td></tr><tr><td>totalAmount</td><td>Загальна сума</td><td>string</td><td>47</td></tr></tbody></table>

### Приклади :

<details>

<summary>JWS Payload — тіло запиту перед підписанням</summary>

```
{ }
```

</details>



<details>

<summary>JWS Payload — тіло відповіді перед підписанням</summary>

```
{
    "merchantId": "235d9304-0368-11ed-b939-0242ac120002",
    "balanceAmount": 47,
    "balanceLimit": 0,
    "totalAmount": 47
}
```

</details>

