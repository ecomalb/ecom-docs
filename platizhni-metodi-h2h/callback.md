---
description: >-
  Для відправки Callback буде виконаний Post запит на notificationUrl який був
  вказаний в запиті на проведення платежу. Шифрування Callback регулюється
  параметром notificationEncryption
---

# Callback

* Для платежів типу **A2A** (переказ з рахунку на рахунок) додатково передаються параметри з інформацією про відправника платежу в межах **SEP**. Ці параметри стосуються тільки платежів A2A.
* Якщо статус отримання Callback не 200 ОК, відбувається перевідправка Callback через 5 сек, потім через 30 сек, потім через 5 хв, потім через 30 хв, через 1 годину
* Якщо статус отримання Callback не 200 ОК для 1-го разу, а для 2-го разу 200 ОК, то перевідправка Callback більше не виконується&#x20;

#### **Вхідні параметри**

| **Параметр**                           | **Опис**                                                                    | **Формат даних** | **Приклад**                             |
| -------------------------------------- | --------------------------------------------------------------------------- | ---------------- | --------------------------------------- |
| `type`                                 | Тип транзакції                                                              | string / enum    | `PURCHASE`                              |
| `rrn`                                  | RRN — номер транзакції в МПС                                                | string           | `000000000001`                          |
| `purpose`                              | Призначення платежу                                                         | string           | `Тестове призначення платежу`           |
| `comment`                              | Коментар до транзакції                                                      | string           | `Тестовий коментар`                     |
| `coinAmount`                           | Сума платежу в копійках                                                     | int              | `50000`                                 |
| `merchantId`                           | Ідентифікатор мерчанта                                                      | string (UUID)    | `a1111111-1111-4111-8111-111111111111`  |
| `operationId`                          | Ідентифікатор транзакції в системі                                          | string           | `TEST_OPERATION_001`                    |
| `ecomOperationId`                      | Ідентифікатор транзакції в системі Ecom                                     | string (UUID)    | `b2222222-2222-4222-8222-222222222222`  |
| `merchantName`                         | Найменування торговця                                                       | string           | `TEST_MERCHANT`                         |
| `approvalCode`                         | Код авторизації транзакції                                                  | string           | `000000`                                |
| `status`                               | Статус транзакції                                                           | string / enum    | `SUCCESS`                               |
| `transactionType`                      | Числовий код типу транзакції                                                | number           | `35`                                    |
| `merchantRequestId`                    | Ідентифікатор запиту мерчанта                                               | string           | `c3333333-3333-4333-8333-333333333333`  |
| `transactionCurrency`                  | Код валюти за ISO 4217                                                      | string           | `980`                                   |
| `merchantCommission`                   | Комісія мерчанта                                                            | int              | `600`                                   |
| `commissionAmount`                     | Сума комісії за операцією                                                   | number           | `0`                                     |
| `creationDateTime`                     | Дата й час створення транзакції                                             | string           | `2026.10.26 12:15:40.478`               |
| `modificationDateTime`                 | Дата й час останньої зміни транзакції                                       | string           | `2026.10.26 12:16:43.132`               |
| `processingDateTime`                   | Дата й час обробки транзакції                                               | string           | `2026.10.26 12:15:40.000`               |
| `transactionResponseInfo`              | Об’єкт із результатом обробки транзакції                                    | object           | `{}`                                    |
| `transactionResponseInfo.actionCode`   | Код результату обробки від процесингу                                       | string           | `"0"`                                   |
| `transactionResponseInfo.responseCode` | Код відповіді процесингу                                                    | string           | `"00"`                                  |
| `transactionResponseInfo.description`  | Опис результату обробки                                                     | string           | `approved`                              |
| `bankCode`                             | Код банку, пов’язаного з транзакцією                                        | string           | `BANK_ALLIANCE`                         |
| `paymentSystem`                        | Назва платіжної системи                                                     | string           | `MasterCard`                            |
| `productType`                          | Тип продукту термінала                                                      | string           | `PURCHASE`                              |
| `notificationUrl`                      | URL, на який надсилається callback                                          | string (URL)     | `https://example.com/test-callback`     |
| `paymentServiceType`                   | Тип платіжного сервісу                                                      | string / enum    | `CARD`                                  |
| `notificationEncryption`               | Ознака шифрування даних callback                                            | boolean          | `false`                                 |
| `notificationSignature`                | Ознака підпису callback                                                     | boolean          | `true`                                  |
| `receiptUrl`                           | URL для отримання або перегляду чека                                        | string (URL)     | `https://example.com/test-receipt`      |
| `cardNumberMask`                       | Маскований номер картки                                                     | string           | `00000000••••0000`                      |
| `externalCardToken`                    | Ідентифікатор токена картки                                                 | string           | `TEST_TOKEN_001`                        |
| `desiredThreeDSMode`                   | Бажаний мерчантом режим застосування 3DS                                    | string / enum    | `MUST`                                  |
| `threeDSMode`                          | Режим застосування 3DS для транзакції                                       | string / enum    | `MUST_NOT`                              |
| `statusThreeDs`                        | Результат проходження 3DS: `Y` — успішно, `N` — неуспішно                   | string           | `Y`                                     |
| `threeDSServerTransId`                 | Ідентифікатор транзакції на стороні 3DS Server                              | string (UUID)    | `f6666666-6666-4666-8666-666666666666`  |
| `acsTransId`                           | Ідентифікатор транзакції в ACS                                              | string (UUID)    | `d4444444-4444-4444-8444-444444444444`  |
| `dsTransId`                            | Ідентифікатор транзакції Directory Server                                   | string (UUID)    | `e5555555-5555-4555-8555-555555555555`  |
| `eci`                                  | Electronic Commerce Indicator — індикатор рівня безпеки транзакції          | string           | `02`                                    |
| `hppOrderId`                           | Ідентифікатор HPP-ордера, у межах якого створено платіж                     | string           | `TEST_ORDER_001`                        |
| `processingMerchantId`                 | Ідентифікатор мерчанта в процесинговому центрі                              | string           | `TEST000001`                            |
| `processingTerminalId`                 | Ідентифікатор термінала в процесинговому центрі                             | string           | `TEST0001`                              |
| `creatorSystem`                        | Система, у якій створено платіж                                             | string / enum    | `H2H`                                   |
| `redirect3dsUrl`                       | URL перенаправлення клієнта на сторінку емітента для проходження 3DS        | string (URL)     | `https://example.com/test-3ds-redirect` |
| `txnType`                              | Підтип транзакції                                                           | string / enum    | `NONCVV`                                |
| `tnxType`                              | Підтип транзакції; альтернативне поле, яке також зустрічається у відповідях | string / enum    | `NONCVV`                                |
| `balanceAmountAfter`                   | Значення балансу після операції                                             | number           | `1000000`                               |
| `merchantComment`                      | Коментар мерчанта до транзакції                                             | string           | `TEST_REQUEST_001`                      |
| `merchantBusinessCode`                 | Код категорії діяльності мерчанта (MCC)                                     | string           | `7995`                                  |
| `statusUrl`                            | URL для отримання статусу ордера, якщо передбачений контрактом              | string / null    | `null`                                  |
| `expiredOrderDate`                     | Дата й час закінчення строку дії ордера                                     | string           | `2026-10-27 10:59:43.100+02:00`         |
| `hppPayType`                           | Тип платежу HPP                                                             | string / enum    | `A2A`                                   |
| `hppDirectType`                        | Тип переходу або відкриття платіжної сторінки HPP                           | string / enum    | `BANK_LINK`                             |
| `tryMode`                              | Режим виконання спроб оплати                                                | string / enum    | `ONE_TRY`                               |
| `repeatedPayment`                      | Ознака повторного A2A-платежу                                               | boolean          | `false`                                 |
| `senderCustomerId`                     | Ідентифікатор клієнта-відправника                                           | string           | `TEST_CUSTOMER_001`                     |
| `senderFirstName`                      | Ім’я відправника                                                            | string           | `Іван`                                  |
| `senderLastName`                       | Прізвище відправника                                                        | string           | `Іванов`                                |
| `senderMiddleName`                     | По батькові відправника                                                     | string           | `Іванович`                              |
| `senderEmail`                          | Електронна пошта відправника                                                | string           | `test.sender@example.com`               |
| `senderCountry`                        | Країна відправника                                                          | string           | `Україна`                               |
| `senderRegion`                         | Область або регіон відправника                                              | string           | `Тестова область`                       |
| `senderCity`                           | Місто відправника                                                           | string           | `Тестове місто`                         |
| `senderStreet`                         | Вулиця відправника                                                          | string           | `Тестова вулиця`                        |
| `senderAdditionalAddress`              | Додаткова адресна інформація відправника                                    | string           | `Будинок 1, кв. 2`                      |
| `senderItn`                            | ІПН відправника                                                             | string           | `0000000000`                            |
| `senderPassport`                       | Номер паспорта або іншого документа відправника                             | string           | `ТЕ000001`                              |
| `senderIp`                             | IPv4- або IPv6-адреса відправника                                           | string           | `192.0.2.10`                            |
| `senderPhone`                          | Номер телефону відправника                                                  | string           | `380000000000`                          |
| `senderBirthday`                       | Дата народження відправника                                                 | string           | `01.01.1990`                            |
| `senderGender`                         | Гендер відправника                                                          | string           | `M`                                     |
| `senderZipCode`                        | Поштовий індекс відправника                                                 | string           | `00000`                                 |
| `senderBankCode`                       | Код банку відправника                                                       | string           | `BANK_ALLIANCE`                         |
| `senderPaymentSystem`                  | Платіжна система картки відправника                                         | string           | `MasterCard`                            |
| `senderCardNumberMask`                 | Маскований номер картки відправника                                         | string           | `00000000••••0000`                      |
| `senderAccount`                        | Рахунок відправника                                                         | string           | `UA000000000000000000000000001`         |
| `recipientCustomerId`                  | Ідентифікатор клієнта-отримувача                                            | string           | `TEST_CUSTOMER_002`                     |
| `recipientFirstName`                   | Ім’я отримувача                                                             | string           | `Олена`                                 |
| `recipientLastName`                    | Прізвище отримувача                                                         | string           | `Петренко`                              |
| `recipientMiddleName`                  | По батькові отримувача                                                      | string           | `Іванівна`                              |
| `recipientEmail`                       | Електронна пошта отримувача                                                 | string           | `test.recipient@example.com`            |
| `recipientCountry`                     | Країна отримувача                                                           | string           | `Україна`                               |
| `recipientRegion`                      | Область або регіон отримувача                                               | string           | `Тестова область`                       |
| `recipientCity`                        | Місто отримувача                                                            | string           | `Тестове місто`                         |
| `recipientStreet`                      | Вулиця отримувача                                                           | string           | `Тестова вулиця`                        |
| `recipientAdditionalAddress`           | Додаткова адресна інформація отримувача                                     | string           | `Будинок 2, кв. 3`                      |
| `recipientItn`                         | ІПН отримувача                                                              | string           | `0000000000`                            |
| `recipientPassport`                    | Номер паспорта або іншого документа отримувача                              | string           | `ТЕ000002`                              |
| `recipientIp`                          | IPv4- або IPv6-адреса отримувача                                            | string           | `192.0.2.20`                            |
| `recipientPhone`                       | Номер телефону отримувача                                                   | string           | `380000000001`                          |
| `recipientBirthday`                    | Дата народження отримувача                                                  | string           | `02.02.1990`                            |
| `recipientGender`                      | Гендер отримувача                                                           | string           | `F`                                     |
| `recipientZipCode`                     | Поштовий індекс отримувача                                                  | string           | `00000`                                 |
| `recipientBankCode`                    | Код банку отримувача                                                        | string           | `BANK_ALLIANCE`                         |
| `recipientPaymentSystem`               | Платіжна система картки отримувача                                          | string           | `MasterCard`                            |
| `recipientCardNumberMask`              | Маскований номер картки отримувача                                          | string           | `00000000••••0000`                      |
| `recipientAccount`                     | Рахунок отримувача                                                          | string           | `UA000000000000000000000000002`         |
| `originalOperationId`                  | Ідентифікатор оригінальної операції                                         | string           | `TEST_ORIGINAL_OPERATION_001`           |
| `originalCoinAmount`                   | Сума оригінального платежу в копійках                                       | int              | `10000`                                 |
| `originalEcomOperationId`              | Ідентифікатор оригінальної операції в системі Ecom                          | string (UUID)    | `d4444444-4444-4444-8444-444444444444`  |
| `rrnOriginal`                          | RRN оригінальної транзакції в МПС                                           | string           | `000000000003`                          |
| `sepSenderFirstName`                   | ПІБ відправника в контексті SEP-переказу                                    | string           | `Тестовий Іван Іванович`                |
| `sepSenderItn`                         | ІПН відправника в контексті SEP-переказу                                    | string           | `0000000000`                            |
| `sepSenderAccount`                     | Рахунок відправника в контексті SEP-переказу                                | string           | `UA000000000000000000000000003`         |
| `sepSenderBankCode`                    | Код банку відправника в контексті SEP-переказу                              | string           | `BANK_ALLIANCE`                         |

