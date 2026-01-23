# Робота з підписанням

## Структура JWS

Типовий JWS складається з трьох частин, розділених крапками (`.`):

```
{Base64Url(header)}.{Base64Url(payload)}.{Base64Url(signature)}
```

Де:

* **header** — описує загальні мета данні&#x20;

<pre class="language-json"><code class="lang-json"><strong>{
</strong><strong>    "alg": "ES256",  // Алгоритм підписання 
</strong><strong>    "kid": "uuid",  // Ідентифікатор публічного ключа (надається від співробітника банку)
</strong><strong>    "ts" : "1769174930000", // Дата та час у форматі timestamp в мілісекундах
</strong><strong>    "targetUrl" : "/ecom/jws/payments/create/purchase_v3" // URL на який надсилається запит
</strong>}
</code></pre>

* **payload** — дані, які потрібно передати (необхідні данні для коженого запиту, дивитись у документації [Платіжні методи H2H](https://docs.merchant.alb.ua/avtorizaciya-2.0/platizhni-metodi-h2h)).
* **signature** — цифровий підпис, створений за допомогою приватного ключа відправника.

Приклад JWS:

```
eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.
eyJ1c2VySWQiOiIxMjMiLCJyb2xlIjoiYWRtaW4ifQ.
MEYCIQDmG...
```

**Як виконується підписання**

1. Формується **header** (мета дані) **payload** (дані запиту).
2. Обидві частини кодуються у формат **Base64Url**.
3.  Об’єднуються в одне повідомлення:

    ```
    signingInput = base64Url(header) + "." + base64Url(payload)
    ```
4. Це повідомлення підписується приватним ключем (детальніше як отирмати ключ - [Генерація ключів](generaciya-klyuchiv.md)) за вказаним алгоритмом .
5. Результат (signature) додається як третя частина JWS.

Приклад генерації JWS можна переглянути на сайті [https://www.jwt.io/](https://www.jwt.io/)

**Приклад коду для генерації підпису:**&#x20;

{% tabs %}
{% tab title="JavaScript" %}
```javascript
import { CompactSign, importPKCS8 } from 'jose';

// === Дані ===
const privateKeyPem = `
-----BEGIN EC PRIVATE KEY-----
MHcCAQEEIBOS+Xg3qgYSe5T4H2AoB0zWrhb0jNmcdW6o2bTXXWlQoAoGCCqGSM49
AwEHoUQDQgAEMO4qQsgPskZ4E1X6nHZU9yHnJrZ97K3QAjQ1oG1zgrht3mA4+lf5
aMqTIk1glXZpMT4pAzTURmmP2+prvQul3g==
-----END EC PRIVATE KEY-----
`;

const header = {
  alg: "ES256",
  kid: "9a3f6e6d-4f56-4b8b-99d3-24db19f54d8a",
  ts: Math.floor(Date.now() / 1000),
  targetUrl: "/ecom/jws/payments/create/purchase_v3"
};

// payload — це тіло запиту
const payload = {
  merchantId: "12345",
  amount: "1000.00",
  currency: "UAH",
  orderId: "ORD-2025-001"
};

// === Генерація JWS ===
const privateKey = await importPKCS8(privateKeyPem, 'ES256');
const encoder = new TextEncoder();

const encodedHeader = Buffer.from(JSON.stringify(header)).toString('base64url');
const encodedPayload = Buffer.from(JSON.stringify(payload)).toString('base64url');
const signingInput = `${encodedHeader}.${encodedPayload}`;

const sign = new CompactSign(encoder.encode(JSON.stringify(payload)))
  .setProtectedHeader(header);

const jws = await sign.sign(privateKey);

console.log("JWS:", jws);


```
{% endtab %}

{% tab title="Python" %}
```python
from jwcrypto import jwk, jws
import json, time, base64

# === Приватний ключ ===
private_key_pem = """-----BEGIN EC PRIVATE KEY-----
MHcCAQEEIBOS+Xg3qgYSe5T4H2AoB0zWrhb0jNmcdW6o2bTXXWlQoAoGCCqGSM49
AwEHoUQDQgAEMO4qQsgPskZ4E1X6nHZU9yHnJrZ97K3QAjQ1oG1zgrht3mA4+lf5
aMqTIk1glXZpMT4pAzTURmmP2+prvQul3g==
-----END EC PRIVATE KEY-----"""

key = jwk.JWK.from_pem(private_key_pem.encode())

header = {
    "alg": "ES256",
    "kid": "9a3f6e6d-4f56-4b8b-99d3-24db19f54d8a",
    "ts": int(time.time()),
    "targetUrl": "/ecom/jws/payments/create/purchase_v3"
}

payload = {
    "merchantId": "12345",
    "amount": "1000.00",
    "currency": "UAH",
    "orderId": "ORD-2025-001"
}

protected = base64.urlsafe_b64encode(json.dumps(header).encode()).decode().rstrip("=")
body = base64.urlsafe_b64encode(json.dumps(payload).encode()).decode().rstrip("=")

signing_input = f"{protected}.{body}"

signature = jws.JWS(json.dumps(payload))
signature.add_signature(key, protected=json.dumps(header), alg="ES256")

print("JWS:", signature.serialize(compact=True))
```
{% endtab %}

{% tab title="Java" %}
```java
import com.nimbusds.jose.*;
import com.nimbusds.jose.crypto.*;
import com.nimbusds.jose.util.Base64URL;

import java.security.*;
import java.security.spec.*;
import java.util.*;

public class GenerateJWS {
    public static void main(String[] args) throws Exception {
        // Завантажуємо приватний ключ (EC P-256)
        String privateKeyPEM = """
        -----BEGIN EC PRIVATE KEY-----
        MHcCAQEEIBOS+Xg3qgYSe5T4H2AoB0zWrhb0jNmcdW6o2bTXXWlQoAoGCCqGSM49
        AwEHoUQDQgAEMO4qQsgPskZ4E1X6nHZU9yHnJrZ97K3QAjQ1oG1zgrht3mA4+lf5
        aMqTIk1glXZpMT4pAzTURmmP2+prvQul3g==
        -----END EC PRIVATE KEY-----
        """;

        // (Простий приклад: створити EC ключову пару)
        KeyPairGenerator keyGen = KeyPairGenerator.getInstance("EC");
        keyGen.initialize(Curve.P_256.toECParameterSpec());
        KeyPair pair = keyGen.generateKeyPair();

        Map<String, Object> payload = new HashMap<>();
        payload.put("merchantId", "12345");
        payload.put("amount", "1000.00");
        payload.put("currency", "UAH");
        payload.put("orderId", "ORD-2025-001");

        JWSHeader header = new JWSHeader.Builder(JWSAlgorithm.ES256)
                .customParam("kid", "9a3f6e6d-4f56-4b8b-99d3-24db19f54d8a")
                .customParam("ts", System.currentTimeMillis() / 1000)
                .customParam("targetUrl", "/ecom/jws/payments/create/purchase_v3")
                .build();

        Payload jwsPayload = new Payload(new com.nimbusds.jose.util.JSONObjectUtils().toJSONString(payload));

        JWSObject jwsObject = new JWSObject(header, jwsPayload);
        jwsObject.sign(new ECDSASigner((ECPrivateKey) pair.getPrivate()));

        System.out.println("JWS: " + jwsObject.serialize());
    }
}
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php
require 'vendor/autoload.php';

use Jose\Component\Core\JWK;
use Jose\Component\Signature\JWSBuilder;
use Jose\Component\Signature\Algorithm\ES256;
use Jose\Component\Core\Util\JsonConverter;

// Приватний ключ
$privateKey = <<<EOD
-----BEGIN EC PRIVATE KEY-----
MHcCAQEEIBOS+Xg3qgYSe5T4H2AoB0zWrhb0jNmcdW6o2bTXXWlQoAoGCCqGSM49
AwEHoUQDQgAEMO4qQsgPskZ4E1X6nHZU9yHnJrZ97K3QAjQ1oG1zgrht3mA4+lf5
aMqTIk1glXZpMT4pAzTURmmP2+prvQul3g==
-----END EC PRIVATE KEY-----
EOD;

$jwk = JWK::createFromPem($privateKey);

$header = [
    'alg' => 'ES256',
    'kid' => '9a3f6e6d-4f56-4b8b-99d3-24db19f54d8a',
    'ts' => time(),
    'targetUrl' => '/ecom/jws/payments/create/purchase_v3'
];

$payload = [
    'merchantId' => '12345',
    'amount' => '1000.00',
    'currency' => 'UAH',
    'orderId' => 'ORD-2025-001'
];

$jwsBuilder = new JWSBuilder(null, [new ES256()]);
$jws = $jwsBuilder
    ->create()
    ->withPayload(JsonConverter::encode($payload))
    ->addSignature($jwk, $header)
    ->build();

$serializer = new \Jose\Component\Signature\Serializer\CompactSerializer();
echo "JWS: " . $serializer->serialize($jws, 0);

```
{% endtab %}
{% endtabs %}

## Вимоги до JWS

### **1. Загальні вимоги до JWS :**&#x20;

* &#x20;Усі запити до API повинні бути підписані за допомогою **JWS (JSON Web Signature)**.
* Підпис формується відповідно до алгоритму, що відповідає типу ключа, переданого у параметрі `kid`.
* При валідації JWS система перевіряє правильність **header**, **payload** та **signature**.

У разі порушення будь-якої з вимог запит відхиляється з помилкою.

### 2. Вимоги до частини header JWS :&#x20;

ПІдтримувальні параметри header :&#x20;

<table><thead><tr><th>Поле</th><th>Опис</th><th>Тип</th><th>Обов'язкове</th><th>Приклад</th></tr></thead><tbody><tr><td><code>alg</code></td><td>Алгоритм підпису, що відповідає типу ключа</td><td>string</td><td>так</td><td><pre><code><strong>ES256
</strong></code></pre></td></tr><tr><td><code>kid</code></td><td>Ідентифікатор публічного ключа</td><td>string</td><td>так</td><td><pre><code>28da60c2-d60f-404e-b4da-6b089fb29555
</code></pre></td></tr><tr><td><code>ts</code></td><td>Час генерації JWS по UTC(Kyiv)</td><td>number (Unix timestamp, milliseconds)</td><td>так</td><td><pre><code>1769174930000
</code></pre></td></tr><tr><td><code>targetUrl</code></td><td>URL, для якого формується запит</td><td>string (URL)</td><td>так</td><td><pre><code><strong>/ecom/jws/payments/create/purchase_v3
</strong></code></pre></td></tr></tbody></table>

#### 2.1. **Перевірка терміну дії токена (`ts`)**

* Поле `ts` повинно містити timestamp (в мілісекундах).
* JWS вважається дійсним протягом **60 секунд** з моменту формування.

{% hint style="danger" %}
#### Умови помилки:

* Якщо `ts` > (поточний час + 60 секунд) або `ts` < (поточний час − 60 секунд).
* Якщо значення `ts` не відповідає формату `1769174930000`&#x20;
* Якщо значення не відповідає UTC по Київу
{% endhint %}

#### 2.2. **Перевірка `targetUrl`**

Система перевіряє, що значення:

* відповідає формату URL,
* є дозволеним маршрутом API,
* відповідає фактичному endpoint, куди надсилається запит.\
  Приклад : \
  Запит надійщо в на- `{url}/ecom/jws/payments/create/purchase_v3`\
  Фактичний - `/ecom/jws/payments/create/purchase_v3`

{% hint style="danger" %}
#### **Умови помилки:**

* Якщо `targetUrl` невалідний, має неправильний формат або не співпадає з фактичним шляхом запиту.
* Якщо запит надійшов на `/ecom/jws/payments/account_to_card_v3` , а значення `targetURL` вказаний `/ecom/jws/payments/create/purchase_v3` .
{% endhint %}

#### 2.3. **Перевірка алгоритму підпису (`alg`)**

Значення `alg` повинно відповідати алгоритму пари ключів, що використовується для підпису `ES256`.

{% hint style="danger" %}
#### Умова помилки:

* Якщо в `alg` передано значення, що не відповідає алгоритму згенерованого ключа.
{% endhint %}

#### 2.4. **Перевірка існування ключа (`kid`)**

* `kid` повинен відповідати одному з активних ключів мерчанта.

{% hint style="danger" %}
#### Умова помилки:

Якщо ключ із зазначеним `kid` не існує.
{% endhint %}



### 3. **Вимоги до JWS Payload**

Payload JWS повинен містити **тіло запиту (request body)** у JSON, яке повністю відповідає вимогам конкретного endpoint’у.

Приклад: якщо запит виконується до `/ecom/jws/payments/create/purchase_v3`, то саме тіло цього запиту ([Запит проведення PURCHASE Крок 1](https://docs.merchant.alb.ua/avtorizaciya-2.0/platizhni-metodi-h2h/purchase/zapit-provedennya-purchase-krok-1)) включається у payload JWS.

#### 3.1. **Валідація структури тіла запиту**

Payload повинен:

* містити всі обов'язкові параметри, визначені для відповідного endpoint’у,
* відповідати JSON схемі,
* проходити внутрішню бізнес-валідацію.

{% hint style="danger" %}
#### Умова помилки:

Якщо тіло запиту не відповідає вимогам (відсутні поля, неправильні типи).
{% endhint %}

#### 3.2. **Перевірка мерчанта (`merchantId`)**

Усі операції повинні виконуватися від імені існуючого мерчанта.

{% hint style="danger" %}
#### Умова помилки:

Якщо в payload передано `merchantId`, який:

* не існує
* деактивований
* не прив’язаний до ключа `kid`
{% endhint %}
