---
description: Початок роботи
---

# Аутентифікація

### Для початку роботи з платформою AlliancePay необхідно:

1\. Звернутись до АТ “БАНК АЛЬЯНС” для отримання інформації щодо умов послуги інтернет-еквайринг.

2\. Відкрити рахунок в АТ “БАНК АЛЬЯНС”.

3\. Підписати договір про підключення до послуги інтернет-еквайрингу.

4\. Здійснити підключення до тестового стенду та провести тестові операції.

5\. Здійснити підключення до продуктового середовища.

6\. Почати користуватись послугою інтернет-еквайрингу.

### Процес створення нового сеансу безпеки користувача

Процес створення нового сеансу безпеки користувача включає в себе ряд послідовних дій, таких як:

* Генеруємо клієнтські ключі “Процес генерації комунікаційних JWK ключів клієнта”
* Отримуємо зашифровані авторизаційні дані зашифрувавши тіло запиту “Процес створення JWE зашифрованих даних” та відправити “Запит створення технічної сесії”
* Розшифровуємо отримані дані&#x20;

Уточнення: URL криптування і розкриптування :

<kbd>\{{url\}}cipher/decrypt\_by\_jwk?message=</kbd>

<kbd>\{{url\}}cipher/encrypt\_by\_jwk?message=</kbd>

**! тільки для допомоги під час тестів!  Їх заборонено виконувати з прод ключами.**

### **Для шифрування та розшифрування використовується :**&#x20;

* Алгоритм шифрування ключів (alg) - <kbd>ECDH-ES+A256KW</kbd>
* Шифрування тіла запиту по алгоритму (enc) - <kbd>A256GCM</kbd>

#### **Приклад по encrypt/decrypt**&#x20;

```python
def encrypt_data(self, msg: str, use_server_public_key: bool = False) -> str:
        """Get compact JWE token with encrypted data"""

        if not use_server_public_key:
            with open(self.public_key, 'rb') as public_key_file:
                public_key_raw = json.loads(public_key_file.read().decode())

        public_key = jwk.JWK()
        key_raw = self.server_public_key if use_server_public_key else public_key_raw
        public_key.import_key(**key_raw)
        protected_header = {'alg': 'ECDH-ES+A256KW', 'enc': 'A256GCM'}

        jwetoken = jwe.JWE(msg.encode('utf-8'), recipient=public_key, protected=protected_header)
        return jwetoken.serialize(compact=True)

    def decrypt_data(self, msg: str) -> str:
        """Get decrypted data (from JWE)"""

        with open(self.private_key, 'rb') as private_key_file:
            private_key_raw = json.loads(private_key_file.read().decode())

        private_key = jwk.JWK()
        private_key.import_key(**private_key_raw)

        jwetoken = jwe.JWE()
        jwetoken.deserialize(msg, key=private_key)
        return jwetoken.payload.decode()
```

### Процес генерації комунікаційних JWK ключів клієнта

Генерація публічного та приватного ключа (JSON Web Key) здійснюється з наступними параметрами:

●       "[kty](https://datatracker.ietf.org/doc/html/rfc7518#section-6.1)": "EC" - тип ключа

●       "[crv](https://datatracker.ietf.org/doc/html/rfc7518#section-6.2.1.1)": "P-384" - еліптична крива ключа

●       "[use](https://datatracker.ietf.org/doc/html/rfc7517#section-4.2)": "enc" – параметр, що використовується для криптування ключем

●       "[alg](https://datatracker.ietf.org/doc/html/rfc7518#section-4.1)": ECDH-ES+A256KW - алгоритм для якого використовується ключ

