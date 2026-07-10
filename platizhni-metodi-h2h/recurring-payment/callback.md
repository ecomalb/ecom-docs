# CallBack

Система надсилає callback на URL, який був вказаний при створенні підписки, у трьох випадках:

<table data-header-hidden><thead><tr><th width="248.2083740234375"></th><th></th></tr></thead><tbody><tr><td><strong>Подія</strong></td><td><strong>Коли надсилається</strong></td></tr><tr><td>Створення підписки</td><td>Одразу після створення підписки</td></tr><tr><td>Інітний платіж</td><td>Після завершення першого платежу (успіх/помилка)</td></tr><tr><td>Recurring списання</td><td>Після кожного автоматичного або ручного списання</td></tr></tbody></table>

#### Вихідні параметри:

<table data-search="false"><thead><tr><th>Параметр</th><th>Опис</th><th>Формат даних</th><th>Приклад</th></tr></thead><tbody><tr><td><code>ecomOrderId</code></td><td>Унікальний ідентифікатор ордера в системі ecom</td><td>UUID (string)</td><td><code>"216d0a89-0153-49e3-a120-442d6c64d094"</code></td></tr><tr><td><code>coinAmount</code></td><td>Сума ордера в мінімальних одиницях валюти (копійках). Для SUBSCRIPTION-ордерів = 0, оскільки сума визначається версією плану</td><td>integer</td><td><code>0</code></td></tr><tr><td><code>merchantId</code></td><td>Унікальний ідентифікатор мерчанта</td><td>UUID (string)</td><td><code>"137d9304-0368-11ed-b939-0242ac120002"</code></td></tr><tr><td><code>statusUrl</code></td><td>URL для перевірки статусу ордера (для SUBSCRIPTION не використовується)</td><td>string | null</td><td><code>null</code></td></tr><tr><td><code>hppOrderId</code></td><td>Внутрішній ідентифікатор ордера в HPP-системі</td><td>string</td><td><code>"1783608520205P81ch623POH"</code></td></tr><tr><td><code>redirectUrl</code></td><td>URL для редіректу клієнта після оплати </td><td>string | null</td><td><code>null</code></td></tr><tr><td><code>notificationUrl</code></td><td>URL мерчанта, на який надсилається callback</td><td>string (URL)</td><td><code>"https://webhook.site/6f05f573-..."</code></td></tr><tr><td><code>notificationEncryption</code></td><td>Прапорець, чи зашифровано тіло callback</td><td>boolean</td><td><code>false</code></td></tr><tr><td><code>hppPayType</code></td><td>Тип платіжного флоу ордера</td><td>enum: <code>SUBSCRIPTION</code></td><td><code>"SUBSCRIPTION"</code></td></tr><tr><td><code>hppDirectType</code></td><td>Тип взаємодії з HPP</td><td>enum: <code>REDIRECT</code>, <code>DIRECT</code></td><td><code>"REDIRECT"</code></td></tr><tr><td><code>merchantRequestId</code></td><td>Ідентифікатор запиту від мерчанта (ідемпотентність ордера)</td><td>UUID (string)</td><td><code>"64fe98ab-9731-48aa-b855-78c28e797aef"</code></td></tr><tr><td><code>createDate</code></td><td>Дата та час створення ордера</td><td>ISO 8601 datetime з timezone</td><td><code>"2026-07-09 17:48:40.26+03:00"</code></td></tr><tr><td><code>paymentMethods</code></td><td>Дозволені методи оплати (для SUBSCRIPTION визначаються при інітному платежі)</td><td>array | null</td><td><code>null</code></td></tr><tr><td><code>orderStatus</code></td><td>Поточний статус ордера</td><td>enum: <code>PENDING</code>, <code>SUCCESS</code></td><td><code>"PENDING"</code></td></tr><tr><td><code>expiredOrderDate</code></td><td>Дата закінчення терміну дії ордера (+10 років для підписок)</td><td>ISO 8601 datetime з timezone</td><td><code>"2036-07-06 18:03:40.20+03:00"</code></td></tr><tr><td><code>operation.type</code></td><td>Тип операції</td><td>enum: <code>PURCHASE</code></td><td><code>"PURCHASE"</code></td></tr><tr><td><code>operation.rrn</code></td><td>Retrieval Reference Number — унікальний номер транзакції в платіжній мережі</td><td>string (12 цифр)</td><td><code>"619015619077"</code></td></tr><tr><td><code>operation.purpose</code></td><td>Призначення платежу</td><td>string</td><td><code>"Payment for food"</code></td></tr><tr><td><code>operation.comment</code></td><td>Коментар до операції</td><td>string</td><td><code>"testing Nick"</code></td></tr><tr><td><code>operation.coinAmount</code></td><td>Сума конкретного платежу в копійках</td><td>integer</td><td><code>100</code> (= 1.00 грн)</td></tr><tr><td><code>operation.merchantId</code></td><td>Ідентифікатор мерчанта</td><td>UUID (string)</td><td><code>"137d9304-0368-11ed-b939-0242ac120002"</code></td></tr><tr><td><code>operation.operationId</code></td><td>Внутрішній ідентифікатор операції в HPP</td><td>string</td><td><code>"1783609267213ROxtSXOXgFm"</code></td></tr><tr><td><code>operation.ecomOperationId</code></td><td>Унікальний ідентифікатор операції в ecom (задається мерчантом)</td><td>UUID (string)</td><td><code>"2b8c65e4-edef-4d62-becc-8fe8c166b0cc"</code></td></tr><tr><td><code>operation.merchantName</code></td><td>Назва мерчанта/терміналу</td><td>string</td><td><code>"KB test terminal"</code></td></tr><tr><td><code>operation.approvalCode</code></td><td>Код авторизації від банку-емітента</td><td>string (6 символів)</td><td><code>"007747"</code></td></tr><tr><td><code>operation.status</code></td><td>Статус операції</td><td>enum: <code>SUCCESS</code>, <code>FAIL</code>, <code>IN_PROGRESS</code></td><td><code>"SUCCESS"</code></td></tr><tr><td><code>operation.transactionType</code></td><td>Тип транзакції (35 = EcomPurchase)</td><td>integer</td><td><code>35</code></td></tr><tr><td><code>operation.merchantRequestId</code></td><td>Ідентифікатор запиту мерчанта для цієї операції (ідемпотентність платежу)</td><td>UUID (string)</td><td><code>"8f989505-d8ee-402e-ae78-..."</code></td></tr><tr><td><code>operation.transactionCurrency</code></td><td>Код валюти транзакції за ISO 4217 (числовий)</td><td>string (3 цифри)</td><td><code>"980"</code> (= UAH)</td></tr><tr><td><code>operation.creationDateTime</code></td><td>Дата та час створення операції</td><td>yyyy.MM.dd HH<span data-gb-custom-inline data-tag="emoji" data-code="1f1f2-1f1f2">🇲🇲</span>ss.SSS</td><td><code>"2026.07.09 18:01:07.271"</code></td></tr><tr><td><code>operation.modificationDateTime</code></td><td>Дата та час останньої зміни статусу</td><td>yyyy.MM.dd HH<span data-gb-custom-inline data-tag="emoji" data-code="1f1f2-1f1f2">🇲🇲</span>ss.SSS</td><td><code>"2026.07.09 18:02:13.061"</code></td></tr><tr><td><code>operation.processingDateTime</code></td><td>Дата та час обробки транзакції процесингом</td><td>yyyy.MM.dd HH<span data-gb-custom-inline data-tag="emoji" data-code="1f1f2-1f1f2">🇲🇲</span>ss.SSS</td><td><code>"2026.07.09 18:01:08.000"</code></td></tr><tr><td><code>operation.transactionResponseInfo.actionCode</code></td><td>Код дії від процесингу (<code>"0"</code> = успіх)</td><td>string</td><td><code>"0"</code></td></tr><tr><td><code>operation.transactionResponseInfo.responseCode</code></td><td>Код відповіді від процесингу (<code>"00"</code> = approved)</td><td>string (2 символи)</td><td><code>"00"</code></td></tr><tr><td><code>operation.transactionResponseInfo.description</code></td><td>Текстовий опис результату</td><td>string</td><td><code>"approved"</code></td></tr><tr><td><code>operation.bankCode</code></td><td>Код банку-еквайера</td><td>string</td><td><code>"BANK_ALLIANCE"</code></td></tr><tr><td><code>operation.paymentSystem</code></td><td>Платіжна система картки</td><td>string</td><td><code>"MasterCard"</code></td></tr><tr><td><code>operation.productType</code></td><td>Тип продукту операції</td><td>enum: <code>PURCHASE</code></td><td><code>"PURCHASE"</code></td></tr><tr><td><code>operation.paymentServiceType</code></td><td>Тип платіжного сервісу</td><td>enum: <code>CARD</code>, <code>TOKEN</code>, <code>APPLE_PAY</code>, <code>GOOGLE_PAY</code></td><td><code>"CARD"</code></td></tr><tr><td><code>operation.notificationEncryption</code></td><td>Чи зашифровано тіло callback на рівні операції</td><td>boolean</td><td><code>false</code></td></tr><tr><td><code>operation.notificationSignature</code></td><td>Чи підписано callback (для верифікації автентичності)</td><td>boolean</td><td><code>true</code></td></tr><tr><td><code>operation.hppOrderId</code></td><td>Ідентифікатор ордера, до якого належить операція</td><td>string</td><td><code>"1783608520205P81ch623POH"</code></td></tr><tr><td><code>operation.processingTerminalId</code></td><td>Ідентифікатор терміналу в процесингу</td><td>string</td><td><code>"AE001001"</code></td></tr><tr><td><code>operation.processingMerchantId</code></td><td>Ідентифікатор мерчанта в процесингу</td><td>string</td><td><code>"AE001001"</code></td></tr><tr><td><code>operation.creatorSystem</code></td><td>Система-ініціатор операції</td><td>string</td><td><code>"HPP"</code></td></tr><tr><td><code>operation.merchantComment</code></td><td>Коментар мерчанта при створенні операції</td><td>string</td><td><code>"Helllo World. Lets rock123"</code></td></tr><tr><td><code>operation.cardNumberMask</code></td><td>Маскований номер картки</td><td>string (PAN masked)</td><td><code>"53759310••••0349"</code></td></tr><tr><td><code>operation.desiredThreeDSMode</code></td><td>Бажаний режим 3DS (вказаний при створенні)</td><td>enum: <code>MUST</code>, <code>MUST_NOT</code>, <code>OPTIONAL</code></td><td><code>"MUST_NOT"</code></td></tr><tr><td><code>operation.threeDSMode</code></td><td>Фактичний режим 3DS, який був застосований</td><td>enum: <code>MUST</code>, <code>MUST_NOT</code>, <code>OPTIONAL</code></td><td><code>"MUST_NOT"</code></td></tr><tr><td><code>operation.senderCustomerId</code></td><td>Ідентифікатор клієнта в системі мерчанта</td><td>string</td><td><code>"Nikos"</code></td></tr><tr><td><code>operation.senderFirstName</code></td><td>Ім'я відправника</td><td>string</td><td><code>"Богдан"</code></td></tr><tr><td><code>operation.senderLastName</code></td><td>Прізвище відправника</td><td>string</td><td><code>"Карпусь"</code></td></tr><tr><td><code>operation.senderMiddleName</code></td><td>По батькові відправника</td><td>string</td><td><code>"Олександрович"</code></td></tr><tr><td><code>operation.senderEmail</code></td><td>Email відправника</td><td>string</td><td><code>"qtest@testor.com"</code></td></tr><tr><td><code>operation.senderCountry</code></td><td>Код країни за ISO 3166-1 (числовий)</td><td>string (3 цифри)</td><td><code>"804"</code> (= Україна)</td></tr><tr><td><code>operation.senderRegion</code></td><td>Область / регіон</td><td>string</td><td><code>"Kiyivska"</code></td></tr><tr><td><code>operation.senderCity</code></td><td>Місто</td><td>string</td><td><code>"Kiyv"</code></td></tr><tr><td><code>operation.senderStreet</code></td><td>Вулиця</td><td>string</td><td><code>"khreshatuk"</code></td></tr><tr><td><code>operation.senderAdditionalAddress</code></td><td>Додаткова адреса</td><td>string</td><td><code>"Ukraine, Lviv, Arsenalna st."</code></td></tr><tr><td><code>operation.senderItn</code></td><td>ІПН (індивідуальний податковий номер)</td><td>string (10 цифр)</td><td><code>"3667709657"</code></td></tr><tr><td><code>operation.senderPassport</code></td><td>Серія та номер паспорта</td><td>string</td><td><code>"HE111999"</code></td></tr><tr><td><code>operation.senderIp</code></td><td>IP-адреса клієнта</td><td>string (IPv4)</td><td><code>"192.168.2.1"</code></td></tr><tr><td><code>operation.senderPhone</code></td><td>Номер телефону (без "+")</td><td>string</td><td><code>"380931234567"</code></td></tr><tr><td><code>operation.senderBirthday</code></td><td>Дата народження</td><td>string (dd.MM.yyyy)</td><td><code>"32.13.2050"</code></td></tr><tr><td><code>operation.senderGender</code></td><td>Стать</td><td>string</td><td><code>"Male"</code></td></tr><tr><td><code>operation.senderZipCode</code></td><td>Поштовий індекс</td><td>string</td><td><code>"18900"</code></td></tr><tr><td><code>operation.senderPaymentSystem</code></td><td>Платіжна система картки відправника</td><td>string</td><td><code>"MasterCard"</code></td></tr><tr><td><code>operation.senderCardNumberMask</code></td><td>Маскований номер картки відправника</td><td>string (PAN masked)</td><td><code>"53759310••••0349"</code></td></tr><tr><td><code>operation.senderBankCode</code></td><td>Код банку-емітента картки відправника</td><td>string</td><td><code>"BANK_ALLIANCE"</code></td></tr><tr><td><code>operation.externalCardToken</code></td><td>Токен картки для наступних recurring-списань</td><td>string</td><td><code>"cjy62IyteD4KMX9j-tGlxCYW"</code></td></tr><tr><td><code>operation.receiptUrl</code></td><td>URL для генерації квитанції за операцією</td><td>string (URL)</td><td><code>"https://defe-api.develop.bankalliance.ua/generate_receipt/..."</code></td></tr><tr><td><code>operation.scheduledPaymentId</code></td><td>Унікальний ідентифікатор запланованого платежу з графіку</td><td>UUID (string)</td><td><code>"64917dd4-ca06-44db-9eb2-99aba73ce2b9"</code></td></tr><tr><td><code>operation.paymentMethodType</code></td><td>Метод оплати, яким було проведено платіж</td><td>enum: <code>CARD</code>, <code>TOKEN</code>, <code>APPLE_PAY_ENCRYPTED</code>, <code>APPLE_PAY_DECRYPTED</code>, <code>GOOGLE_PAY_ENCRYPTED</code>, <code>GOOGLE_PAY_DECRYPTED</code></td><td><code>"CARD"</code></td></tr><tr><td><code>operation.categorySubcategoryIndicator</code></td><td>Тип підписки за класифікацією МПС (Mastercard / Visa). Визначає категорію recurring-платежу</td><td>enum: <code>C101</code>, <code>C102</code>, <code>C103</code>, <code>M101</code>, <code>M102</code>, <code>M103</code></td><td><code>"C102"</code></td></tr><tr><td><code>operation.recurringTransactionType</code></td><td>Тип recurring-транзакції: <code>O</code> — Original (інітний), <code>M</code> — Merchant-initiated (автоматичне списання)</td><td>enum: <code>O</code>, <code>M</code></td><td><code>"O"</code></td></tr><tr><td><code>operation.isInitial</code></td><td>Прапорець, чи є цей платіж інітним (першим) у підписці</td><td>boolean</td><td><code>true</code></td></tr><tr><td><code>tryMode</code></td><td>Режим обробки платежів ордера</td><td>enum: <code>MULTI_PAYMENT</code></td><td><code>"MULTI_PAYMENT"</code></td></tr></tbody></table>

