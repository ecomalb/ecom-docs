---
description: >-
  В розділі описано, яким чином відбувається шифрувння карткових даних, для
  забеспечення конфіденційності чутливих даних.
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Шифрування карткових даних

## Робота зі стандартом шифрування JWE

Для забезпечення конфіденційності передачі даних, використовується **JWE (JSON Web Encryption)** — стандарт, який визначає формат зашифрованих JSON повідомлень.

Для шифрування номеру картки (PAN) використовується публічний платіжний ключ `payment_public_key` , що надається під час генерації ключів (дивитись документацію "[Генерація ключів](https://docs.merchant.alb.ua/avtorizaciya-2.0/generaciya-klyuchiv#proces-otrimannya-klyuchiv)")&#x20;

Ключ відповідає формату JWK :&#x20;

```json
"paymentPublicKey": 
{
    "kty": "EC",
    "x": "Hp833OY6a0VbFD1j8xFyXWcAA-HOlyr7B_-B05esZUy32RA41s0oGAMTal23AX9d",
    "y": "WGHeR9PhKRymoA-ggsR3VkQTgdfzt7PWa8P2qNpu0cV83lmLxE57b8rR7ajBurvj",
    "crv": "P-384"
}
```

> **Публічний платіжний ключ (`payment_public_key`)** відповідає параметрам :
>
> ● "[kty](https://datatracker.ietf.org/doc/html/rfc7518#section-6.1)": "EC" - тип ключа
>
> ● "[crv](https://datatracker.ietf.org/doc/html/rfc7518#section-6.2.1.1)": "P-384" - еліптична крива ключа
>
> ● "[use](https://datatracker.ietf.org/doc/html/rfc7517#section-4.2)": "enc" – параметр, що використовується для криптування ключем
>
> ● "[alg](https://datatracker.ietf.org/doc/html/rfc7518#section-4.1)": ECDH-ES+A256KW - алгоритм для якого використовується ключ

### Приклад ендпоінта, для шифрування :&#x20;

{% hint style="warning" %}
**Запит викоритсосується тільки для тестування.**\
**Запит заборонено виконувати з реальними ключами.** \
**Запит шифрування потрібно реалізовувати на свої стороні.**
{% endhint %}

{% openapi-operation spec="alliancepay-api" path="/cipher/encrypt_by_jwk" method="post" %}
[OpenAPI alliancepay-api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/fb8eff4373522da43ea4180090691d083ec3b1bbf8c6e450cc1ddb88be245e55.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20251211%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20251211T111827Z&X-Amz-Expires=172800&X-Amz-Signature=9b59a7968aa02b0f150c06f5d7c7a25b29c7c6392a2122fcc9040221bb89e892&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

