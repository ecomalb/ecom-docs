---
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
  anchors:
    visible: true
---

# Валідація customerData

Плагін формує `customerData` у методі `prepareCustomerData()` з платіжної адреси покупця у VirtueMart (**BT / BillTo**). Назви країни та регіону він отримує через відповідні моделі VirtueMart. Перед надсиланням до API дані обробляє сервіс `ValidateCustomerData`.

### Джерела та обмеження полів

Довжини в таблиці вказано в символах. Для `senderCustomerId` чинна схема позначає поле обов’язковим, а опис фільтрації уточнює, що порожнє значення плагін пропускає. Решта перелічених полів необов’язкові.

| Поле API                  | Тип             | Макс. довжина | Джерело у VirtueMart                | Обробка                                                                     |
| ------------------------- | --------------- | ------------- | ----------------------------------- | --------------------------------------------------------------------------- |
| `senderCustomerId`        | string          | 255           | BT → customer\_number               | Порожнє поле пропускається.                                                 |
| `senderFirstName`         | string          | 30            | BT → first\_name                    | Правила для імен і додаткова перевірка стоп-слів.                           |
| `senderLastName`          | string          | 30            | BT → last\_name                     | Правила для імен.                                                           |
| `senderMiddleName`        | string          | 30            | BT → middle\_name                   | Ті самі правила, що й для прізвища.                                         |
| `senderEmail`             | string          | 256           | BT → email                          | Довге значення обрізається до 256 символів.                                 |
| `senderCountry`           | string          | 3             | Модель country → country\_num\_code | Числовий код країни ISO за ID країни платника.                              |
| `senderRegion`            | string          | 255           | Модель state → state\_name          | Назва регіону за ID регіону платника.                                       |
| `senderCity`              | string          | 25            | BT → city                           | Обрізається до 25 символів.                                                 |
| `senderStreet`            | string          | 35            | BT → address\_1                     | Обрізається до 35 символів.                                                 |
| `senderAdditionalAddress` | string          | 255           | BT → address\_2                     | Обрізається до 255 символів.                                                |
| `senderIp`                | ip              | —             | BT → ip\_address                    | Перевіряється через FILTER\_VALIDATE\_IP. Некоректну адресу плагін вилучає. |
| `senderPhone`             | numeric\_string | 20            | BT → phone\_1 або phone\_2          | Якщо phone\_1 порожнє, плагін бере phone\_2. Зберігаються лише цифри.       |
| `senderZipCode`           | string          | 50            | BT → zip                            | Обрізається до 50 символів.                                                 |

### Як перевіряються імена

Для `senderFirstName`, `senderLastName` і `senderMiddleName` дозволено літери, цифри, дефіси й апострофи. Спецсимволи на початку або в кінці та значення, що складаються лише із цифр, не проходять перевірку.

Лише для `senderFirstName` плагін перевіряє часткові збіги зі стоп-словами `NULL`, `3D SECURE`, `SURNAME`, `CARDHOLDER` та `UNKNOWN`. Якщо знайдено збіг, плагін вилучає це поле з даних, які передає банку.