Приклад генерації ключа для ознайомлення наведено на сайті[ https://mkjwk.org/](https://mkjwk.org/) .

Процес створення[ JWE](https://datatracker.ietf.org/doc/html/rfc7516) зашифрованих даних

Об'єкт є зашифрованими даними.

Для створення необхідно вказати наступні параметри:

●       Кодування даних, що шифруються UTF-8

●       Алгоритм шифрування ECDH-ES+A256KW

●       Метод шифрування A256GCM

●       Та використовувати відповідний алгоритму публічний ключ.

**Приклад тіла перед шифруванням:**

```json
{
  "deviceType": "ECOM_MERCHANT_SERVICE_DEVICE",
  "clientPublicKey": {
    "kty": "EC",
    "crv": "P-384",
	"x": "Q0aVpIzurAJeLgcwr9SwrjBaxt6vWU9Xt9Om5WseRVHOK0KHt1fS-TmM4nNwocyl",
	"y": "nugxKjzsgyCBY8h095r3dex5LL0MduzU8ovLPYnl3jlExzpSG4sFTsBbUWJo8GLP"
  }
}
```

**Приклад JWE після шифрування:**

```json

eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiSVprUG1oVm5fQUd2RkJXS2dIYmtfOFlLX2Q1aXZabHJJU19DaUxublhlVUkyX1NtSC0wWkJDOWkySDg1c3ladCIsInkiOiJ6SUFkSS1wNXZrdjVuVjNpSVNqMlFiSW85NnU0eXBhZVg0WHBJSUhiYlp4LWhkc3hwLUVCbDIwRDlNOTVHTWtQIiwiY3J2IjoiUC0zODQifX0.jfDIZ64JlVbdOgXkh0bqX6uA8H6Pkkg6s861OKn_vBtIQYk4BRxPjA.9ns8h0iFDcmG_hib.USraeD8abgHZwD_kas3L1rO1U0n_YhLx_LJpxKICAoVqVQ.myDB-We0sg1l5nzfi7b2sg

```

#### Процес розшифрування JWE даних

Приклад JWE токену

```json
eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiSVprUG1oVm5fQUd2RkJXS2dIYmtfOFlLX2Q1aXZabHJJU19DaUxublhlVUkyX1NtSC0wWkJDOWkySDg1c3ladCIsInkiOiJ6SUFkSS1wNXZrdjVuVjNpSVNqMlFiSW85NnU0eXBhZVg0WHBJSUhiYlp4LWhkc3hwLUVCbDIwRDlNOTVHTWtQIiwiY3J2IjoiUC0zODQifX0.jfDIZ64JlVbdOgXkh0bqX6uA8H6Pkkg6s861OKn_vBtIQYk4BRxPjA.9ns8h0iFDcmG_hib.USraeD8abgHZwD_kas3L1rO1U0n_YhLx_LJpxKICAoVqVQ.myDB-We0sg1l5nzfi7b2sg
```

**Приклад даних після розшифрування JWE токену**

```json
{
  "authToken": "c8e28b98-e3bd-42f3-8cba-7b3c3dd5c9da",
  "deviceId": "8485ff92-8ac3-4af1-aaa7-e72edfed2516",
  "serverPublicKey": {
	"kty": "EC",
	"crv": "P-384",
	"x": "glGAHNVNkXbygpcRnhoEGSUEQM-s8RrcaxY7HSJ4Cs0QIreWxYEJI2iz0W4ZtH8a",
	"y": "AQ_vq8Ks_dTB-HiQrPi_fpE-nlQXbHoEeInURhZFVFc1bpi7NqynflKnyBWLy590"
  }
}
```

#### Запит створення технічної сесії&#x20;

Приклад тіла запиту

```json
curl --location 'https://api-ecom-prod.bankalliance.ua/api-gateway/authorize_virtual_device' \
--header 'x-api_version: 1' \
--header 'Content-Type: application/json' \
--header 'Cookie: visid_incap_2770403=fJEGXzciTnG2/y/pST3lzBM/JGMAAAAAQUIPAAAAAAAV+dwIpk/4YrgvV5ijeEu6' \
--data '
{
    "serviceCode": "137d9304-0368-11ed-b939-0242ac120002"
}'
```

**Приклад відповіді**

```json
{
"jwe": "eyJhbGciOiJFQ0RILUVTK0EyNTZLVyIsImVuYyI6IkEyNTZHQ00iLCJlcGsiOnsia3R5IjoiRUMiLCJ4IjoiZ3F2M0xDYnpDcEZoaWhEQlRZX1JxSFN6cUZsLWJYYVZjUHhJU2w4UmNPbHdjNU5UNnpvd3Y1WWhTQW5sekxPMCIsInkiOiJENWpYX2t4UGZVYlJySmVTZGNQbnhzN0dNMlZuZTdvSHA5N3g2SVNPdWNJdU81SVY2R2pFa3NRSlBicGQ2bWVfIiwiY3J2IjoiUC0zODQifX0.nbpNZhLmDpzMdhntvVOrpdLOLu6Ryhhb-S08LgdN8iJscD4j3mqX_w.8WWRrwzW93i0oGui.jjm3mvrLxDvJTy6-lKzXHTzMliD7x3cV3ZhgAcmgWL8uyHj3Cpb5LtcdUM6KxzBsAj0CWmdjj_VCzbloEHJVQCoDPpCqIe8ScIh5irXB3hG8onyK0tKXOibf7gRoEIWES_OuT3yAfXfNn0DuEK6PhKH1sihLMDWD_ns7CATBy6atZQkk00SkswDLgDVucCakC5RmyrDDFHsaEcKAIh6eehlhHotR6x82v9qplYObKMIqneEmYRUrildPyi43_RXmkSZUFt2Bx5Q7SEINQsFw6qRPzAkhpPH2d5JWefDr3elamiJeibMJQDcKcfUDnDCviX-e2Wf3sTnacufV8O5s1hDpfJYZAxZonGK8g3CvcWk34EsnPD0pm8DOoTtSeIP9cgS4w05s53LxbFPH9xXYtxkfrSBVtnbiHcZ37GVWOdEqVeqgmDKizu6WxQnW9oJdNEsG6a5FavarFURvS5Xgz46cluYj3ppZSqIQiRSRhNDH0AD9fFPeskvsGjZ5O8efA3eRyT5gNKCO05I9ZtnC.w3pu8oSnWaBkbBjQyQN9hQ"
}

```

#### **Запит розшифрування технічної сесії**

Приклад тіла запиту

```json
curl --location 'https://api-ecom-release.develop.bankalliance.ua/cipher/decrypt_by_jwk?message={{responseJwe}}' \
--header 'Content-Type: application/json' \
--header 'Cookie: visid_incap_2770403=fJEGXzciTnG2/y/pST3lzBM/JGMAAAAAQUIPAAAAAAAV+dwIpk/4YrgvV5ijeEu6' \
--data '
{
    "kty": "EC",
    "d": "xVoCzl9Vvlk_bP_O1OLmlTSN9P07fq_7bEBnpQhoqo29PV2TR7smqu5nAz0wZhZ_",
    "use": "enc",
    "crv": "P-384",
    "x": "tfOqYVvawSq5HDGvWd_zm-ha8tDuZci5THnAokWJpdZSUk40VpAtofDY_Q8fUG9O",
    "y": "LMHt1lT4ZdK3puWwrdrAUZBLazDbwwoZveFnlcYlL7PO62dDdHdo_KhYeUoPOHgk",
    "alg": "ECDH-ES+A256KW"
}'
```

Приклад відповіді

```json
{
    "refreshToken": "5aba78ac-8850-4619-8232-f62089cbcbb3",
    "authToken": "14a74387-9f20-4e73-a314-0d2ca80222b6",
    "deviceId": "1d9742cf-d392-4c2b-9982-4dc6ec2224b2",
    "serverPublic": {
        "kty": "EC",
        "crv": "P-384",
        "x": "BSWUuzrcIWk3GFUqD2ClMxVwycEWXoMnqJsDwOJNidTtfJJ0dn8h9m3Q8fRoxBaA",
        "y": "PnFAa3LNxJgiUYZXUx7-kr049B0IxOUXP2l8_Z7mEgUv9-xhVWuf0sJhiOn69VPe"
    },
    "tokenExpirationDateTime": "2023-03-18 12:34:52.0998 +0000"
}
```

_Refresh сесіі не передбаченний, для генераціі нового serverPublic необхідно виконати Запит створення технічної сесії повторно_&#x20;
