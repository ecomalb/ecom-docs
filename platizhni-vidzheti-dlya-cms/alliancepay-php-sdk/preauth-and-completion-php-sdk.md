---
description: >-
  PREAUTH — двофазний платіж: спочатку кошти блокуються на картці покупця, а
  потім мерчант підтверджує списання через операцію COMPLETION.
---

# PreAuth and Completion PHP SDK

`PREAUTH` резервує кошти. `COMPLETION` окремим запитом підтверджує списання. Для підтвердження збережіть `operationId` успішного резервування та його початкову суму в копійках UAH.

### Створення PREAUTH

Сформуйте `$orderData` за прикладом «Створення замовлення». Перш ніж підтверджувати списання, дочекайтеся успішної операції PREAUTH.

```php
use AlliancePay\Sdk\Payment\Dto\Order\OrderRequestDTO;
use AlliancePay\Sdk\Payment\Order\CreateOrder;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

$orderData['merchantRequestId'] = GenerateRequestIdentification::generateRequestId();
$orderData['hppPayType'] = 'PREAUTH';
$orderData['paymentMethods'] = ['CARD'];
$order = (new CreateOrder())->createOrder(OrderRequestDTO::fromArray($orderData), $authDto);
$hppOrderId = $order->getHppOrderId();
$redirectUrl = $order->getRedirectUrl();
```

#### Поля `OrderRequestDTO` для резервування

| Поле                | Тип            | Опис                                                                                                                                                                                                                                                 |
| ------------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `merchantRequestId` | `string`       | Згенеруйте унікальний ID нового запиту через `GenerateRequestIdentification::generateRequestId()` і збережіть його у своєму застосунку.                                                                                                              |
| `hppPayType`        | `string`       | Передайте `PREAUTH`, щоб зарезервувати кошти на картці покупця.                                                                                                                                                                                      |
| `paymentMethods`    | `array`        | Для прикладу з банківською карткою передайте `['CARD']`.                                                                                                                                                                                             |
| `preAuthExpDate`    | `string\|null` | Строк дії резерву. Якщо пропустити поле, SDK v1.5.0 додасть до поточного часу 2 години й 30 секунд. Власне значення має бути в межах від 2 годин до 28 діб. Формат включає дату, час, дві цифри дробової частини секунди та зміщення часового поясу. |

### Підтвердження списання

#### Поля `OrderRequestCompletionDTO`

| Поле                  | Тип                 | Опис                                                                                                                                    |
| --------------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `merchantRequestId`   | `string`            | Згенеруйте унікальний ID нового запиту через `GenerateRequestIdentification::generateRequestId()` і збережіть його у своєму застосунку. |
| `merchantId`          | `string`            | Ідентифікатор мерчанта у вашому середовищі. Візьміть його з `$authDto->getMerchantId()`.                                                |
| `originalOperationId` | `string`            | Ідентифікатор успішного резервування. Візьміть `operationId` операції PREAUTH з перевіреного callback або з історії операцій.           |
| `coinAmount`          | `int`               | Сума списання в копійках гривні. SDK допускає відхилення до 20% в обидва боки від початкової суми PREAUTH.                              |
| `date`                | `DateTimeImmutable` | Дата й час запиту. У прикладі значення створює `DateTimeImmutableProvider::nowByTimezone()` для часового поясу Києва.                   |
| `notificationUrl`     | `string`            | HTTPS-адреса вашого сервера, на яку банк надсилає повідомлення про результат операції.                                                  |

Третім аргументом `createCompletion()` передайте початкову суму резерву `$originalCoinAmount` у копійках UAH. Цю суму SDK порівнює із запитаним списанням, зокрема й для замовлень у USD або EUR.

```php
use AlliancePay\Sdk\Payment\Dto\Order\OrderRequestCompletionDTO;
use AlliancePay\Sdk\Payment\Order\CreateOrderCompletion;
use AlliancePay\Sdk\Services\DateTime\DateTimeImmutableProvider;

$completion = OrderRequestCompletionDTO::fromArray([
    'merchantRequestId'   => GenerateRequestIdentification::generateRequestId(),
    'merchantId'          => $authDto->getMerchantId(),
    'originalOperationId' => $originalOperationId,
    'coinAmount'          => $originalCoinAmount,
    'date'                => DateTimeImmutableProvider::nowByTimezone(
        DateTimeImmutableProvider::KYIV_TIMEZONE
    ),
    'notificationUrl'     => 'https://shop.example/webhooks/alliancepay',
]);
$result = (new CreateOrderCompletion())->createCompletion(
    $completion, $authDto, $originalCoinAmount
);
$operation = $result->toArray();
```

SDK перевіряє допустиме відхилення ±20% від резерву. Наприклад, для `10000` копійок перевірку суми проходять значення від `8000` до `12000`. Банк окремо визначає результат списання. Збережіть його статус та `operationId`. Після тайм-ауту спочатку звірте операції за `hppOrderId`.
