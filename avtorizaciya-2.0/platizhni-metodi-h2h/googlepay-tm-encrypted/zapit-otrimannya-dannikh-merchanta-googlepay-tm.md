---
description: '{{url}}/ecom/jws/payments/google_pay/merchant/get_v1'
---

# Запит отримання даних мерчанта GooglePay™

Запит для отримання мерчантом даних та налаштувань GooglePay™ мерчанта

Опціональний запит. Можливий hard-coded данних GooglePay™ на стороні мерчанта

### Вхідні параметри частини payload JWS :

<table data-header-hidden><thead><tr><th>Параметр</th><th width="187">Опис</th><th>Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>id</td><td>Ідентифікатор продавця в системі gPay</td><td>string</td><td> "1234567890"</td></tr><tr><td>gPayMerchantName</td><td>Назва торговця</td><td>string</td><td>Example Merchant</td></tr><tr><td>gatewayIds</td><td>Id gateway</td><td>list</td><td> </td></tr><tr><td>countryCode</td><td>Значення кодів країн</td><td>string</td><td>UA</td></tr><tr><td>allowedAuthMethods</td><td><p>Поля, які підтримуються для автентифікації карткової транзакції.</p><ul><li>PAN_ONLY: цей метод автентифікації пов’язано з платіжними картками, які зберігаються в обліковому записі Google користувача. Дані про повернений платіж містять номер особового рахунку (PAN) із зазначенням місяця закінчення терміну дії та року закінчення терміну дії.</li><li>CRYPTOGRAM_3DS: цей метод автентифікації пов’язаний із картками, що зберігаються як маркери пристрою Android. Повернені платіжні дані містять криптограму 3-D Secure (3DS), згенеровану на пристрої.</li></ul><p> </p></td><td>string</td><td>["PAN_ONLY", "CRYPTOGRAM_3DS"]</td></tr><tr><td>allowedCardNetworks</td><td><p>Одна або кілька карткових мереж, які ви підтримуєте, а також підтримується Google Pay API.</p><ul><li>MASTERCARD</li><li>VISA</li></ul></td><td>string</td><td>["MASTERCARD", "VISA"]</td></tr><tr><td>enabled</td><td>Ознака активний чи не активний статс мерчанта</td><td> string</td><td>true/false</td></tr></tbody></table>



### Приклади :&#x20;

<details>

<summary>JWS Payload — тіло запиту перед підписанням</summary>

```json
{  }
```

</details>



<details>

<summary>JWS Payload — тіло відповіді перед підписанням</summary>

```json
{
    "id": "paujUKks5E7jFHdsGLgShAIZ",
    "gPayMerchantName": "gPayMerchantName00",
    "gatewayIds": [
        "9ACW_gv4dRs6yLIzdW_WZUNw"
    ],
    "allowedCardNetworks": [
        "MASTERCARD",
        "VISA"
    ],
    "allowedAuthMethods": [
        "PAN_ONLY",
        "CRYPTOGRAM_3DS"
    ],
    "enabled": true,
    "countryCode": "UA"
}
```

</details>
