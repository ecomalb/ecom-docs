# Авторизація

#### Авторизація запитів

Для авторизації запиту необхідно до запиту додати заголовки:

> x-api\_version:V1
>
> x-device\_id:\{{deviceId\}}
>
> x-refresh\_token:\{{refreshToken\}}

#### Відновлення авторизації

При виконанні запитів, у разі отримання у відповіді http status 401, необхідно відновити авторизаційні дані Запит оновлення сесії та виконати невдалий запит ще раз

#### Таймаут

Інформація щодо таймаутів буде додана у наступній версії документу.

#### Робота з платежами

Платіж - тип операцій, що використовується для оплати на сайтах товарів/сервісів/послуг за допомогою платіжної картки.

По операціям Платежу передбачено верифікацію картотримача за допомогою технології 3D Secure, якщо карта залучена до даної програми.

#### Дані для проведення тестування

serviceCode для авторизації девайсу - UUID, приклад a51e68aa-c6fa-11ed-afa1-0242ac120005.&#x20;

В продуктивному середовищі генерується Банком окремо для кожного мерчанта

Ключ для авторизації:

```json
{
    "kty": "EC",
    "d": "QVwaujXBuM1mdyNSadU5qSjRk5xggY-aX7yzes_qyNQC9nTVO1SmNBHd_fBzZILd",
    "use": "enc",
    "crv": "P-384",
    "x": "lxF9kVkpdTRqd256CO0Q3fOEAPcek-U_Q72UoySdXXZWr9Tf8bSMhc8gwVbgtDC",
    "y": "3aQaGq0Va9OshPr63jZ2KEcfO1jqibz6bKFeJr6K6h4dHFGj298hv7sb6bYaUyD",
    "alg": "ECDH-ES+A256KW"
}
```

Payment ключ

```json
{
    "kty": "EC",
    "use": "enc",
    "crv": "P-384",
    "x": "lxF9kVkpdTRqd256CO0Q3fOEgAPcek-U_Q72UoySdXXZWr9Tf8bSMhc8gwVbgtDC",
    "y": "3aQaGq0Va9OsGhPr3jZ2KEcfO1jqibz6bKFeJr6K6h4dHFGj298hv7sb6bYaUyD",
    "alg": "ECDH-ES+A25KW"
}
```

URL - https://api-ecom-prod.bankalliance.ua

#### Headers для запитів<br>

| Параметр         | Опис                                              | Приклад                              |
| ---------------- | ------------------------------------------------- | ------------------------------------ |
| x-api\_version   | Версія api                                        | v1                                   |
| x-device\_id     | Генерується при запиті authorize\_virtual\_device | f7b244ae-57e7-4fe2-89d7-7d6a02a17048 |
| x-refresh\_token | Генерується при запиті authorize\_virtual\_device | 9a64d090-732c-4e28-9c57-609083b8bd56 |