#### Приклад відповіді

```json
{
   "ecomOrderId":"216d0a89-0153-49e3-a120-442d6c64d094",
   "coinAmount":0,
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "statusUrl":null,
   "hppOrderId":"1783608520205P81ch623POH",
   "redirectUrl":null,
   "notificationUrl":"https://webhook.site/6f05f573-c4f3-453c-83e3-d1c5993eb57d",
   "notificationEncryption":false,
   "hppPayType":"SUBSCRIPTION",
   "hppDirectType":"REDIRECT",
   "merchantRequestId":"64fe98ab-9731-48aa-b855-78c28e797aef",
   "createDate":"2026-07-09 17:48:40.26+03:00",
   "paymentMethods":null,
   "orderStatus":"PENDING",
   "expiredOrderDate":"2036-07-06 18:03:40.20+03:00",
   "operation":{
      "type":"PURCHASE",
      "rrn":"619015619077",
      "purpose":"Payment for food",
      "comment":"testing Nick",
      "coinAmount":100,
      "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
      "operationId":"1783609267213ROxtSXOXgFm",
      "ecomOperationId":"2b8c65e4-edef-4d62-becc-8fe8c166b0cc",
      "merchantName":"KB test terminal",
      "approvalCode":"007747",
      "status":"SUCCESS",
      "transactionType":35,
      "merchantRequestId":"8f989505-d8ee-402e-ae78-14b45de81ef2",
      "transactionCurrency":"980",
      "creationDateTime":"2026.07.09 18:01:07.271",
      "modificationDateTime":"2026.07.09 18:02:13.061",
      "processingDateTime":"2026.07.09 18:01:08.000",
      "transactionResponseInfo":{
         "actionCode":"0",
         "responseCode":"00",
         "description":"approved"
      },
      "bankCode":"BANK_ALLIANCE",
      "paymentSystem":"MasterCard",
      "productType":"PURCHASE",
      "paymentServiceType":"CARD",
      "notificationEncryption":false,
      "notificationSignature":true,
      "hppOrderId":"1783608520205P81ch623POH",
      "processingTerminalId":"AE001001",
      "processingMerchantId":"AE001001",
      "creatorSystem":"HPP",
      "merchantComment":"Helllo World. Lets rock123",
      "cardNumberMask":"53759310••••0349",
      "desiredThreeDSMode":"MUST_NOT",
      "threeDSMode":"MUST_NOT",
      "senderCustomerId":"Nikos",
      "senderFirstName":"Богдан",
      "senderLastName":"Карпусь",
      "senderMiddleName":"Олександрович",
      "senderEmail":"qtest@testor.com",
      "senderCountry":"804",
      "senderRegion":"Kiyivska",
      "senderCity":"Kiyv",
      "senderStreet":"khreshatuk",
      "senderAdditionalAddress":"Ukraine, Lviv, Arsenalna st.",
      "senderItn":"3667709657",
      "senderPassport":"HE111999",
      "senderIp":"192.168.2.1",
      "senderPhone":"380931234567",
      "senderBirthday":"32.13.2050",
      "senderGender":"Male",
      "senderZipCode":"18900",
      "senderPaymentSystem":"MasterCard",
      "senderCardNumberMask":"53759310••••0349",
      "senderBankCode":"BANK_ALLIANCE",
      "externalCardToken":"cjy62IyteD4KMX9j-tGlxCYW",
      "receiptUrl":"https://defe-api.develop.bankalliance.ua/generate_receipt/2b8c65e4-edef-4d62-becc-8fe8c166b0cc/1783609267213ROxtSXOXgFm",
      "scheduledPaymentId":"64917dd4-ca06-44db-9eb2-99aba73ce2b9",
      "paymentMethodType":"CARD",
      "categorySubcategoryIndicator":"C102",
      "recurringTransactionType":"O",
      "isInitial":true
   },
   "tryMode":"MULTI_PAYMENT"
}
```



