---
description: POST {{url}}/ecom/jws/scheduled_payments/payments/initial_subscription_v1
---

# Iнітний (перший) платіж

| **Параметр**                         | **Опис**                                                                                    | **Формат даних**                   | **Обовʼязковість**                                                             | **Приклад**                                                                                                                                                                                                                           |
| ------------------------------------ | ------------------------------------------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| merchantRequestId                    | Id запиту мерчанта                                                                          | uuid (36)                          | Так                                                                            | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                                                  |
| merchantId                           | Id мерчанту згенерований в Єкомі                                                            | uuid(36)                           | Так                                                                            | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                                                  |
| paymentMethodType                    | Ознака, що визначає тип платіжного методу, через який здійснюється Purchase.                | enum                               | Так                                                                            | <ol start="1"><li>CARD - по номеру</li><li>TOKEN - по токену згенерованному в нашій системі</li><li>APPLE_PAY_ENCRYPTED</li><li>APPLE_PAY_DECRYPTED</li><li>GOOGLE_PAY_ENCRYPTED</li><li>GOOGLE_PAY_DECRYPTED</li></ol>               |
| encryptedCardNumber                  | Номер карти зашифрований в JWE за допомогою публічного платіжного ключа                     | string                             | Так, якщо paymentMethodType = CARD                                             |                                                                                                                                                                                                                                       |
| encryptedCardData                    | термін дії карти та cvv2 зашифровані в JWE. Перші 4 символи ExpDate, слідуючи 3 символи cvv | string                             | Так, якщо paymentMethodType = CARD                                             | 2503111 (розшифрований вигляд)                                                                                                                                                                                                        |
| token                                | токен картки                                                                                | string                             | Так, якщо paymentMethodType = TOKEN                                            |                                                                                                                                                                                                                                       |
| paymentToken                         | оплата по закриптованному токену aPay                                                       | object                             | Так, якщо paymentMethodType = APPLE\_PAY\_ENCRYPTED                            |                                                                                                                                                                                                                                       |
| paymentDataEncrypted                 | оплата по розкриптованному токену aPay                                                      | object                             | Так, якщо paymentMethodType = APPLE\_PAY\_DECRYPTED або GOOGLE\_PAY\_DECRYPTED |                                                                                                                                                                                                                                       |
| googlePayPaymentData                 | оплата по закриптованному токену gPay                                                       | object                             | Так, якщо paymentMethodType = GOOGLE\_PAY\_ENCRYPTED                           |                                                                                                                                                                                                                                       |
| environment                          | середовище. По замовчуванню production                                                      | string                             | Так, GOOGLE\_PAY\_ENCRYPTED                                                    |  TEST/PRODUCTION                                                                                                                                                                                                                      |
| orderId                              | id ордеру підписки                                                                          | string                             | Так                                                                            |                                                                                                                                                                                                                                       |
| browserInfo                          | об’єкт за даними браузера                                                                   | object                             | Так                                                                            |                                                                                                                                                                                                                                       |
| browserAcceptHeader                  | Http заголовок запиту                                                                       | string                             | Так                                                                            | text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,\*/\*;q=0.8,application/signed-exchange;v=b3;q=0.9                                                                                             |
| browserUserAgent                     | програмний елемент браузера, що позначає систему, що користується нею                       | string                             | Так                                                                            | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36                                                                                                                     |
| browserLanguage                      | мова браузера                                                                               | string                             | Так                                                                            | en-US,en                                                                                                                                                                                                                              |
| browserColorDepth                    | значення глибини кольору екрана у браузері                                                  | string                             | Так                                                                            | 24                                                                                                                                                                                                                                    |
| browserScreenHeight                  | висота області перегляду вікна браузера                                                     | string                             | Так                                                                            | 800                                                                                                                                                                                                                                   |
| browserScreenWidth                   | широта області перегляду вікна браузера                                                     | string                             | Так                                                                            | 1280                                                                                                                                                                                                                                  |
| browserTZ                            | Timezone браузера                                                                           | string                             | Так                                                                            | -180                                                                                                                                                                                                                                  |
| merchantComment                      | додатковий коментар мерчанта                                                                | string                             | Ні                                                                             | null                                                                                                                                                                                                                                  |
| desiredThreeDSMode                   | Ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.                        | string                             | Так                                                                            | <p>За замовчуванням SHOULD</p><p>Можливі значення:</p><ul><li>MUST - мерчант вимагає проведення платежу з 3DS</li><li>MUST_NOT - примусова операція без 3DS</li><li>SHOULD - якщо картка підтримує 3DS, то робимо перевірку</li></ul> |
| date                                 | дата та час платежу                                                                         | string                             | Так                                                                            | \{{currentdateT\}}.00+00:00                                                                                                                                                                                                           |
| comment                              | додаткова опис операції яку заповнює клієнт мерчанта                                        | string                             | Ні                                                                             | ///5555.25412                                                                                                                                                                                                                         |
| purpose                              | призначення платежу яке заповнює мерчант                                                    | string                             | Ні                                                                             | За товар                                                                                                                                                                                                                              |
| resultRedirectUrl                    | Url для редиректа клієнта після проходження 3DS аутентифікації                              | string                             | Ні                                                                             | [https://support.google.com/](https://support.google.com/)                                                                                                                                                                            |
| customerData                         |                                                                                             | object                             | Так                                                                            |                                                                                                                                                                                                                                       |
| customerData.senderCustomerId        | Id клієнта відправника                                                                      | string (255)                       | Так                                                                            | 1258728c1                                                                                                                                                                                                                             |
| customerData.senderFirstName         | пошта відправника                                                                           | string (30)                        | Ні                                                                             | Іваненко                                                                                                                                                                                                                              |
| customerData.senderLastName          | прізвище відправника                                                                        | string (30)                        | Ні                                                                             | Іван                                                                                                                                                                                                                                  |
| customerData.senderMiddleName        | ім'я відправника                                                                            | string (30)                        | Ні                                                                             | Іванович                                                                                                                                                                                                                              |
| customerData.senderEmail             | по-батькові відправника                                                                     | string (256)                       | Ні                                                                             | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                                               |
| customerData.senderСountry           | країна відправника                                                                          | string (3) ISO 3166, 804 (Ukraine) | Ні                                                                             | 804                                                                                                                                                                                                                                   |
| scustomerData.senderRegion           | область відправника                                                                         | string (255)                       | Ні                                                                             | Київська                                                                                                                                                                                                                              |
| customerData.senderСity              | місто відправника                                                                           | string (25)                        | Ні                                                                             | Київ                                                                                                                                                                                                                                  |
| customerData.senderStreet            | вулиця відправника                                                                          | string (35)                        | Ні                                                                             | Січових стрільців                                                                                                                                                                                                                     |
| customerData.senderAdditionalAddress | додаткові дані адреси відправника (поверх, номер дому, квартира)                            | string (255)                       | Ні                                                                             | 23                                                                                                                                                                                                                                    |
| customerData.senderItn               | іпн відправника                                                                             | string (20)                        | Ні                                                                             | 123456789                                                                                                                                                                                                                             |
| customerData.senderPassport          | паспорт відправника                                                                         | string (255)                       | Ні                                                                             | АН123456                                                                                                                                                                                                                              |
| customerData.senderIp                | IP адреса відправника                                                                       | string (50)                        | Ні                                                                             | 123.12.12.12                                                                                                                                                                                                                          |
| customerData.senderPhone             | номер телефону відправника                                                                  | string (50)                        | Ні                                                                             | 380630000000                                                                                                                                                                                                                          |
| customerData.senderBirthday          | день народження відправника                                                                 | string (50)                        | Ні                                                                             | 31.12.2000                                                                                                                                                                                                                            |
| customerData.senderGender            | Гендер відправника                                                                          | string (50)                        | Ні                                                                             | Male/Female                                                                                                                                                                                                                           |
| customerData.senderZipCode           | Індекс відправника                                                                          | string (50)                        | Ні                                                                             |  49000                                                                                                                                                                                                                                |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**    | **Опис**                                                           | **Формат даних** | **Приклад**                                                                                                                                                                                            |
| --------------- | ------------------------------------------------------------------ | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| operationId     | Id операціі                                                        | string           | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId | Id операціі в системі Ecom                                         | string           | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| status          | статус операціі                                                    | string           | SUСCESS FAIL PENDING REQUIRED\_3DS                                                                                                                                                                     |
| redirect3dsUrl  | url для редиректа клієнта на сторінку емітента для проходження 3DS | string           | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |

#### Приклад запиту paymentMethodType CARD

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "resultRedirectUrl":"https://card.com/3ds-return?",
   "desiredThreeDSMode":"MUST",
   "clientComment":"MERCHANT_NAME=TOV",
   "comment":"testing Nick",
   "purpose":"Payment for food",
   "date":"{{currentdateT}}.00+00:00",
   "paymentMethodType":"CARD",
   "encryptedCardNumber":"{{encryptedPanT}}",
   "encryptedCardData":"{{encryptedDateAndSecurityT}}",
   "orderId":"{{hppOrderId}}",
   "paymentCurrencyCode":"980",
   "merchantComment":"Helllo World. Lets rock123",
   "paymentAmount":"100",
   "browserInfo":{
      "browserAcceptHeader":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "browserUserAgent":"Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/111.0.0.0+Safari/537.36",
      "browserLanguage":"ru-RU",
      "browserColorDepth":"24",
      "browserScreenHeight":"864",
      "browserScreenWidth":"1536",
      "browserTZ":"-180"
   },
   "customerData":{
      "senderCustomerId":"Nikos",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":"qtest@testor.com",
      "senderCountry":804,
      "senderRegion":"Kiyivska",
      "senderCity":"Kiyv",
      "senderStreet":"khreshatuk",
      "senderAdditionalAddress":"Ukraine, Lviv, Arsenalna st.",
      "senderItn":"3667709657",
      "senderPassport":"HE111999",
      "senderIp":"192.168.2.1",
      "senderPhone":"380931234567",
      "senderBirthday":"32.13.2050",
      "senderGender":"Male",
      "senderZipCode":"18900"
   }
}
```

#### Приклад запиту paymentMethodType TOKEN

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "resultRedirectUrl":"https://card.com/3ds-return?",
   "desiredThreeDSMode":"MUST",
   "purpose":"purpose=TOV",
   "comment":"comment",
   "merchantComment":"merchantComment",
   "date":"{{currentdateT}}.00+00:00",
   "paymentMethodType":"TOKEN",
   "token":"RrVmxPxfvZWEe_J5wMx6zHfZ",
   "orderId":"{{hppOrderId}}",
   "paymentCurrencyCode":"980",
   "paymentAmount":"20000",
   "browserInfo":{
      "browserAcceptHeader":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "browserUserAgent":"Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/111.0.0.0+Safari/537.36",
      "browserLanguage":"ru-RU",
      "browserColorDepth":"24",
      "browserScreenHeight":"864",
      "browserScreenWidth":"1536",
      "browserTZ":"-180"
   },
   "customerData":{
      "senderCustomerId":"tesChokan102726t",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":null,
      "senderCountry":null,
      "senderRegion":null,
      "senderCity":null,
      "senderStreet":null,
      "senderAdditionalAddress":null,
      "senderItn":"3667709657",
      "senderPassport":null,
      "senderIp":null,
      "senderPhone":null,
      "senderBirthday":null,
      "senderGender":null,
      "senderZipCode":null
   }
}
```

