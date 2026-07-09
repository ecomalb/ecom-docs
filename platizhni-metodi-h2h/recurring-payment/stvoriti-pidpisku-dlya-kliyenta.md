---
description: POST {{url}}/ecom/jws/scheduled_payments/subscription-orders/create_v1
---

# Створити підписку для клієнта

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр**           | **Опис**                                             | **Формат даних**           | **Обовʼязковість** | **Приклад**                                              |
| ---------------------- | ---------------------------------------------------- | -------------------------- | ------------------ | -------------------------------------------------------- |
| planId                 | Id плану до якого необхідно створити підписку        |  uuid                      | Так                | a9562240-10ca-42d7-8d90-bbd1ace3dc5a                     |
| merchantId             | ід мерчанта                                          | uuid(36)                   | Так                | 137d9304-0368-11ed-b939-0242ac120002                     |
| purpose                | Призначення платежу                                  | string (255)               | Ні                 | purpose                                                  |
| notificationUrl        | Url CallBack                                         | string (255)               | Ні                 | [https://example.com/notify](https://example.com/notify) |
| notificationEncryption | ознака криптування данних CallBack                   | boolean                    | Ні                 | true/false                                               |
| merchantComment        | додаткова інформація\коментар мерчанта по замовленню | <p>string(255)</p><p> </p> | Ні                 | merchantComment                                          |
| merchantRequestId      | Унікальний ID покупки у Вашому магазині.             | string (50)                | Так                | 137d9304-0368-11ed-b939-0242ac120002                     |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**      | **Опис**                        | **Формат даних** | **Приклад**                                                                                                                    |
| ----------------- | ------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| hppOrderId        | Id підписки                     | string           | 1697008393082nW0c1jr6KVv                                                                                                       |
| merchantRequestId | ID операції в системі Мерчанта  | string           | 137d9304-0368-11ed-b939-0242ac120002                                                                                           |
| orderStatus       | статус підписки                 | string           | <p>PENDING</p><p><a href="https://alliancedigital.atlassian.net/wiki/spaces/ECOMM1/pages/554729530">Статуси ECOM_ORDER</a></p> |
| merchantId        | ід мерчанту                     | string           | 137d9304-0368-11ed-b939-0242ac120002                                                                                           |
| createdAt         | Дата створення підписки         | string           | 2024-09-05 18:35:18.210+03:00                                                                                                  |

#### Приклад запиту&#x20;

```json
{
   "planId":"{{planId}}",
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "merchantRequestId":"{{requestUUIDT}}",
   "purpose":"Payment for food",
   "notificationUrl":"https://webhook.site/6f07f573-c4f3-453c-83e3-d1c5993eb57d",
   "notificationEncryption":false,
   "merchantComment":"erdshjtpasdfasfsadfs"
}
```

#### Приклад відповіді&#x20;

```json
{
    "hppOrderId": "1783608520205P81ch623POH",
    "merchantRequestId": "64fe98ab-9731-48aa-b855-78c28e797aef",
    "orderStatus": "PENDING",
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "createdAt": "2026-07-09 17:48:40.02+03:00"
}
```
