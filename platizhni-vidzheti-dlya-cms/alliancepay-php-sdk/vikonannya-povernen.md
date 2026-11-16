# Виконання повернень

Повернення прив’язане до успішного списання. Якщо у вас є лише `hppOrderId`, спочатку відкрийте історію операцій цього замовлення.

### Повернення коштів

#### Поля `RefundRequestDTO` у прикладі

| Поле                | Тип                 | Опис                                                                                                                               |
| ------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `merchantRequestId` | `string`            | Згенеруйте унікальний ID нового запиту на повернення й збережіть його до звернення до банку.                                       |
| `merchantId`        | `string`            | Ідентифікатор мерчанта. Візьміть його з `$authDto->getMerchantId()`.                                                               |
| `operationId`       | `string`            | Ідентифікатор успішного списання, за яким повертаєте кошти. Візьміть його з перевіреного callback або історії операцій замовлення. |
| `coinAmount`        | `int`               | Сума повернення в копійках UAH, зокрема й для валютного платежу. Наприклад, `100` означає 1,00 грн.                                |
| `date`              | `DateTimeImmutable` | Дата й час формування запиту. У прикладі використано поточний час у Києві.                                                         |

У прикладі нижче мерчант повертає 1,00 грн.

```php
use AlliancePay\Sdk\Payment\Dto\Refund\RefundRequestDTO;
use AlliancePay\Sdk\Payment\Refund\RefundOrder;
use AlliancePay\Sdk\Services\DateTime\DateTimeImmutableProvider;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

$refund = RefundRequestDTO::fromArray([
    'merchantRequestId' => GenerateRequestIdentification::generateRequestId(),
    'merchantId'        => $authDto->getMerchantId(),
    'operationId'       => $operationId,
    'coinAmount'        => 100,
    'date'              => DateTimeImmutableProvider::nowByTimezone(
        DateTimeImmutableProvider::KYIV_TIMEZONE
    ),
]);
$result = (new RefundOrder())->createRefund($refund, $authDto);
```

### Повернення за валютною операцією

Для повного повернення звірте гривневу суму початкової операції та попередні повернення. Для часткового повернення використовуйте погоджену суму за курсом вихідної операції. Наприклад, 10,00 USD за курсом 39,50 грн/USD відповідають `39500` копійкам.

Якщо відповідь втрачено після надсилання запиту, спочатку перевірте операції замовлення. Перед наступним поверненням звірте залишок, доступний до повернення.
