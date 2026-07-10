---
description: POST {{url}}/ecom/jws/scheduled_payments/payments/initial_subscription_v1
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
  tags:
    visible: true
  actions:
    visible: true
---

# Iнітний (перший) платіж

Це перший платіж, який підтверджує підписку клієнта. Він **обов'язково** проходить 3DS-аутентифікацію (підтвердження від власника картки).

**Підтримувані методи оплати:**

* 💳 **CARD** — за номером картки (автоматично створюється токен для наступних списань)
* 🔑 **TOKEN** — за існуючим токеном
* 🍏 **APPLE\_PAY** (encrypted / decrypted)
* 🤖 **GOOGLE\_PAY** (encrypted / decrypted)

**Що відбувається після успішного платежу:**

1. Зберігається **токен картки** клієнта для майбутніх автоматичних списань
2. Автоматично генерується **повний графік запланованих платежів**&#x20;
3. Мерчант отримує **callback** з результатом

#### Вхідні параметри

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Обовʼязковість</strong></td><td><strong>Приклад</strong></td></tr><tr><td>merchantRequestId</td><td>Id запиту мерчанта</td><td>uuid (36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>uuid(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>paymentMethodType</td><td>Ознака, що визначає тип платіжного методу, через який здійснюється Purchase.</td><td>enum</td><td>Так</td><td><ol start="1"><li>CARD - по номеру</li><li>TOKEN - по токену згенерованному в нашій системі</li><li>APPLE_PAY_ENCRYPTED</li><li>APPLE_PAY_DECRYPTED</li><li>GOOGLE_PAY_ENCRYPTED</li><li>GOOGLE_PAY_DECRYPTED</li></ol></td></tr><tr><td>encryptedCardNumber</td><td>Номер карти зашифрований в JWE за допомогою публічного платіжного ключа</td><td>string</td><td>Так, якщо paymentMethodType = CARD</td><td> </td></tr><tr><td>encryptedCardData</td><td>термін дії карти та cvv2 зашифровані в JWE. Перші 4 символи ExpDate, слідуючи 3 символи cvv</td><td>string</td><td>Так, якщо paymentMethodType = CARD</td><td>2503111 (розшифрований вигляд)</td></tr><tr><td>token</td><td>токен картки </td><td>string</td><td>Так, якщо paymentMethodType = TOKEN</td><td> </td></tr><tr><td>paymentToken</td><td>оплата по закриптованному токену aPay</td><td>object</td><td>Так, якщо paymentMethodType = APPLE_PAY_ENCRYPTED</td><td> </td></tr><tr><td>paymentDataEncrypted</td><td>оплата по розкриптованному токену aPay</td><td>object</td><td>Так, якщо paymentMethodType = APPLE_PAY_DECRYPTED або GOOGLE_PAY_DECRYPTED</td><td> </td></tr><tr><td>googlePayPaymentData</td><td>оплата по закриптованному токену gPay</td><td>object</td><td>Так, якщо paymentMethodType = GOOGLE_PAY_ENCRYPTED</td><td> </td></tr><tr><td>environment</td><td>середовище. По замовчуванню production</td><td>string</td><td>Так, GOOGLE_PAY_ENCRYPTED</td><td> TEST/PRODUCTION</td></tr><tr><td>orderId</td><td>id ордеру підписки</td><td>string</td><td>Так</td><td> </td></tr><tr><td>browserInfo</td><td>об’єкт за даними браузера</td><td>object</td><td>Так</td><td> </td></tr><tr><td>browserAcceptHeader</td><td>Http заголовок запиту</td><td>string</td><td>Так</td><td>text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9</td></tr><tr><td>browserUserAgent</td><td>програмний елемент браузера, що позначає систему, що користується нею</td><td>string</td><td>Так</td><td>Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like,Gecko)Chrome/87.0.4280.66 Safari/537.36</td></tr><tr><td>browserLanguage</td><td>мова браузера</td><td>string</td><td>Так</td><td>en-US,en</td></tr><tr><td>browserColorDepth</td><td>значення глибини кольору екрана у браузері</td><td>string</td><td>Так</td><td>24</td></tr><tr><td>browserScreenHeight</td><td>висота області перегляду вікна браузера</td><td>string</td><td>Так</td><td>800</td></tr><tr><td>browserScreenWidth</td><td>широта області перегляду вікна браузера</td><td>string</td><td>Так</td><td>1280</td></tr><tr><td>browserTZ</td><td>Timezone браузера</td><td>string</td><td>Так</td><td>-180</td></tr><tr><td>merchantComment</td><td>додатковий коментар мерчанта</td><td>string</td><td>Ні</td><td>null</td></tr><tr><td>desiredThreeDSMode</td><td>Ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string</td><td>Так</td><td><p>За замовчуванням SHOULD</p><p>Можливі значення:</p><ul><li>MUST - мерчант вимагає проведення платежу з 3DS</li><li>MUST_NOT - примусова операція без 3DS</li><li>SHOULD - якщо картка підтримує 3DS, то робимо перевірку</li></ul></td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string</td><td>Ні</td><td>За товар</td></tr><tr><td>resultRedirectUrl</td><td>Url для редиректа клієнта після проходження 3DS аутентифікації</td><td>string</td><td>Ні</td><td><a href="https://support.google.com/">https://support.google.com/</a></td></tr><tr><td>customerData</td><td> </td><td>object</td><td>Так</td><td> </td></tr><tr><td>customerData.senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>customerData.senderFirstName</td><td>пошта відправника</td><td>string (30)</td><td>Ні</td><td>Іваненко</td></tr><tr><td>customerData.senderLastName</td><td>прізвище відправника</td><td>string (30)</td><td>Ні</td><td>Іван</td></tr><tr><td>customerData.senderMiddleName</td><td>ім'я відправника</td><td>string (30)</td><td>Ні</td><td>Іванович</td></tr><tr><td>customerData.senderEmail</td><td>по-батькові відправника</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>customerData.senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>scustomerData.senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>customerData.senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>customerData.senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>customerData.senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>customerData.senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>customerData.senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>customerData.senderIp</td><td>IP адреса відправника</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>customerData.senderPhone</td><td>номер телефону відправника</td><td>string (50)</td><td>Ні</td><td>380630000000</td></tr><tr><td>customerData.senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>customerData.senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>customerData.senderZipCode</td><td>Індекс відправника</td><td>string (50)</td><td>Ні</td><td> 49000</td></tr></tbody></table>

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
