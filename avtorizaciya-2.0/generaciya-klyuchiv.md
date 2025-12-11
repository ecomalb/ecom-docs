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

### Параметри ключів для підписання

Ключі генеруються за такими параметрами :&#x20;

* `kty`: `"EC"` (Elliptic Curve)
* `crv`: `"P-256"` - (ES256) - найпоширеніша крива, підтримується більшістю фреймворків і браузерів, має достатній рівень безпеки.
* `use`: `"sig"` - означає, що ключ використовується для підпису (signature)
* `alg`: `"ES256"`.

Відбражаються у форматі `X.509 PEM Format`

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

