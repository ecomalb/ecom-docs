---
description: POST {{url}}/ecom/jws/scheduled_payments/subscription-orders/create_v1
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

# Створити підписку для клієнта

**Підписка** — це зв'язка між вашим планом та конкретним клієнтом (пейєром). Один план може мати багато підписок — по одному на кожного підписника.

**Як працює:**

1. Ви викликаєте API створення підписки
2. Система перевіряє, що план в статусі `ACTIVE`
3. Підписка отримує статус **PENDING** і залишається в ньому до завершення всіх платежів або скасування

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр**                         | **Опис**                                                               | **Формат даних**                   | **Обовʼязковість**                                           | **Приклад**                                                                 |
| ------------------------------------ | ---------------------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------- |
| planId                               | Id плану до якого необхідно необхідно створити ордер                   |  string(36)                        | Так                                                          |                                                                             |
| merchantId                           | ид мерчанта                                                            | string(36)                         | Так                                                          | 137d9304-0368-11ed-b939-0242ac120002                                        |
| purpose                              | Призначення платежу                                                    | string (255)                       | Ні                                                           | purpose                                                                     |
| notificationUrl                      | куда отправлять колбек                                                 |  string (255)                      | Ні                                                           | [https://example.com/notify](https://example.com/notify)                    |
| notificationEncryption               | ознака криптування данних CallBack                                     | Boolean                            | Ні                                                           | true/false                                                                  |
| merchantComment                      | додаткова інформація\коментар мерчанта по замовленню                   | <p>string(255)</p><p> </p>         | Ні                                                           | merchantComment                                                             |
| merchantRequestId                    | Унікальний ID покупки у Вашому магазині.                               | string (50)                        | Так                                                          | 137d9304-0368-11ed-b939-0242ac120002                                        |
| statusPageType                       | сторінка статусу                                                       | string                             | Так, якщо directType REDIRECT                                | statusTimerPage, statusRedirectMerchantPage, statusPage                     |
| successUrl                           | url, для редіректу на сайт мерчанту при успішному статусі              | <p>string (1000)<br></p>           | Так, якщо directType REDIRECT                                | [https://example.com/success](https://example.com/success)                  |
| failUrl                              | <p>url, для редіректу на сайт мерчанту при неуспішному статусі<br></p> | string (1000)                      | Так, якщо directType REDIRECT                                | [https://example.com/fail](https://example.com/fail)                        |
| hppPaymentMethods                    |  Параметр в якому передаються способи оплати                           | string                             | Так якщо directType not null                                 | <ul><li>CARD,</li><li>APPLE_PAY,</li><li>GOOGLE_PAY</li><li>TOKEN</li></ul> |
| directType                           | тип ордера                                                             | string                             | Так, якщо необхідно отримати redirectUrl для переходу на HPP | REDIRECT                                                                    |
| customerData                         |                                                                        | object                             | Так                                                          |                                                                             |
| customerData.senderCustomerId        | Id клієнта відправника                                                 | string (255)                       | Так                                                          | 1258728c1                                                                   |
| customerData.senderFirstName         | пошта відправника                                                      | string (30)                        | Ні                                                           | Іваненко                                                                    |
| customerData.senderLastName          | прізвище відправника                                                   | string (30)                        | Ні                                                           | Іван                                                                        |
| customerData.senderMiddleName        | ім'я відправника                                                       | string (30)                        | Ні                                                           | Іванович                                                                    |
| customerData.senderEmail             | по-батькові відправника                                                | string (256)                       | Ні                                                           | [mail@gmail.com](mailto:mail@gmail.com)                                     |
| customerData.senderСountry           | країна відправника                                                     | string (3) ISO 3166, 804 (Ukraine) | Ні                                                           | 804                                                                         |
| scustomerData.senderRegion           | область відправника                                                    | string (255)                       | Ні                                                           | Київська                                                                    |
| customerData.senderСity              | місто відправника                                                      | string (25)                        | Ні                                                           | Київ                                                                        |
| customerData.senderStreet            | вулиця відправника                                                     | string (35)                        | Ні                                                           | Січових стрільців                                                           |
| customerData.senderAdditionalAddress | додаткові дані адреси відправника (поверх, номер дому, квартира)       | string (255)                       | Ні                                                           | 23                                                                          |
| customerData.senderItn               | іпн відправника                                                        | string (20)                        | Ні                                                           | 123456789                                                                   |
| customerData.senderPassport          | паспорт відправника                                                    | string (255)                       | Ні                                                           | АН123456                                                                    |
| customerData.senderIp                | IP адреса відправника                                                  | string (50)                        | Ні                                                           | 123.12.12.12                                                                |
| customerData.senderPhone             | номер телефону відправника                                             | string (50)                        | Ні                                                           | 380630000000                                                                |
| customerData.senderBirthday          | день народження відправника                                            | string (50)                        | Ні                                                           | 31.12.2000                                                                  |
| customerData.senderGender            | Гендер відправника                                                     | string (50)                        | Ні                                                           | Male/Female                                                                 |
| customerData.senderZipCode           | Індекс відправника                                                     | string (50)                        | Ні                                                           |  49000                                                                      |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**      | **Опис**                          | **Формат даних** | **Приклад**                                                                                                                                                                               |
| ----------------- | --------------------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| hppOrderId        | Id підписки                       | string           | 1697008393082nW0c1jr6KVv                                                                                                                                                                  |
| merchantRequestId | ID операції в системі Мерчанта    | uuid             | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                      |
| orderStatus       | статус підписки                   | string           | PENDING                                                                                                                                                                                   |
| merchantId        | ід мерчанту                       | uuid             | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                      |
| redirectUrl       | Url для редіректу на hpp сторіни  | string           | <p><a href="http://pgi-ecom-polcom.develop.bankalliance.ua/?hpp_id=1725536712817G6AXGJ4evXJ"><br>http://pgi-ecom-polcom.develop.bankalliance.ua//?hpp_id=1725536712817G6AXGJ4evXJ</a></p> |
| createdAt         | Дата створення підписки           | string           | 2024-09-05 18:35:18.210+03:00                                                                                                                                                             |

#### Приклад запиту&#x20;

```json
{
  "planId": "{{planId}}",
  "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
  "merchantRequestId": "{{requestUUIDT}}",
  "purpose": "Payment for food",
  "notificationUrl": "https://webhook.site/6f07f573-c4f3-453c-83e3-d1c5993eb57d",
  "notificationEncryption": false,
  "merchantComment": "erdshjtpasdfasfsadfs",
  "statusPageType": "statusPage",
  "successUrl": "",
  "failUrl": "statusPage",
  "hppPaymentMethods": [
    "CARD",
    "APPLE_PAY",
    "GOOGLE_PAY"
  ],
  "directType": "REDIRECT",
  "customerData": {
    "senderCustomerId": "Nikos",
    "senderFirstName": "Богдан",
    "senderLastName": "Карпусь",
    "senderMiddleName": "Олександрович",
    "senderEmail": "qtest@testor.com",
    "senderCountry": 804,
    "senderRegion": "Kiyivska",
    "senderCity": "Kiyv",
    "senderStreet": "khreshatuk",
    "senderAdditionalAddress": "Ukraine, Lviv, Arsenalna st.",
    "senderItn": "3667709657",
    "senderPassport": "HE111999",
    "senderIp": "192.168.2.1",
    "senderPhone": "380931234567",
    "senderBirthday": "32.13.2050",
    "senderGender": "Male",
    "senderZipCode": "18900"
  }
}
```

#### Приклад відповіді&#x20;

```json
{
    "hppOrderId": "1783608520205P81ch623POH",
    "merchantRequestId": "64fe98ab-9731-48aa-b855-78c28e797aef",
    "orderStatus": "PENDING",
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "redirectUrl": "http://pgi-ecom-polcom.develop.bankalliance.ua//?hpp_id=1725536712817G6AXGJ4evXJ",
    "createdAt": "2026-07-09 17:48:40.02+03:00"
}
```