#### Приклад запиту paymentMethodType APPLE\_PAY\_ENCRYPTED

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "resultRedirectUrl":"https://card.cascad.com/3ds-return?pid=4f03b1cc-711b-4769-8db6-669c5a967d8c",
   "desiredThreeDSMode":"MUST",
   "purpose":"purpose=TOV",
   "comment":"comment",
   "merchantComment":"merchantComment",
   "date":"{{currentdateT}}.00+00:00",
   "paymentMethodType":"APPLE_PAY_ENCRYPTED",
   "paymentToken":{
      "transactionIdentifier":"9b537d0eb9d362cc4fad5747271bade00eb366c91ea17cabcd6d67c71e9c173e",
      "paymentData":{
         "data":"EXCr5+KMwshSGHK3oN5cGk/dUl3ejIrmRbFPfeHIqO8+vC9MWcHL7RuxnJEAWMIqQxFf3toQr5/VrJJXgM65/2C4sUsYwByGLFAlSbHm2/7FzZoH9g5Mg9Ntsn3J64FFiyFMfmpt6HWn3jAHQlBHE3zBWmEL5V5VYU4XzurT2JnOqf5dpBbGTk0U0uGAksDL0b0wcQE44X4qw37cC7tyq8mT0gevOEmODyrabeVqnUXULBabPWtgUxfp4u79yWl7tqpxTnaU/Z42/RYt71jS2OLKWFkLbf7muCE0HjnaPG6uleVCYYBKczQHbBmszinkdzSLq3is1n7e00bsr4+43/ZrQRNPFyak3bUIvtbzSMafKOK3YMSH6Rg+5qrjykrUXMFDVXnnyJe17ucAqQ==",
         "signature":"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",
         "header":{
            "publicKeyHash":"3RA+IEMm6t+ZfpjW09xfVXsjRVamcUTGwXdp181xWCYk=",
            "ephemeralPublicKey":"MFkwEwYHKo465zj0CAQYIKoZIzj0DAQcDQgAEYLT/oF7S9xkHoZVE0FAQF2rjczs/QNqqIOdjCiKbcKGtcm2Svn7fqztjOD5qvXXGfvSESzv8uY+sXar2NuFkEw==",
            "transactionId":"9b537d0eb9d362cc4fad747271bade00eb366c91ea17cabcd6d67c71e9c173e"
         },
         "version":"EC_v1"
      },
      "paymentMethod":{
         "displayName":"MasterCard 6702",
         "network":"MasterCard",
         "type":"credit"
      }
   },
   "orderId":"{{hppOrderId}}",
   "browserInfo":{
      "browserAcceptHeader":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "browserUserAgent":"Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/111.0.0.0+Safari/537.36",
      "browserLanguage":"ru-RU",
      "browserColorDepth":"24",
      "browserScreenHeight":"864",
      "browserScreenWidth":"1536",
      "browserTZ":"-180"
   },
   "customerData":{
      "senderCustomerId":"tesChokan102726t",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":null,
      "senderCountry":null,
      "senderRegion":null,
      "senderCity":null,
      "senderStreet":null,
      "senderAdditionalAddress":null,
      "senderItn":"3667709657",
      "senderPassport":null,
      "senderIp":null,
      "senderPhone":null,
      "senderBirthday":null,
      "senderGender":null,
      "senderZipCode":null
   }
}
```

#### Приклад запиту paymentMethodType APPLE\_PAY\_DECRYPTED

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "resultRedirectUrl":"https://card.com/3ds-return",
   "desiredThreeDSMode":"MUST_NOT",
   "purpose":"purpose=TOV",
   "comment":"comment",
   "merchantComment":"merchantComment",
   "date":"{{currentdateT}}.00+00:00",
   "paymentMethodType":"APPLE_PAY_DECRYPTED",
   "paymentDataEncrypted":"{{encryptedPaymentData}}",
   "orderId":"{{hppOrderId}}",
   "browserInfo":{
      "browserAcceptHeader":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "browserUserAgent":"Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/111.0.0.0+Safari/537.36",
      "browserLanguage":"ru-RU",
      "browserColorDepth":"24",
      "browserScreenHeight":"864",
      "browserScreenWidth":"1536",
      "browserTZ":"-180"
   },
   "customerData":{
      "senderCustomerId":"tesChokan102726t",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":null,
      "senderCountry":null,
      "senderRegion":null,
      "senderCity":null,
      "senderStreet":null,
      "senderAdditionalAddress":null,
      "senderItn":"3667709657",
      "senderPassport":null,
      "senderIp":null,
      "senderPhone":null,
      "senderBirthday":null,
      "senderGender":null,
      "senderZipCode":null
   }
}
```

