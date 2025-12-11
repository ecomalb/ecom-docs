---
description: '{{url}}/ecom/jws/token/create_v1'
---

# Запит створення токену

### Вхідні параметри частини payload JWS :

<table data-full-width="true"><thead><tr><th>Параметр</th><th>Опис</th><th width="154">Формат даних</th><th width="149">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта</td><td>string (36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>customerId</td><td>Id клієнта</td><td>string(255)</td><td>Так</td><td>12345</td></tr><tr><td>encryptedCardNumber</td><td>Номер карти зашифрований в JWE за допомогою публічного платіжного ключа</td><td>string</td><td>Так</td><td>5573670000000304 (розшифрований вигляд)</td></tr><tr><td>encryptedExpDate</td><td>термін дії карти зашифрованний в JWE. </td><td>string</td><td>Так</td><td>2503 (розшифрований вигляд)</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00 </td></tr></tbody></table>

### Вихідні параметри частини payload JWS :

| Параметр   | Опис                             | Формат даних | Приклад                              |
| ---------- | -------------------------------- | ------------ | ------------------------------------ |
| customerId | Id клієнта                       | string(255)  | 14534543                             |
| token      | Id токену                        | string       | _TlcMw5uKf9Gp6nM\_7cHGAf_            |
| maskedPan  | маска картки                     | string       | 528529••••••0255                     |
| merchantId | Id мерчанту згенерований в Єкомі | string(36)   | 137d9304-0368-11ed-b939-0242ac168002 |
| status     | статус токену                    | string       | ACTIVE                               |

### Приклади :

<details>

<summary>JWS Payload — тіло запиту перед підписанням</summary>

```
{
    "merchantId": "137d9304-0368-11ed-b939-0242ac168002",
    "customerId": "14534543",
    "encryptedCardNumber": "eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoidE1sRVIyWGNHWGpxUTg2dEpRTEgyeHRyQ2NvVzdLUXJnVVZRNVJtQmNSaEZycmhnZnlxVW5sLTF2WVh0cjZIeiIsInkiOiJ3T0xyV3R5RzBqYlA4OWlUaVl1UkF2Si1valNoZE0yVWUycnVlYkhqUmlIMEt5clJELVBfdGFZV0ZxX3dGemRvIiwiY3J2IjoiUC0zODQifX0.ZAIlVIU6nh2Nt5yAx1QVolk82fEb-Gyw8X6DZxmhCbq-E1Kvz83jYQ.HGw9tqjLb8HtdmeF.nCXcOe4S9KcX-k4MKHNpXw.bDUYIFzik3HfHBrYYz-Wdw",
    "encryptedExpDate": "eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoibHZxMTdaWnBVWTNsX1JlcFpFU0lRUnlOeWlpS09xU0tfRUF5aHdvNGk4c0QwaVF4ZnE3ZTQxM1VjRFJMbjJQZyIsInkiOiIwVXJkcjJialhOTS16SUxiOTg1bGNZYjJrcUJReGNBMkZSNzdhWXhVVU1qUHFNR0Z6SlBxUDhpT2hGaU9pZHNiIiwiY3J2IjoiUC0zODQifX0.L35f-ycKXciH_WM2Zh-iOzMqsjL9pTz6OBPu8BVkqj9kp8Ck-faNjg.Q5CGl2neg0laf4TP.TZ_giQ.w7e9zx6LTbA_e607veBRHA",
    "date": "2025-02-20 16:42:05.00+00:00",
    "merchantRequestId": "8d1b3cbb-3d31-4067-81bd-57edbe050011"
}
```

</details>



<details>

<summary>JWS Payload — тіло відповіді перед підписанням</summary>

```
{
    "customerId": "14534543",
    "token": "_TlcMw5uKf9Gp6nM_7cHGAf_",
    "maskedPan": "528529••••••0255",
    "merchantId": "137d9304-0368-11ed-b939-0242ac168002",
    "status": "ACTIVE"
}
```

</details>
