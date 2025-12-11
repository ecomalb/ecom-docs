---
description: '{{url}}/ecom/jws/payments/merchant/get_v1'
---

# Запит отримання данних мерчанта aPау

Запит для отримання мерчантом даних та налаштувань аРау мерчанта

Опціональний запит. Можливий hard-coded данних аРау на стороні мерчанта

### Вхідні параметри частини payload JWS :

| Параметр             | Опиc                                                                                                                 | Формат даних	 | Приклад                                    |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- | ------------- | ------------------------------------------ |
| merchantCapabilities | визначає, які можливості підтримує мерчант для обробки платежів через Apple Pay                                      | object        | supports3DS, supportsCredit, supportsDebit |
| supportedNetworks    | визначає список платіжних мереж (типів карток), які підтримуються мерчантом для обробки платежів через Apple Pay.    | object        | visa, masterCard                           |
| countryCode          | дволітерний код країни (згідно зі стандартом ISO 3166-1 alpha-2), де буде здійснено транзакцію через Apple Pay.      | string        | UA                                         |
| currencyCode         | визначає валюту, в якій буде здійснено платіж через Apple Pay. Трилітерний код валюти згідно зі стандартом ISO 4217. | string        | UAH                                        |

### Приклади :

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
    "merchantCapabilities": [
        "SUPPORTS_3DS"
    ],
    "supportedNetworks": [
        "VISA"
    ],
    "countryCode": [
        "UA"
    ],
    "currencyCode": "UAH"
}
```

</details>
