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

<table data-header-hidden data-search="false">
<thead>
<tr>
<th></th>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Параметр</strong></td>
<td><strong>Опис</strong></td>
<td><strong>Формат даних</strong></td>
<td><strong>Обовʼязковість</strong></td>
<td><strong>Приклад</strong></td>
</tr>

<tr>
<td>planId</td>
<td>Id плану до якого необхідно створити підписку</td>
<td>uuid</td>
<td>Так</td>
<td>a9562240-10ca-42d7-8d90-bbd1ace3dc5a</td>
</tr>

<tr>
<td>merchantId</td>
<td>ід мерчанта</td>
<td>uuid(36)</td>
<td>Так</td>
<td>137d9304-0368-11ed-b939-0242ac120002</td>
</tr>

<tr>
<td>purpose</td>
<td>Призначення платежу</td>
<td>string (255)</td>
<td>Ні</td>
<td>purpose</td>
</tr>

<tr>
<td>notificationUrl</td>
<td>Url CallBack</td>
<td>string (255)</td>
<td>Ні</td>
<td><a href="https://example.com/notify">https://example.com/notify</a></td>
</tr>

<tr>
<td>notificationEncryption</td>
<td>ознака криптування данних CallBack</td>
<td>boolean</td>
<td>Ні</td>
<td>true/false</td>
</tr>

<tr>
<td>merchantComment</td>
<td>додаткова інформація\коментар мерчанта по замовленню</td>
<td>string (255)</td>
<td>Ні</td>
<td>merchantComment</td>
</tr>

<tr>
<td>merchantRequestId</td>
<td>Унікальний ID покупки у Вашому магазині.</td>
<td>string (50)</td>
<td>Так</td>
<td>137d9304-0368-11ed-b939-0242ac120002</td>
</tr>

<tr>
<td>statusPageType</td>
<td>Тип сторінки статусу, на яку буде перенаправлено користувача після завершення платежу</td>
<td>enum</td>
<td>Так, якщо directType = REDIRECT</td>
<td>statusTimerPage, statusPage</td>
</tr>

<tr>
<td>hppPaymentMethods</td>
<td>Параметр, що визначає доступні для користувача способи оплати на HPP</td>
<td>enum</td>
<td>Так, якщо directType передано</td>
<td>CARD, APPLE_PAY, GOOGLE_PAY, TOKEN</td>
</tr>

<tr>
<td>directType</td>
<td>Тип переходу/відображення HPP для створеного ордера</td>
<td>enum</td>
<td>Так, якщо необхідно отримати redirectUrl для переходу на HPP</td>
<td>REDIRECT</td>
</tr>

<tr>
<td>customerData</td>
<td>Дані клієнта/платника, що передаються мерчантом для збереження та подальшого використання під час обробки платежу</td>
<td>object</td>
<td>Так</td>
<td>—</td>
</tr>

<tr>
<td>customerData.senderCustomerId</td>
<td>Унікальний ідентифікатор клієнта відправника в системі мерчанта</td>
<td>string (255)</td>
<td>Так</td>
<td>1258728c1</td>
</tr>

<tr>
<td>customerData.senderFirstName</td>
<td>Імʼя відправника</td>
<td>string (30)</td>
<td>Ні</td>
<td>Іван</td>
</tr>

<tr>
<td>customerData.senderLastName</td>
<td>Прізвище відправника</td>
<td>string (30)</td>
<td>Ні</td>
<td>Іваненко</td>
</tr>

<tr>
<td>customerData.senderMiddleName</td>
<td>По батькові відправника</td>
<td>string (30)</td>
<td>Ні</td>
<td>Іванович</td>
</tr>

<tr>
<td>customerData.senderEmail</td>
<td>Електронна пошта відправника</td>
<td>string (256)</td>
<td>Ні</td>
<td>mail@gmail.com</td>
</tr>

<tr>
<td>customerData.senderCountry</td>
<td>Код країни відправника відповідно до ISO 3166</td>
<td>string (3), ISO 3166</td>
<td>Ні</td>
<td>804</td>
</tr>

<tr>
<td>customerData.senderRegion</td>
<td>Область/регіон відправника</td>
<td>string (255)</td>
<td>Ні</td>
<td>Київська</td>
</tr>

<tr>
<td>customerData.senderCity</td>
<td>Місто відправника</td>
<td>string (25)</td>
<td>Ні</td>
<td>Київ</td>
</tr>

<tr>
<td>customerData.senderStreet</td>
<td>Вулиця відправника</td>
<td>string (35)</td>
<td>Ні</td>
<td>Січових стрільців</td>
</tr>

<tr>
<td>customerData.senderAdditionalAddress</td>
<td>Додаткові дані адреси відправника (номер будинку, квартира, поверх тощо)</td>
<td>string (255)</td>
<td>Ні</td>
<td>буд. 23, кв. 15</td>
</tr>

<tr>
<td>customerData.senderItn</td>
<td>Ідентифікаційний податковий номер (ІПН) відправника</td>
<td>string (20)</td>
<td>Ні</td>
<td>123456789</td>
</tr>

<tr>
<td>customerData.senderPassport</td>
<td>Дані паспорта відправника</td>
<td>string (255)</td>
<td>Ні</td>
<td>АН123456</td>
</tr>

<tr>
<td>customerData.senderIp</td>
<td>IP-адреса відправника</td>
<td>string (50)</td>
<td>Ні</td>
<td>123.12.12.12</td>
</tr>

<tr>
<td>customerData.senderPhone</td>
<td>Номер телефону відправника</td>
<td>string (50)</td>
<td>Ні</td>
<td>380630000000</td>
</tr>

<tr>
<td>customerData.senderBirthday</td>
<td>Дата народження відправника</td>
<td>string (50)</td>
<td>Ні</td>
<td>31.12.2000</td>
</tr>

<tr>
<td>customerData.senderGender</td>
<td>Гендер відправника</td>
<td>string (50)</td>
<td>Ні</td>
<td>Male/Female</td>
</tr>

<tr>
<td>customerData.senderZipCode</td>
<td>Поштовий індекс відправника</td>
<td>string (50)</td>
<td>Ні</td>
<td>49000</td>
</tr>

</tbody>
</table>

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**      | **Опис**                        | **Формат даних** | **Приклад**                          |
| ----------------- | ------------------------------- | ---------------- | ------------------------------------ |
| hppOrderId        | Id підписки                     | string           | 1697008393082nW0c1jr6KVv             |
| merchantRequestId | ID операції в системі Мерчанта  | uuid             | 137d9304-0368-11ed-b939-0242ac120002 |
| orderStatus       | статус підписки                 | string           | PENDING                              |
| merchantId        | ід мерчанту                     | uuid             | 137d9304-0368-11ed-b939-0242ac120002 |
| createdAt         | Дата створення підписки         | string           | 2024-09-05 18:35:18.210+03:00 
| redirectUrl       | Посилання на перенаправлення клєінта на платіжку сторінку HPP| string           |http://pgi-ecom-polcom.develop.bankalliance.ua//?hpp_id=1725536712817G6AXGJ4evXJ) |

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
    "createdAt": "2026-07-09 17:48:40.02+03:00",
    "redirectUrl": "http://pgi-ecom-polcom.develop.bankalliance.ua//?hpp_id=1725536712817G6AXGJ4evXJ"

}
```
