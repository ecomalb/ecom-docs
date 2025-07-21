---
description: >-
  Для відправки Callback буде виконаний Post запит на notificationUrl який був
  вказаний в запиті на створення замовлення
---

# Callback

**Вхідні параметри**

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="141">Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>ecomOrderId</td><td>Id замовлення в системі єком</td><td>string</td><td>bd68c2e5-3642-4527-90c3-e3fd8a73e594</td></tr><tr><td>coinAmount</td><td>сума замовлення</td><td>long</td><td>2000</td></tr><tr><td>merchantId</td><td>Id мерчанта в системі єком</td><td>string</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>statusUrl</td><td>url для редіректу на сторінку статусу</td><td>string</td><td><a href="http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY">http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY</a></td></tr><tr><td>hppOrderId</td><td>Id замовлення</td><td>string</td><td>17285584837476oqrSs7PszY</td></tr><tr><td>redirectUrl</td><td>посилання на перенаправлення клієнта на платіжку сторінку </td><td>string</td><td><a href="http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY">http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY</a></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string</td><td><a href="https://example.com/notify">https://example.com/notify</a></td></tr><tr><td>hppPayType</td><td>тип оплати</td><td>string</td><td>PURCHASE</td></tr><tr><td>merchantRequestId</td><td>унікальний ідентифікатор мерчанта</td><td>string</td><td>137d9304-0318-11ed-b939-0241ac120104</td></tr><tr><td>orderStatus</td><td>статус замовлення </td><td>string</td><td>SUCCESS</td></tr><tr><td>createDate</td><td>дата та час створення замовлення</td><td>string</td><td>22024-10-10 14:08:03.67+03:00</td></tr><tr><td>paymentMethods</td><td>методи оплати </td><td></td><td>CARD</td></tr><tr><td>expiredOrderDate</td><td>дата та час дії замовлення </td><td>string</td><td>2024-10-10 14:23:03.67+03:00</td></tr><tr><td>operations</td><td>об'єкт з даними по операції</td><td>object</td><td><a href="https://docs.merchant.alb.ua/~/revisions/abJLhIBPG580oCHyrm7Q/platizhni-metodi-h2h/callback">https://docs.merchant.alb.ua/~/revisions/abJLhIBPG580oCHyrm7Q/platizhni-metodi-h2h/callback</a></td></tr></tbody></table>

**Вхідні параметри:**&#x20;

```json
{
   "ecomOrderId":" ",
   "coinAmount":5000,
   "merchantId":" ",
   "statusUrl":"https://status-pay.alb.ua/?hpp_id=",
   "hppOrderId":" ",
   "redirectUrl":"https://pay.alb.ua/?hpp_id=",
   "notificationUrl":" ",
   "notificationEncryption":false,
   "hppPayType":"PURCHASE",
   "hppDirectType":"REDIRECT",
   "merchantRequestId":" ",
   "createDate":"2025-07-21 10:20:23.49+00:00",
   "paymentMethods":[
      "APPLE_PAY",
      "GOOGLE_PAY",
      "CARD"
   ],
   "orderStatus":"SUCCESS",
   "expiredOrderDate":"2025-07-21 10:35:23.41+00:00",
   "operation":{
      
   }
}
```

