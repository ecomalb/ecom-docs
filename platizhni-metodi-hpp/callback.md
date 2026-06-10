---
description: >-
  Для відправки Callback буде виконаний Post запит на notificationUrl який був
  вказаний в запиті на створення замовлення
---

# Callback

**Вхідні параметри**

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="141">Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td>ecomOrderId</td><td>Id замовлення в системі єком</td><td>string</td><td>bd68c2e5-3642-4527-90c3-e3fd8a73e594</td></tr><tr><td>coinAmount</td><td>сума замовлення в копійках</td><td>long</td><td>2000</td></tr><tr><td>merchantId</td><td>Id мерчанта в системі єком</td><td>string</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>statusUrl</td><td>url для редіректу на сторінку статусу</td><td>string</td><td><a href="http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY">http://pgi-status-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY</a></td></tr><tr><td>hppOrderId</td><td>Id замовлення</td><td>string</td><td>17285584837476oqrSs7PszY</td></tr><tr><td>redirectUrl</td><td>посилання на перенаправлення клієнта на платіжку сторінку </td><td>string</td><td><a href="http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY">http://pgi-ecom-release.develop.bankalliance.ua/?hpp_id=17285584837476oqrSs7PszY</a></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string</td><td><a href="https://example.com/notify">https://example.com/notif</a></td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>true/false Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</td></tr><tr><td>hppPayType</td><td>тип оплати</td><td>string</td><td>PURCHASE</td></tr><tr><td>hppDirectType</td><td>спосіб перенаправлення клієнта на платіжні сторінку</td><td>Enum</td><td><p></p><ul><li>LINK - Link згенерована в офісі (клієнт попадає на хпп по лінку)</li><li>REDIRECT - Link згенерована через Api (клієнт попадає на хпп через редірект від мерчанта)</li></ul></td></tr><tr><td>merchantRequestId</td><td>унікальний ідентифікатор мерчанта</td><td>string</td><td>137d9304-0318-11ed-b939-0241ac120104</td></tr><tr><td>orderStatus</td><td>статус замовлення </td><td>string</td><td>SUCCESS</td></tr><tr><td>createDate</td><td>дата та час створення замовлення</td><td>string</td><td>22024-10-10 14:08:03.67+03:00</td></tr><tr><td>paymentMethods</td><td>методи оплати </td><td>object</td><td><p>"APPLE_PAY",</p><p>"GOOGLE_PAY",</p><p> "CARD"</p></td></tr><tr><td>expiredOrderDate</td><td>дата та час дії замовлення </td><td>string</td><td>2024-10-10 14:23:03.67+03:00</td></tr><tr><td>operation</td><td>об'єкт з даними по операції</td><td>object</td><td><a href="https://docs.merchant.alb.ua/platizhni-metodi-h2h/callback">https://docs.merchant.alb.ua/platizhni-metodi-h2h/callback</a></td></tr></tbody></table>

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

**Вхідні параметри для зовнішнього А2А**&#x20;

```json
{
   "ecomOrderId":"c6c4fe06-8d26-4c04-ae4a-a97b1bf03676",
   "coinAmount":100,
   "merchantId":"7437c8e2-0ed1-449c-bbb5-cdf27447bf0a",
   "statusUrl":null,
   "hppOrderId":"1781086744398g0HxVBDHeuY",
   "redirectUrl":"",
   "notificationUrl":"https://webhook.site/...",
   "notificationEncryption":false,
   "hppPayType":"A2A",
   "hppDirectType":"BANK_LINK",
   "merchantRequestId":"e3a815a9-6084-4047-b9a1-04b9466fdfc2",
   "createDate":"2026-06-10 13:19:05.44+03:00",
   "paymentMethods":[
      "CARD",
      "APPLE_PAY",
      "GOOGLE_PAY"
   ],
   "orderStatus":"SUCCESS",
   "expiredOrderDate":"2026-06-11 13:19:04.40+03:00",
   "operation":{
      "type":"ACCOUNT_2_ACCOUNT",
      "purpose":"Payment for Order №1234565555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555555",
      "coinAmount":1054,
      "merchantId":"7437c8e2-0ed1-449c-bbb5-cdf27447bf0a",
      "operationId":"1781086765946c5WS7nTkPp7",
      "ecomOperationId":"ae54e521-199f-4c9e-b222-f03aed229dc5",
      "merchantName":"ФОП тест",
      "status":"SUCCESS",
      "transactionType":54,
      "transactionCurrency":"980",
      "creationDateTime":"2026.06.10 13:19:29.126",
      "modificationDateTime":"2026.06.10 13:19:29.126",
      "transactionResponseInfo":{
         
      },
      "bankCode":"BANK_ALLIANCE",
      "paymentServiceType":"ACCOUNT",
      "notificationEncryption":false,
      "notificationSignature":false,
      "hppOrderId":"1781086744398g0HxVBDHeuY",
      "creatorSystem":"HPP",
      "merchantComment":"Сплата рахунку від 10.06.2026, за послугою на сайті https://test.ua/, акаунт Id",
      "senderCountry":"804",
      "senderCity":"Іaws - Юыяєї'ь .?,/-'*_()",
      "senderStreet":"Мальвіна - Vict'рыя 12345юєїяуь3435",
      "senderAccount":"UA923004650000025702103000001",
      "senderFirstName":"Іваaws - Ювяєї'ь 1234 Куицьйкф",
      "senderLastName":"Іваaws - Ювяєї'ь 1234 Куицьйкф",
      "senderGender":"Female",
      "senderCustomerId":"Id",
      "senderMiddleName":"Іваaws - Ювяєї'ь 1234 Куицьйкф",
      "senderEmail":"aq@",
      "senderRegion":"Київ",
      "senderAdditionalAddress":"aqavbnmwreyuio іюяєео'жуї эыжъвб .,/-_+=`1234098(ff)#![]*^ 1122121222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222222",
      "senderItn":"5555557777",
      "senderPassport":"Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis,",
      "senderIp":"2001:0db8:3333:4444:5555:6666:7777:8888",
      "senderPhone":"380634387596",
      "senderBirthday":"10.01.2000",
      "senderZipCode":"111111111111111111111111111111111111111111111141",
      "senderBankCode":"BANK_ALLIANCE",
      "recipientAccount":"UA703001190000026201132371001",
      "recipientFirstName":"Бондар Діана",
      "recipientBankCode":"BANK_ALLIANCE",
      "repeatedPayment":false
   },
   "tryMode":"ONE_TRY"
}
```