#### Приклад тіла запиту PURCHASE&#x20;

```json
{
  "type": "PURCHASE",
  "rrn": "000000000002",
  "purpose": "TEST_PAYMENT_002",
  "coinAmount": 10000,
  "merchantId": "a1111111-1111-4111-8111-111111111111",
  "operationId": "TEST_OPERATION_002",
  "ecomOperationId": "b2222222-2222-4222-8222-222222222222",
  "merchantName": "test-merchant.example",
  "approvalCode": "000000",
  "status": "SUCCESS",
  "transactionType": 35,
  "merchantRequestId": "c3333333-3333-4333-8333-333333333333",
  "transactionCurrency": "980",
  "creationDateTime": "2026.10.26 12:15:40.478",
  "modificationDateTime": "2026.10.26 12:16:43.132",
  "processingDateTime": "2026.10.26 12:15:40.000",
  "transactionResponseInfo": {
    "actionCode": "0",
    "responseCode": "00",
    "description": "approved"
  },
  "bankCode": "BANK_ALLIANCE",
  "paymentSystem": "MasterCard",
  "productType": "PURCHASE",
  "notificationUrl": "https://example.com/test-callback",
  "paymentServiceType": "CARD",
  "notificationEncryption": false,
  "notificationSignature": true,
  "processingTerminalId": "TEST0001",
  "processingMerchantId": "TEST000001",
  "creatorSystem": "H2H",
  "cardNumberMask": "00000000••••0000",
  "desiredThreeDSMode": "MUST_NOT",
  "threeDSMode": "MUST_NOT",
  "tnxType": "NONCVV",
  "txnType": "NONCVV",
  "senderCustomerId": "TEST_CUSTOMER_002",
  "senderItn": "0000000000",
  "senderPaymentSystem": "MasterCard",
  "senderCardNumberMask": "00000000••••0000",
  "senderBankCode": "BANK_ALLIANCE",
  "receiptUrl": "https://example.com/test-receipt"
}
```

