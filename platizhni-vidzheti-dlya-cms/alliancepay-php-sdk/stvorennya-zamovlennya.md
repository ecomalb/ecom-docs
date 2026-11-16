# Створення замовлення

Для разової оплати сформуйте `OrderRequestDTO`, викличте `CreateOrder::createOrder()` і перенаправте покупця за `redirectUrl`. У наведених прикладах `$authDto` створено за інструкцією «Авторизація».

### Створення посилання на оплату

Приклад створює замовлення на 100,50 грн. Замініть адреси `shop.example` на адреси свого застосунку.

#### Поля `OrderRequestDTO` у прикладі

| Поле                            | Тип            | Опис                                                                                                                                    |
| ------------------------------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `merchantRequestId`             | `string`       | Згенеруйте унікальний ID нового запиту через `GenerateRequestIdentification::generateRequestId()` і збережіть його у своєму застосунку. |
| `merchantId`                    | `string`       | Ідентифікатор мерчанта у вашому середовищі. Візьміть його з `$authDto->getMerchantId()`.                                                |
| `hppPayType`                    | `string`       | Тип платежу. Для разової оплати з одразу ж виконаним списанням передайте `PURCHASE`.                                                    |
| `directType`                    | `string\|null` | Спосіб переходу до оплати. Для перенаправлення на платіжну сторінку в прикладі передано `REDIRECT`.                                     |
| `coinAmount`                    | `int`          | Сума в мінімальних одиницях валюти замовлення. Наприклад, 100,50 грн передайте як `10050`.                                              |
| `currencyCode`                  | `int`          | Числовий код валюти. SDK підтримує `980` (UAH), `840` (USD) та `978` (EUR). За замовчуванням — `980`.                                   |
| `paymentMethods`                | `array`        | Перелік способів оплати. Для оплати карткою у прикладі передано `['CARD']`.                                                             |
| `statusPageType`                | `string`       | Вигляд сторінки результату в банку. У прикладі `STATUS_TIMER_PAGE` показує сторінку з таймером.                                         |
| `successUrl`                    | `string`       | Адреса вашого сайту, яку відкриє покупець після успішної оплати.                                                                        |
| `failUrl`                       | `string`       | Адреса вашого сайту, яку відкриє покупець у разі невдалої оплати.                                                                       |
| `notificationUrl`               | `string\|null` | HTTPS-адреса вашого сервера, на яку банк надсилає повідомлення про результат операції.                                                  |
| `customerData`                  | `array`        | Дані покупця. У прикладі передано масив із полем `senderCustomerId`.                                                                    |
| `customerData.senderCustomerId` | `string`       | Ідентифікатор покупця у вашій системі. Передайте його всередині масиву `customerData`.                                                  |

```php
use AlliancePay\Sdk\Payment\Dto\Order\OrderRequestDTO;
use AlliancePay\Sdk\Payment\Order\CreateOrder;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

$orderData = [
    'merchantRequestId' => GenerateRequestIdentification::generateRequestId(),
    'merchantId'        => $authDto->getMerchantId(),
    'hppPayType'        => 'PURCHASE',
    'directType'        => 'REDIRECT',
    'coinAmount'        => 10050,
    'currencyCode'      => OrderRequestDTO::CURRENCY_UAH,
    'paymentMethods'    => ['CARD'],
    'statusPageType'    => 'STATUS_TIMER_PAGE',
    'successUrl'        => 'https://shop.example/pay/success',
    'failUrl'           => 'https://shop.example/pay/fail',
    'notificationUrl'   => 'https://shop.example/webhooks/alliancepay',
    'customerData'      => ['senderCustomerId' => '12345'],
];

$order = (new CreateOrder())->createOrder(OrderRequestDTO::fromArray($orderData), $authDto);
$hppOrderId = $order->getHppOrderId();
$redirectUrl = $order->getRedirectUrl();
```

#### Поля відповіді `OrderResponseDTO`

| Поле          | Тип      | Опис                                                                                                              |
| ------------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `hppOrderId`  | `string` | Ідентифікатор замовлення на платіжній сторінці банку. Збережіть його разом із номером замовлення у вашій системі. |
| `redirectUrl` | `string` | Посилання на платіжну сторінку банку. Перенаправте покупця за цією адресою.                                       |

Перед перенаправленням покупця збережіть `merchantRequestId` і `hppOrderId` разом із локальним номером, валютою й сумою замовлення. Оплату підтверджуйте за перевіреним callback або серверним запитом стану.

### Суми в UAH, USD та EUR

|        |                     |                    |
| ------ | ------------------- | ------------------ |
| Валюта | currencyCode        | Приклад coinAmount |
| UAH    | 980 · CURRENCY\_UAH | 10050 — 100,50 грн |
| USD    | 840 · CURRENCY\_USD | 1000 — 10,00 USD   |
| EUR    | 978 · CURRENCY\_EUR | 2500 — 25,00 EUR   |

Передавайте ціле число в мінімальних одиницях валюти замовлення. Для `PURCHASE` у доларах чи євро змініть `currencyCode` і `coinAmount` у прикладі та перевірте, що валюту підключено для вашого мерчанта. У результаті валютної операції звіряйте суму й валюту джерела (`sourceAmount`, `sourceCurrencyCode`), курс `conversionRate` та гривневу суму `coinAmount`.
