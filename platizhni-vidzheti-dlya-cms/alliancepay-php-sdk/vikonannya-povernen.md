# Повернення коштів (Refund)

Для виконання операції повернення коштів використовується клас `AlliancePay\Sdk\Payment\Refund\RefundOrder`. Ви можете ініціювати як повне, так і часткове повернення, передавши відповідну суму в DTO.

#### Приклад виконання Refund : <a href="#priklad-vikonannya-refund" id="priklad-vikonannya-refund"></a>

Для роботи знадобляться допоміжні сервіси SDK для генерації ID запиту та роботи з часом.

```php
use AlliancePay\Sdk\Payment\Refund\RefundOrder;
use AlliancePay\Sdk\Payment\Dto\Refund\RefundRequestDTO;
use AlliancePay\Sdk\Services\DateTime\DateTimeImmutableProvider;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

// 1. Ініціалізація сервісу повернення
$refundService = new RefundOrder();

// 2. Підготовка даних (приклад для масиву даних)
$refundData = [
    'merchantRequestId' => GenerateRequestIdentification::generateRequestId(),
    'merchantId' => $authDto->getMerchantId(),
    'operationId' => 'OPERATION_ID', // ID успішної операції по створенню замовлення.
    'coinAmount' => 100, // Сума повернення в копійках
    'date' => DateTimeImmutableProvider::fromString('now', DateTimeImmutableProvider::KYIV_TIMEZONE),
];

// 3. Виконання запитів
try {
    $refundDto = RefundRequestDTO::fromArray($refundData);
        
    // Виклик методу createRefund (потрібен збережений $authDto)
    $resultRefund = $refundService->createRefund($refundDto, $authDto);
} catch (\AlliancePay\Sdk\Exceptions\RefundOrderException $exception) {
    // Обробка помилок (наприклад, недостатньо коштів або невірний ID операції)
    echo "Помилка повернення: " . $exception->getMessage();
}
```