#### Приклад тіла запиту REFUND&#x20;

```json
{
  "type": "REFUND",
  "rrn": "000000000003",
  "coinAmount": 10000,
  "merchantId": "a1111111-1111-4111-8111-111111111111",
  "operationId": "TEST_REFUND_001",
  "ecomOperationId": "b2222222-2222-4222-8222-222222222222",
  "merchantName": "TEST_MERCHANT",
  "approvalCode": "000000",
  "status": "SUCCESS",
  "transactionType": 76,
  "merchantRequestId": "c3333333-3333-4333-8333-333333333333",
  "transactionCurrency": "980",
  "creationDateTime": "2026.10.26 11:57:12.867",
  "modificationDateTime": "2026.10.26 11:58:15.896",
  "processingDateTime": "2026.10.26 11:57:12.000",
  "transactionResponseInfo": {
    "actionCode": "0",
    "responseCode": "00"
  },
  "bankCode": "AT_KB_PrivatBank",
  "paymentSystem": "MasterCard",
  "productType": "PURCHASE",
  "notificationUrl": "https://example.com/test-refund-callback",
  "notificationEncryption": false,
  "notificationSignature": true,
  "processingTerminalId": "TEST0001",
  "processingMerchantId": "TEST000001",
  "creatorSystem": "H2H",
  "merchantComment": "TEST_COMMENT_001",
  "rrnOriginal": "000000000003",
  "originalOperationId": "TEST_ORIGINAL_OPERATION_001",
  "cardNumberMask": "00000000••••0000",
  "originalEcomOperationId": "d4444444-4444-4444-8444-444444444444"
}
```

