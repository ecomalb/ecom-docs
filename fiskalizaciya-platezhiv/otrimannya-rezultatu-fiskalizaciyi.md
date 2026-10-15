# Отримання результату фіскалізації

Після надсилання запиту на фіскалізацію необхідно дочекатися результату обробки.

Успішне завершення платіжної операції та успішна фіскалізація — це два окремі процеси.

Платіж може мати статус `SUCCESS`, тоді як фіскалізація ще перебуватиме в обробці.

AlliancePay надсилає окремий Callback із результатом фіскалізації на адресу `notificationUrl`, передану в запиті. Структуру повідомлення та приклад наведено в документі «Callback по фіскалізації».

Рекомендується використовувати отриманий результат для оновлення стану фіскалізації замовлення у власній системі.

#### 7.1. Статуси фіскалізації

| Статус    | Значення                                                                                                                         |
| --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `SUCCESS` | Фіскалізація успішна; фіскальний номер присутній.                                                                                |
| `FAIL`    | Поточний запит завершився помилкою. Після усунення її причини операцію можна повторно подати на фіскалізацію.                    |
| `PENDING` | Запит прийнято до опрацювання; потрібно очікувати результату.                                                                    |
| `RECEIPT` | Чек сформовано в офлайн-режимі під час недоступності ДПС. У Callback уже є фіскальний номер; для мерчанта це успішний результат. |

Якщо ДПС недоступна, мерчант отримує Callback зі статусом `RECEIPT` і фіскальним номером. Після відновлення доступу чек автоматично реєструється в ДПС, а статус фіскалізації змінюється з `RECEIPT` на `SUCCESS`. **Повторний Callback після цієї зміни не надсилається.** Тому `RECEIPT` слід обробляти як успішний результат для мерчанта, не очікуючи ще одного повідомлення.

Платіжний Callback зі статусом `SUCCESS` підтверджує оплату, але не фіскалізацію. Оновлюйте стан фіскалізації за її окремим Callback зі статусом `SUCCESS`, `RECEIPT` або `FAIL`.

### Тіло повідомлення