#### Приклад запиту paymentMethodType GOOGLE\_PAY\_DECRYPTED

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "resultRedirectUrl":"https://card.com/3ds-return?",
   "desiredThreeDSMode":"MUST",
   "purpose":"purpose=TOV",
   "comment":"comment",
   "merchantComment":"merchantComment",
   "date":"{{currentdateT}}.00+00:00",
   "paymentMethodType":"GOOGLE_PAY_DECRYPTED",
   "paymentDataEncrypted":"{{encryptedPaymentData}}",
   "orderId":"{{hppOrderId}}",
   "browserInfo":{
      "browserAcceptHeader":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "browserUserAgent":"Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/111.0.0.0+Safari/537.36",
      "browserLanguage":"ru-RU",
      "browserColorDepth":"24",
      "browserScreenHeight":"864",
      "browserScreenWidth":"1536",
      "browserTZ":"-180"
   },
   "customerData":{
      "senderCustomerId":"tesChokan102726t",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":null,
      "senderCountry":null,
      "senderRegion":null,
      "senderCity":null,
      "senderStreet":null,
      "senderAdditionalAddress":null,
      "senderItn":"3667709657",
      "senderPassport":null,
      "senderIp":null,
      "senderPhone":null,
      "senderBirthday":null,
      "senderGender":null,
      "senderZipCode":null
   }
}
```

#### Приклад запиту paymentMethodType GOOGLE\_PAY\_ENCRYPTED

```json
{
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "resultRedirectUrl":"https://card.com/3ds-return",
   "desiredThreeDSMode":"MUST",
   "purpose":"purpose=TOV",
   "comment":"comment",
   "merchantComment":"merchantComment",
   "date":"{{currentdateT}}.00+00:00",
   "paymentMethodType":"GOOGLE_PAY_ENCRYPTED",
   "googlePayPaymentData":{
      "apiVersion":2,
      "apiVersionMinor":0,
      "paymentMethodData":{
         "description":"Test Card: Mastercard •••• 4444",
         "info":{
            "assuranceDetails":{
               "accountVerified":true,
               "cardHolderAuthenticated":false
            },
            "cardDetails":"4444",
            "cardFundingSource":"CREDIT",
            "cardNetwork":"MASTERCARD"
         },
         "tokenizationData":{
            "token":"{\"signature\":\"MEUCIQDSiLi99B8hu54wY2tWuGYCu+FUBmzrknzIuoDSGMTqjUgIgQJsvwZkwIPLrmX3IpGcO/yOs8zGrgHqukrzRA9fC/xU\\u003d\",\"intermediateSigningKey\":{\"signedKey\":\"{\\\"keyValue\\\":\\\"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAExu+AHD9JwNYEK0MGHg8GUAN2keEWqpOcI8cwgn4reEmSL6xzeTn42qxO7eD1SqtIg7qM+zMgwLbYec+is3ODGQ\\\\u003d\\\\u003d\\\",\\\"keyExpiration\\\":\\\"1779796382513\\\"}\",\"signatures\":[\"MEUCIF+2b5mEHN/POjs8vPzFHDs7j2R3rdJ4iLyaXtzxvzT/AiEAv7XoaGsJig2diGIcnf1uUnmOBQL2wKnti+9m8Lc/1/g\\u003d\"]},\"protocolVersion\":\"ECv2\",\"signedMessage\":\"{\\\"encryptedMessage\\\":\\\"2jbfBFihag5NGjxtguJ/GmmRDnDUHQCdqWV6Lipi0U4S18mm/54erZcgfu8JUu+F7Z/r6ZzbvqyAqRH1ObwjkZ+5zysR98K1dQU1E+Ij/tylaVcrrqR5El/xLjpyjtQdSrOmfyXNxH/ZcnOF/ag349ssMXmNsiZrphGo7tujpA2M9zEDesdKFlkLwnu5Wh0noiMfNXdetEKQR11T1i4CNQEoqJQNuFOzBHL18aZdmzC9+KybJNaAO8hLLo1wDBcGGPgeFjZ8pvt62sUpWsbaNTcHNtVQwJ1pwmkHsJrOzBUAnZZPuWsEoCUJciNHbMuU/1dNU/M5UAHs3HNIdCqui30WnXSMkn5GyzirfJFpO11RunKnmEFxXnHEBvWq9rRfdLakZU72XedNOZkSz6URtC01mm/3Qh6AgwRNxdmlob4LWb3LMnaITdfYBeOJRHqLaY9DVO4E7EGGtYVKX1UzVVTny3MsRfo55GB89GUmY0UvTF1bVvcwKowEjFBkWNhgZZyGsG6BcfgonhMYBlgVfaCAvs2yO5aqmRUmUbSE/dQbFejDt+85mSEwtT/hNN6QnxML2LqYn3WNSVlDxKgKJMRo9UCduyOR4niC5SWNK9xgIlC/XI+898g+6w\\\\u003d\\\\u003d\\\",\\\"ephemeralPublicKey\\\":\\\"BHo3YsVBgDU8ImSykinHdWa8epwjQaa0MXCbJngwDT03BFe/wjAB9iZyYAVpasd8MnTMWN2YLc0xEAu3qijZGbU\\\\u003d\\\",\\\"tag\\\":\\\"kB7S5cPOfR7zUlazdHOIsalRzumxm4KZDF/qZmS0dSY\\\\u003d\\\"}\"}",
            "type":"PAYMENT_GATEWAY"
         },
         "type":"CARD"
      },
      "merchantInfo":{
         "merchantId":"Iltdpa99j20LCOZ2oU_Hw6SJ",
         "gateway":"timeproject"
      }
   },
   "environment":"PROD",
   "orderId":"{{hppOrderId}}",
   "browserInfo":{
      "browserAcceptHeader":"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7",
      "browserUserAgent":"Mozilla/5.0+(Windows+NT+10.0;+Win64;+x64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/111.0.0.0+Safari/537.36",
      "browserLanguage":"ru-RU",
      "browserColorDepth":"24",
      "browserScreenHeight":"864",
      "browserScreenWidth":"1536",
      "browserTZ":"-180"
   },
   "customerData":{
      "senderCustomerId":"tesChokan102726t",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":null,
      "senderCountry":null,
      "senderRegion":null,
      "senderCity":null,
      "senderStreet":null,
      "senderAdditionalAddress":null,
      "senderItn":"3667709657",
      "senderPassport":null,
      "senderIp":null,
      "senderPhone":null,
      "senderBirthday":null,
      "senderGender":null,
      "senderZipCode":null
   }
}
```

#### Приклад відповіді&#x20;

```json
{
   "operationId":"1783609267213ROxtSXOXgFm",
   "ecomOperationId":"2b8c65e4-edef-4d62-becc-8fe8c166b0cc",
   "status":"REQUIRED_3DS",
   "redirect3dsUrl":"https://defe-api.develop.bankalliance.ua/threeDS/getRedirectHtml/1783610757877XqGmQPB9P79"
}      
```