#### Приклад тіла запиту ACCOUNT\_2\_ACCOUNT

```json
{
  "type": "ACCOUNT_2_ACCOUNT",
  "purpose": "Тест",
  "coinAmount": 100,
  "merchantId": "b2222222-2222-4222-8222-222222222222",
  "operationId": "TEST_OPERATION_001",
  "ecomOperationId": "d4444444-4444-4444-8444-444444444444",
  "merchantName": "Тестовий Мерчант",
  "status": "SUCCESS",
  "transactionType": 54,
  "transactionCurrency": "980",
  "creationDateTime": "2026.10.26 11:01:01.324",
  "modificationDateTime": "2026.10.26 11:01:01.324",
  "transactionResponseInfo": {},
  "bankCode": "AT_UNIVERSAL_BANK",
  "paymentServiceType": "ACCOUNT",
  "notificationEncryption": false,
  "notificationSignature": false,
  "hppOrderId": "TEST_ORDER_001",
  "creatorSystem": "HPP",
  "merchantComment": "Тестова оплата рахунку №TEST-001 за послугою на https://example.com, акаунт ID TEST_ACCOUNT, ІПН 0000000000, Тестовий Іван Іванович",
  "commissionAmount": 0,
  "senderCountry": "804",
  "senderCity": "Тестове місто",
  "senderStreet": "Тестова вулиця, 1",
  "senderAccount": "UA000000000000000000000000001",
  "senderFirstName": "Іван",
  "senderLastName": "Іванов",
  "senderGender": "Male",
  "senderCustomerId": "TEST_CUSTOMER_001",
  "senderMiddleName": "Іванович",
  "senderEmail": "test.sender@example.com",
  "senderRegion": "Тестова область",
  "senderAdditionalAddress": "Тестова адреса",
  "senderItn": "0000000000",
  "senderPassport": "ТЕ000001",
  "senderPhone": "380000000000",
  "senderBirthday": "01.01.1990",
  "senderZipCode": "00000",
  "senderBankCode": "AT_UNIVERSAL_BANK",
  "recipientAccount": "UA000000000000000000000000002",
  "recipientFirstName": "Петренко Олена",
  "recipientItn": "0000000000",
  "recipientBankCode": "BANK_ALLIANCE",
  "repeatedPayment": false,
  "sepSenderFirstName": "Тестовий Петро Петрович",
  "sepSenderItn": "0000000000",
  "sepSenderAccount": "UA000000000000000000000000003",
  "sepSenderBankCode": "AT_UNIVERSAL_BANK"
}
```