| Назва                               | Опис                                                           | Тип даних                                               | Обов'язковість                                                                                         | Приклад                                                 |
| ----------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------- |
| `merchantRequestId`                 | Ідентифікатор первинного запиту Merchant.                      | `string`                                                | Так                                                                                                    | `"8d2d1234-5678-4e92-a975-672f42fca5e3"`                |
| `merchantId`                        | Ідентифікатор Merchant у Ecom.                                 | `string`                                                | Так                                                                                                    | `"f3bb63ae-0ed7-422b-a36a-98f0c65a36b3"`                |
| `operationId`                       | Ідентифікатор платіжної операції Ecom.                         | `string`                                                | Так                                                                                                    | `"1772887138149SIx5b1QV7AI"`                            |
| `operationType`                     | Тип операції в термінах Ecom.                                  | `string`, enum: `PURCHASE`, `REFUND`                    | Так                                                                                                    | `"PURCHASE"`                                            |
| `bucketId`                          | Ідентифікатор фіскального документа Alliance Kasa.             | `string` / `null`                                       | Так після того, як Kasa прийняла або знайшла запит; для локальної validation error може бути `null`.   | `"17884211495330w3O5fjP0Jj"`                            |
| `status`                            | Поточний статус фіскалізації.                                  | `string`, enum: `PENDING`, `SUCCESS`, `RECEIPT`, `FAIL` | Так                                                                                                    | `"PENDING"`                                             |
| `fiscalNumber`                      | Фіскальний номер чека.                                         | `string` / `null`                                       | Так для `SUCCESS` і `RECEIPT`; інакше `null`.                                                          | `"7711175116"`                                          |
| `receiptUrl`                        | Посилання на фіскальний чек.                                   | `string` / `null`                                       | Так для `SUCCESS` і `RECEIPT`; інакше `null`.                                                          | `"https://example.com/check/17884211495330w3O5fjP0Jj"`  |
| `receiptComment`                    | Коментар, який передав Merchant.                               | `string` / `null`                                       | Ні                                                                                                     | `"PAYMENT_FOR_ORDER_123"`                               |
| `notificationUrl`                   | URL Merchant для доставки callback.                            | `string`                                                | Так у callback за чинним описом; для sync response потребує підтвердження, оскільки є transport field. | `"https://merchant.example.com/fiscalization/callback"` |
| `fiscalizationDateTime`             | Час фіскалізації на стороні Alliance Kasa/ДПС.                 | `datetime` з timezone / `null`                          | Так для `SUCCESS` і `RECEIPT`; інакше `null`.                                                          | `"2026-09-03T10:39:10.000+03:00"`                       |
| `fiscalizationModificationDateTime` | Час останньої зміни фіскальних даних на стороні Alliance Kasa. | `datetime` з timezone / `null`                          | Ні; передається, якщо Kasa повернула `modificationDataTime`.                                           | `"2026-09-03T10:39:10.602+03:00"`                       |
| `creationDateTime`                  | Час створення запису фіскалізації в Ecom.                      | `datetime` з timezone                                   | Так                                                                                                    | `"2026-09-03T10:39:09.540+03:00"`                       |
| `modificationDateTime`              | Час останньої зміни локального запису фіскалізації в Ecom.     | `datetime` з timezone                                   | Так                                                                                                    | `"2026-09-03T10:39:10.602+03:00"`                       |
| `errorCode`                         | Код помилки Ecom або Alliance Kasa.                            | `string` / `null`                                       | Так для `FAIL`, якщо error code доступний; інакше `null`.                                              | `"541"`                                                 |
| `errorDescription`                  | Безпечний для Merchant опис помилки.                           | `string` / `null`                                       | Так для `FAIL`, якщо опис доступний; інакше `null`.                                                    | `"Помилка під час підписання"`                          |
| `products`                          | Незмінний список товарів/послуг первинного запиту Merchant.    | `array<object>`                                         | Так для повної єдиної DTO.                                                                             | `[]`                                                    |
| `products[].id`                     | ID товару в системі Merchant.                                  | `string`                                                | Так                                                                                                    | `"yuiofaa2-7428-4053-8156-de4de571ac0e"`                |
| `products[].name`                   | Назва товару/послуги.                                          | `string`                                                | Так                                                                                                    | `"Товар 1"`                                             |
| `products[].count`                  | Кількість товару.                                              | `number`                                                | Так                                                                                                    | `2.000`                                                 |
| `products[].measurementCode`        | Код одиниці виміру.                                            | `string`                                                | Так                                                                                                    | `"0001"`                                                |
| `products[].unitPrice`              | Ціна за одиницю у копійках — у форматі Merchant API.           | `integer`                                               | Так                                                                                                    | `12000`                                                 |
| `products[].taxCode`                | Код податкової групи.                                          | `integer` / `null`                                      | Умовно                                                                                                 | `2`                                                     |
| `products[].classificationCode`     | УКТЗЕД.                                                        | `string` / `null`                                       | Умовно                                                                                                 | `"2203000000"`                                          |
| `products[].exciseLabels`           | Акцизні марки.                                                 | `array<string>`                                         | Умовно                                                                                                 | `["AATE123456"]`                                        |

> **Потребує звірки зі схемою API:** У таблиці `products[].taxCode` має тип `integer`, а в наведеному прикладі передається як рядок (`"1"`, `"2"`).

### Приклад Callback

```json
{
  "merchantRequestId": "8a2dd1e6-00c8-4dab-9d8f-38567e20ac30",
  "merchantId": "f1958cfc-d69c-457d-a4be-b9a679daa9ad",
  "operationId": "1792065660719CH80FbvSte4",
  "operationType": "PURCHASE",
  "bucketId": "17920657374048Zg9QcX_vs8",
  "status": "SUCCESS",
  "fiscalNumber": "8038919714",
  "receiptUrl": "https://kasa.alb.ua/public/check/17920657374048Zg9QcX_vs8/generate_receipt",
  "receiptComment": "Оплата за товар",
  "notificationUrl": "https://webhook.site/03b7bbbe-b2e2-49bd-a5f3-038ae8398da3",
  "fiscalizationDateTime": "2026-10-15T15:02:20+03:00",
  "fiscalizationModificationDateTime": "2026-10-15T15:02:20.848+03:00",
  "creationDateTime": "2026-10-15T15:02:17.300424+03:00",
  "modificationDateTime": "2026-10-15T15:02:21.103961+03:00",
  "errorCode": null,
  "errorDescription": null,
  "products": [
    {
      "id": "ac7082-product-001",
      "name": "Тестовий товар Ecom",
      "count": 1,
      "taxCode": "1",
      "unitPrice": 50,
      "measurementCode": "0303"
    },
    {
      "id": "ac7082-product-001",
      "name": "Тестовий товар Ecom",
      "count": 1,
      "taxCode": "2",
      "unitPrice": 50,
      "exciseLabels": [
        "AATE123456"
      ],
      "measurementCode": "0303",
      "classificationCode": "1234567890"
    }
  ]
}
```
