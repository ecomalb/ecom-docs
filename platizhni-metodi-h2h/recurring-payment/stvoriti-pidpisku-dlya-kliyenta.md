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

<table data-header-hidden data-search="false"><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Обовʼязковість</strong></td><td><strong>Приклад</strong></td></tr><tr><td>planId</td><td>Id плану до якого необхідно створити підписку</td><td> uuid</td><td>Так</td><td>a9562240-10ca-42d7-8d90-bbd1ace3dc5a</td></tr><tr><td>merchantId</td><td>ід мерчанта</td><td>uuid(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>purpose</td><td>Призначення платежу</td><td>string (255)</td><td>Ні</td><td>purpose</td></tr><tr><td>notificationUrl</td><td>Url CallBack</td><td>string (255)</td><td>Ні</td><td><a href="https://example.com/notify">https://example.com/notify</a></td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>boolean</td><td>Ні</td><td>true/false</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255)</p><p> </p></td><td>Ні</td><td>merchantComment</td></tr><tr><td>merchantRequestId</td><td>Унікальний ID покупки у Вашому магазині.</td><td>string (50)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr></tbody></table>

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**      | **Опис**                        | **Формат даних** | **Приклад**                          |
| ----------------- | ------------------------------- | ---------------- | ------------------------------------ |
| hppOrderId        | Id підписки                     | string           | 1697008393082nW0c1jr6KVv             |
| merchantRequestId | ID операції в системі Мерчанта  | uuid             | 137d9304-0368-11ed-b939-0242ac120002 |
| orderStatus       | статус підписки                 | string           | PENDING                              |
| merchantId        | ід мерчанту                     | uuid             | 137d9304-0368-11ed-b939-0242ac120002 |
| createdAt         | Дата створення підписки         | string           | 2024-09-05 18:35:18.210+03:00        |

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