#### Приклад тіла запиту ACCOUNT\_2\_CARD

```json
{
  "type": "ACCOUNT_2_CARD",
  "rrn": "000000000001",
  "purpose": "Тестове повернення коштів",
  "coinAmount": 150000,
  "merchantId": "a1111111-1111-4111-8111-111111111111",
  "operationId": "TEST_OPERATION_001",
  "ecomOperationId": "b2222222-2222-4222-8222-222222222222",
  "merchantName": "TEST_MERCHANT",
  "approvalCode": "000000",
  "status": "SUCCESS",
  "transactionType": 46,
  "merchantRequestId": "TEST_REQUEST_001",
  "transactionCurrency": "980",
  "merchantCommission": 600,
  "creationDateTime": "2026.10.26 12:09:38.821",
  "modificationDateTime": "2026.10.26 12:10:39.385",
  "processingDateTime": "2026.10.26 12:09:37.000",
  "transactionResponseInfo": {
    "actionCode": "0",
    "responseCode": "00",
    "description": "approved"
  },
  "bankCode": "AT_OSHADBANK",
  "paymentSystem": "MasterCard",
  "productType": "A2C",
  "notificationUrl": "https://example.com/test-callback",
  "paymentServiceType": "CARD",
  "notificationEncryption": false,
  "notificationSignature": false,
  "processingTerminalId": "TEST0001",
  "processingMerchantId": "TEST000001",
  "creatorSystem": "H2H",
  "balanceAmountAfter": 1000000,
  "merchantComment": "TEST_REQUEST_001",
  "merchantBusinessCode": "7995",
  "recipientBankCode": "AT_OSHADBANK",
  "senderAccount": "0000000000000000",
  "recipientCardNumberMask": "00000000••••0000",
  "cardNumberMask": "00000000••••0000",
  "recipientCustomerId": "TEST_CUSTOMER_001",
  "recipientFirstName": "Тест",
  "recipientLastName": "Тестов",
  "recipientMiddleName": "Тестович",
  "recipientItn": "0000000000",
  "recipientPassport": "ТЕ000001",
  "recipientPhone": "380000000000",
  "recipientBirthday": "01.01.1990",
  "recipientPaymentSystem": "MasterCard"
}
```

#### Приклад відповіді&#x20;

```http
HTTP 200 OK
```
