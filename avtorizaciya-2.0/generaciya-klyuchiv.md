# Генерація ключів

## &#x20;Процес отримання ключів:&#x20;

1. Потібно перейти на [сторінку генерації ключів](https://merchant.alb.ua/jwt)&#x20;
2. Згенерувати пару ключів&#x20;
3. Зберегти на свої стороні частину `private_key`&#x20;
4. Надіслати співробітнику банку частину `public_key`&#x20;
5. Після виконання реєстрації співробітником банку, буде надіслано всі необхідні дані для роботи з підписанням&#x20;

> Буде надано такі параметри:&#x20;
>
> * `merchantId` - внутрішній ідентифікатор термінала (використовується в запитах)&#x20;
> * `kid` - ідентифікатор ключів&#x20;
> * `payment_public_key` - публічний платіжний ключ (використовується для шифрування карткових даних). Ознайомитись можна за посиланням : [https://docs.merchant.alb.ua/kriptuvannya-danikh#zapit-kriptuvannya-nomeru-kartki](https://docs.merchant.alb.ua/kriptuvannya-danikh#zapit-kriptuvannya-nomeru-kartki)

### Вимоги до ключів для підписання

Для підписання та перевірки запитів використовується асиметрична криптографія. Мерчант повинен згенерувати пару ключів (приватний та публічний) відповідно до однієї з підтримуваних комбінацій алгоритмів.

#### Підтримувані алгоритми

| Тип ключа           | Підтримувані алгоритми |
| ------------------- | ---------------------- |
| RSA                 | RS256, RS384, RS512    |
| Elliptic Curve (EC) | ES256, ES384, ES512    |

#### Вимоги до ключів

**RSA**

* Тип ключа (`kty`): `RSA`&#x20;
* Призначення (`use`): `sig` (підпис)
* Алгоритм (`alg`): `RS256`, `RS384` або `RS512`

**Elliptic Curve (EC)**

| Алгоритм | Крива (`crv`) |
| -------- | ------------- |
| ES256    | P-256         |
| ES384    | P-384         |
| ES512    | P-521         |

* Тип ключа (`kty`): `EC`
* Призначення (`use`): `sig` (підпис)
* Алгоритм (`alg`): один із підтримуваних ES256 / ES384 / ES512

#### Формат ключів

Публічний та приватний ключі повинні бути представлені у форматі **X.509 PEM**.

**Приклад вигляду ключів :**&#x20;

{% tabs %}
{% tab title="Private_key" %}
```
-----BEGIN PRIVATE KEY-----
MEECAQAwEwYHKoZIzj0CAQYIKoZIzj0DAQcEJzAlAgEBBCDCOWlpGDoMfQ25x4Ku
K9J96WuwVn3Ri/UTYEMIV/KPXA==
-----END PRIVATE KEY-----
```
{% endtab %}

{% tab title="Public_key" %}
```
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEHZ+3wM4Hmyq6f1H7RJjU4SSrqjt3
8f2VX9aS8ikCxXHID92roxYMsDBzAcVRPwNPiexCu5eS/UzyJsP8e9eydA==
-----END PUBLIC KEY-----
```
{% endtab %}
{% endtabs %}

