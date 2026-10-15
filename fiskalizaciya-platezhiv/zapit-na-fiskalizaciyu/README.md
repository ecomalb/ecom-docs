---
description: 'Endpoint: POST /ecom/jws/cashbox/v2/fiscalization/create'
---

# Запит на фіскалізацію

Запит виконується після успішного завершення платіжної операції.

#### Особливості фіскалізації повернень

У разі повного або часткового повернення коштів фіскалізація виконується окремо для відповідної успішної операції повернення.

При частковому поверненні передайте коректні дані про товари або послуги, за які повертаються кошти. Ідентифікатори товарів мають відповідати товарам у початковій покупці; інші ідентифікатори або невідповідна кількість призводять до помилки.

Дані операції повернення зіставляються з початковою операцією покупки, що дозволяє сформувати фіскальний чек повернення з урахуванням інформації про початковий продаж.

### Тіло запиту

| Назва                           | Опис                                                                                                                                                                                                                                                                                   | Тип даних         | Обов'язковість                                                          | Приклад                                                 |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | ----------------------------------------------------------------------- | ------------------------------------------------------- |
| `merchantRequestId`             | Унікальний ідентифікатор запиту мерчанта.                                                                                                                                                                                                                                              | `string`          | Так                                                                     | `"8d2d1234-5678-4e92-a975-672f42fca5e3"`                |
| `merchantId`                    | Унікальний ідентифікатор мерчанта                                                                                                                                                                                                                                                      | `string`          | Так                                                                     | `“713e73d8-84ee-4873-98a3-7f67bf0ddd63“`                |
| `operationId`                   | Ідентифікатор платіжної операції Ecom, яку потрібно фіскалізувати.                                                                                                                                                                                                                     | `string`          | Так                                                                     | `"1772887138149SIx5b1QV7AI"`                            |
| `receiptComment`                | Коментар, переданий мерчантом для чека.                                                                                                                                                                                                                                                | `string` / `null` | Ні                                                                      | `"PAYMENT_FOR_ORDER_123"`                               |
| `notificationUrl`               | URL Merchant для асинхронного callback результату.                                                                                                                                                                                                                                     | `string`          | Так                                                                     | `"https://merchant.example.com/fiscalization/callback"` |
| `products`                      | Список товарів/послуг, що мають увійти до чека.                                                                                                                                                                                                                                        | `array<object>`   | Так                                                                     | `[]`                                                    |
| `products[].id`                 | ID товару в системі Merchant.                                                                                                                                                                                                                                                          | `string`          | Так                                                                     | `"yuiofaa2-7428-4053-8156-de4de571ac0e"`                |
| `products[].name`               | Назва товару/послуги.                                                                                                                                                                                                                                                                  | `string`          | Так                                                                     | `"Товар 1"`                                             |
| `products[].count`              | Кількість товару.                                                                                                                                                                                                                                                                      | `number`          | Так                                                                     | `2.000`                                                 |
| `products[].measurementCode`    | <p>Код одиниці виміру.<br>Беремо <code>UNIT_CODE</code> з <a href="https://app.gitbook.com/o/zBSkiJ3Oy2kvtv30JbMh/sites/site_0gnMK/s/djW26z83WQoOq0ZjunWw/~/edit/~/changes/438/fiskalizaciya-platezhiv/zapit-na-fiskalizaciyu/dovidnik-odinic-vimiru">довідника одиниць виміру</a></p> | `string`          | Так                                                                     | `"0001"`                                                |
| `products[].unitPrice`          | Ціна за одиницю в копійках.                                                                                                                                                                                                                                                            | `integer`         | Так                                                                     | `12000`                                                 |
| `products[].taxCode`            | <p>Код податкової групи.<br>Беремо <code>id</code> з <a href="https://app.gitbook.com/o/zBSkiJ3Oy2kvtv30JbMh/sites/site_0gnMK/s/djW26z83WQoOq0ZjunWw/~/edit/~/changes/438/fiskalizaciya-platezhiv/zapit-na-fiskalizaciyu/dovidnik-podatkovikh-grup">довідника податкових груп</a> </p> | `string`          | Умовно: так, якщо для товару є податок.                                 | `"2"`                                                   |
| `products[].classificationCode` | УКТЗЕД.                                                                                                                                                                                                                                                                                | `string` / `null` | Так, якщо products\[].taxCode == 2,7,8.                                 | `"2203000000"`                                          |
| `products[].exciseLabels`       | Акцизні марки товару.                                                                                                                                                                                                                                                                  | `array<string>`   | Так, якщо products\[].taxCode == 2,7,8 і товар вимагає вводу акц. марки | `["AATE123456"]`                                        |

### Відповідь

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
| `products[].taxCode`                | Код податкової групи.                                          | `string` / `null`                                       | Умовно                                                                                                 | `"2"`                                                   |
| `products[].classificationCode`     | УКТЗЕД.                                                        | `string` / `null`                                       | Умовно                                                                                                 | `"2203000000"`                                          |
| `products[].exciseLabels`           | Акцизні марки.                                                 | `array<string>`                                         | Умовно                                                                                                 | `["AATE123456"]`                                        |

> **Потребує звірки зі схемою API:** У прикладах синхронної відповіді нижче є поле `orderTaxNum`, якого немає в таблиці, а частина полів із таблиці в прикладах відсутня. Перед публікацією потрібно уточнити, які поля гарантовано повертає синхронна відповідь.

#### Приклад тіла запиту&#x20;

```json
{
    "merchantRequestId": "16d005d0-5746-417a-b141-c62cc8a948e7",
    "merchantId": "b2a21a4f-f918-4b57-88ab-f116ef2594b1",
    "operationId": "17920674411829L5_jTAzFqt",
    "receiptComment": "Оплата за товар",
    "notificationUrl": "https://webhook.site/03b7bbbe-b2e2-49bd-a5f3-038ae8398da3",
    "products": [
        {
            "id": "product-001",
            "name": "Тестовий товар 1",
            "count": 1,
            "measurementCode": "0303",
            "unitPrice": 50.00,
            "taxCode": "1"
        },
        {
            "id": "product-002",
            "name": "Тестовий товар 2",
            "count": 1,
            "measurementCode": "0303",
            "unitPrice": 50.00,
            "taxCode": "2",
            "classificationCode": "1234567890",
            "exciseLabels" : ["AATE123456"]
            
        }
    ]
}
```

#### Приклад відповіді на прийнятий запит

```json
{
    "merchantRequestId": "a1204971-4bec-4bf8-8722-e88d21fb615e",
    "merchantId": "b2a21a4f-f918-4b57-88ab-f116ef2594b1",
    "operationId": "1792065888219SVQb0CTdNxl",
    "status": "PENDING",
    "creationDateTime": "2026-10-15T15:06:06.382967+03:00",
    "orderTaxNum": null,
    "fiscalizationDateTime": null,
    "receiptUrl": null,
    "errorCode": null,
    "errorDescription": null
}
```

#### Приклад відповіді з помилкою перевірки

```json
{
    "merchantRequestId": "16d005d0-5746-417a-b141-c62cc8a948e7",
    "merchantId": "b2a21a4f-f918-4b57-88ab-f116ef2594b1",
    "operationId": "17920674411829L5_jTAzFqt",
    "status": "FAIL",
    "creationDateTime": "2026-10-15T15:31:53.374597+03:00",
    "orderTaxNum": null,
    "fiscalizationDateTime": null,
    "receiptUrl": null,
    "errorCode": "b_bucket_excise_product_without_classification_code_error",
    "errorDescription": "Акцизний товар повинен містити УКТЗЕД"
}
```
