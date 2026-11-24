---
description: >-
  Для відправки Callback буде виконаний Post запит на notificationUrl який був
  вказаний в запиті на створення замовлення
---

# Callback

**Вхідні параметри**

| Параметр               | Опис                                                                                                            | Формат даних           | Приклад                                                                                                                   |
| ---------------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| ecomOrderId            | Ідентифікатор замовлення в системі Ecom                                                                         | string                 | b68a9f2f-ad0d-4f52-a19e-11ee9c68d2a3                                                                                      |
| coinAmount             | Сума замовлення в копійках                                                                                      | long                   | 10                                                                                                                        |
| merchantId             | Ідентифікатор мерчанта в системі Ecom                                                                           | string                 | 467c8a10-c705-11ed-afa1-0242ac120002                                                                                      |
| statusUrl              | URL для перенаправлення клієнта на сторінку статусу замовлення                                                  | string                 | [https://status-pay.alb.ua/?hpp\_id=1783591442895jb5dQjA1bUl](https://status-pay.alb.ua/?hpp_id=1783591442895jb5dQjA1bUl) |
| hppOrderId             | Ідентифікатор замовлення в HPP                                                                                  | string                 | 1783591442895jb5dQjA1bUl                                                                                                  |
| redirectUrl            | URL для перенаправлення клієнта на платіжну сторінку HPP                                                        | string                 | [https://pay.alb.ua/?hpp\_id=1783591442895jb5dQjA1bUl](https://pay.alb.ua/?hpp_id=1783591442895jb5dQjA1bUl)               |
| notificationUrl        | URL, на який надсилається Callback із результатом обробки платежу. Якщо значення null, URL не задано            | string / null          | null                                                                                                                      |
| notificationEncryption | Ознака шифрування даних Callback. Якщо параметр не передано або передано false, дані Callback не шифруються     | boolean                | FALSE                                                                                                                     |
| notificationSignature  | Ознака використання підпису для Callback                                                                        | boolean                | FALSE                                                                                                                     |
| hppPayType             | Тип оплати                                                                                                      | string / Enum          | PURCHASE                                                                                                                  |
| hppDirectType          | Спосіб переходу клієнта на платіжну сторінку HPP                                                                | string / Enum          | QR                                                                                                                        |
| merchantRequestId      | Унікальний ідентифікатор запиту мерчанта                                                                        | string                 | d7208e22-0fb1-466d-b9cc-41c027075fb6                                                                                      |
| createDate             | Дата та час створення замовлення                                                                                | string (дата й час)    | 2026-07-09 13:04:02.91+03:00                                                                                              |
| paymentMethods         | Список доступних методів оплати для замовлення                                                                  | array of string / Enum | \["CARD", "GOOGLE\_PAY", "APPLE\_PAY"]                                                                                    |
| orderStatus            | Поточний статус замовлення                                                                                      | string / Enum          | SUCCESS                                                                                                                   |
| expiredOrderDate       | Дата та час завершення строку дії замовлення                                                                    | string (дата й час)    | 2026-07-10 13:04:02.89+03:00                                                                                              |
| operation              | Об'єкт із даними про платіжну операцію, пов'язану із замовленням                                                | object                 | [https://docs.merchant.alb.ua/platizhni-metodi-h2h/callback](https://docs.merchant.alb.ua/platizhni-metodi-h2h/callback)  |
| tryMode                | Режим виконання платежу, який визначає, чи дозволено виконувати декілька спроб оплати в межах одного замовлення | string / Enum          | ONE\_TRY                                                                                                                  |

#### Приклад тіла запиту HPP ордер&#x443;**:**&#x20;

```json
{
   "ecomOrderId":"b68a9f2f-ad0d-4f52-a19e-11ee9c68d2a3",
   "coinAmount":10,
   "merchantId":"467c8a10-c705-11ed-afa1-0242ac120002",
   "statusUrl":"https://status-pay.alb.ua/?hpp_id=1783591442895jb5dQjA1bUl",
   "hppOrderId":"1783591442895jb5dQjA1bUl",
   "redirectUrl":"https://pay.alb.ua/?hpp_id=1783591442895jb5dQjA1bUl",
   "notificationUrl":null,
   "notificationEncryption":false,
   "notificationSignature": false,
   "hppPayType":"PURCHASE",
   "hppDirectType":"QR",
   "merchantRequestId":"d7208e22-0fb1-466d-b9cc-41c027075fb6",
   "createDate":"2026-07-09 13:04:02.91+03:00",
   "paymentMethods":[
      "CARD",
      "GOOGLE_PAY",
      "APPLE_PAY"
   ],
   "orderStatus":"SUCCESS",
   "expiredOrderDate":"2026-07-10 13:04:02.89+03:00",
   "operation":{},
   "tryMode":"ONE_TRY"
}
```
