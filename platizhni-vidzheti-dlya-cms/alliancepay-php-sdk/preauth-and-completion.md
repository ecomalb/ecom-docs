---
description: >-
  PREAUTH — двофазний платіж: спочатку кошти блокуються на картці покупця, а
  потім мерчант підтверджує списання через операцію COMPLETION.
---

# PreAuth and Completion

## Створення PreAuth

Для створення PREAUTH-замовлення використовуються ті самі класи, що й для звичайного `PURCHASE`; потрібно лише встановити `hppPayType` у значення `PREAUTH`.

#### Поле `preAuthExpDate` — термін дії блокування <a href="#pole-preauthexpdate-termin-diyi-blokuvannya" id="pole-preauthexpdate-termin-diyi-blokuvannya"></a>

| Сценарій           | Поведінка                                                             |
| ------------------ | --------------------------------------------------------------------- |
| Поле не передано   | SDK автоматично встановлює значення `now + 2 години`.                 |
| Поле передано явно | Значення має бути в діапазоні від `now + 2 години` до `now + 28 діб`. |

**Формат:** `YYYY-MM-DD HH:MM:SS.ss±HH:MM`, наприклад `2026-08-10 15:30:00.00+03:00`.

#### Приклад створення PREAUTH-замовлення <a href="#priklad-stvorennya-preauth-zamovlennya" id="priklad-stvorennya-preauth-zamovlennya"></a>

```php
use AlliancePay\Sdk\Payment\Order\CreateOrder;
use AlliancePay\Sdk\Payment\Dto\Order\OrderRequestDTO;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

$orderData = [
    'merchantRequestId' => GenerateRequestIdentification::generateRequestId(),
    'merchantId'        => $authDto->getMerchantId(),
    'hppPayType'        => 'PREAUTH',
    'directType'        => 'REDIRECT',
    'coinAmount'        => 10050,
    'paymentMethods'    => ['CARD'],
    'successUrl'        => '<redacted URL>',
    'failUrl'           => '<redacted URL>',
    'statusPageType'    => 'STATUS_TIMER_PAGE',
    'customerData'      => ['senderCustomerId' => 'customer_id_1'],
    // Опціонально: від +2 год до +28 діб від поточного часу.
    // 'preAuthExpDate' => '2026-08-10 15:30:00.00+03:00',
];

$orderRequest = OrderRequestDTO::fromArray($orderData);
$createOrder  = new CreateOrder();

try {
    $response      = $createOrder->createOrder($orderRequest, $authDto);
    $responseArray = $response->toArray();

    // Збережіть ці значення для COMPLETION.
    $hppOrderId  = $responseArray['hppOrderId'];
    $redirectUrl = $responseArray['redirectUrl'];
} catch (\AlliancePay\Sdk\Exceptions\CreateOrderException $e) {
    echo "Помилка створення PREAUTH: " . $e->getMessage();
} catch (\AlliancePay\Sdk\Exceptions\ValidateDataException $e) {
    echo "Помилка валідації: " . $e->getMessage();
}
```

Після успішного створення PREAUTH-замовлення збережіть у своїй системі `hppOrderId`, `operationId` та `coinAmount` з відповіді. Ці значення потрібні для COMPLETION.



## Completion (Завершення попередньої авторизації) <a href="#id-7.-completion-zavershennya-poperednoyi-avtorizaciyi" id="id-7.-completion-zavershennya-poperednoyi-avtorizaciyi"></a>

**COMPLETION** підтверджує та списує кошти, заблоковані операцією PREAUTH. Для цього використовуються клас `CreateOrderCompletion` і DTO `OrderRequestCompletionDTO`.

#### Ключові правила <a href="#klyuchovi-pravila" id="klyuchovi-pravila"></a>

* `originalOperationId` — це поле `operationId` з відповіді на PREAUTH, а не `ecomOperationId`.
* `coinAmount` — сума списання. Допускається відхилення **±20%** від оригінальної суми PREAUTH.
* Третій аргумент методу `createCompletion()` — оригінальна сума PREAUTH у копійках. SDK використовує її для внутрішньої перевірки діапазону ±20%.

#### Поля `OrderRequestCompletionDTO` <a href="#polya-orderrequestcompletiondto" id="polya-orderrequestcompletiondto"></a>

| Поле                  | Тип               | Опис                                                      |
| --------------------- | ----------------- | --------------------------------------------------------- |
| `merchantRequestId`   | string            | Унікальний ID запиту, генерується для кожного COMPLETION. |
| `merchantId`          | string            | Ідентифікатор мерчанта.                                   |
| `originalOperationId` | string            | `operationId` з відповіді на PREAUTH.                     |
| `coinAmount`          | int               | Сума списання в копійках (±20% від суми PREAUTH).         |
| `date`                | DateTimeImmutable | Дата й час виконання запиту.                              |
| `notificationUrl`     | string            | URL для webhook-сповіщення про результат.                 |

#### Приклад виконання COMPLETION <a href="#priklad-vikonannya-completion" id="priklad-vikonannya-completion"></a>

```php
use AlliancePay\Sdk\Payment\Order\CreateOrderCompletion;
use AlliancePay\Sdk\Payment\Dto\Order\OrderRequestCompletionDTO;
use AlliancePay\Sdk\Services\DateTime\DateTimeImmutableProvider;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

// Дані з БД після успішного PREAUTH.
$originalOperationId = 'OPERATION_ID_FROM_PREAUTH';
$originalCoinAmount  = 10050;

$completionData = [
    'merchantRequestId'   => GenerateRequestIdentification::generateRequestId(),
    'merchantId'          => $authDto->getMerchantId(),
    'originalOperationId' => $originalOperationId,
    'coinAmount'          => 10050,
    'date'                => DateTimeImmutableProvider::nowByTimezone(DateTimeImmutableProvider::KYIV_TIMEZONE),
    'notificationUrl'     => '<redacted URL>',
];

$completionDto    = OrderRequestCompletionDTO::fromArray($completionData);
$createCompletion = new CreateOrderCompletion();

try {
    $response      = $createCompletion->createCompletion($completionDto, $authDto, $originalCoinAmount);
    $responseArray = $response->toArray();

    // status, operationId, rrn, rrnPreauth та інші поля відповіді.
} catch (\AlliancePay\Sdk\Exceptions\CompletionAmountException $e) {
    echo "Помилка суми COMPLETION: " . $e->getMessage();
    print_r($e->getPayload());
} catch (\AlliancePay\Sdk\Exceptions\CreateCompletionException $e) {
    echo "Помилка COMPLETION: " . $e->getMessage();
    print_r($e->getPayload());
}
```

&#x20;



