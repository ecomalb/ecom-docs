# GooglePay™ decrypted

GooglePay™ API

## Для мерчанта:

#### 1.Налаштовувати GooglePay™ до веб-сайту, по інструкціям, розміщених за посиланнями:

Документація: [https://developers.google.com/pay/api/web\
](https://developers.google.com/pay/api/web)Вимоги з брендування: [https://developers.google.com/pay/api/web/guides/brand-guidelines](https://developers.google.com/pay/api/web/guides/brand-guidelines)

#### 2.При оплаті клієнтом послуги, розшифрувати об'єкт [CARD](https://developers.google.com/pay/api/web/guides/resources/payment-data-cryptography?hl=ru#card) за допомогою [PublicKey](https://developers.google.com/pay/api/web/guides/resources/payment-data-cryptography?hl=ru#step-two) та [PrivateKey](https://developers.google.com/pay/api/web/guides/resources/payment-data-cryptography?hl=ru#step-three)

Приклад картки:

```json
{
  "paymentMethod": "CARD",
  "paymentMethodDetails": {
    "authMethod": "PAN_ONLY",
    "pan": "1111222233334444",
    "expirationMonth": 10,
    "expirationYear": 2025
  },
  "gatewayMerchantId": "some-merchant-id",
  "messageId": "some-message-id",
  "messageExpiration": "1759309000000"
}
Приклад криптованого PAN:
{
  "paymentMethod": "CARD",
  "paymentMethodDetails": {
    "authMethod": "CRYPTOGRAM_3DS",
    "pan": "1111222233334444",
    "expirationMonth": 10,
    "expirationYear": 2025,
    "cryptogram": "AAAAAA...",
    "eciIndicator": "5"
   
  },
 
  "messageId": "some-message-id",
  "messageExpiration": "1759309000000"
}
```

#### 3.Об’єкт paymentData який описаний в пункті 2, необхідно закриптувати платіжним ключем
