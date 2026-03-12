# Створення замовлення

Для створення платежу необхідно використовувати раніше збережений об'єкт `AuthorizationDTO` та підготувати дані замовлення через `OrderRequestDTO`.

{% hint style="info" %}
Детальніше про опис параметрів масиву `orderData` можна ознайомитись тут :  [Створення замовлення HPP](https://docs.merchant.alb.ua/platizhni-metodi-hpp/stvorennya-zamovlennya/stvorennya-zamovlennya)
{% endhint %}

#### Приклад коду для створення замовлення: <a href="#priklad-kodu-dlya-stvorennya-zamovlennya" id="priklad-kodu-dlya-stvorennya-zamovlennya"></a>

```php
use AlliancePay\Sdk\Payment\Dto\Order\OrderRequestDTO;
use AlliancePay\Sdk\Payment\Services\OrderService;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

// 1. Готуємо дані замовлення
$orderData = [
    'merchantRequestId' => GenerateRequestIdentification::generateRequestId(),
    'merchantId' => $authDto->getMerchantId(),
    'hppPayType' => 'PURCHASE',
    'coinAmount' => 10050,
    'paymentMethods' => ['CARD', 'APPLE_PAY', 'GOOGLE_PAY'],
    'successUrl' => 'https://your-site.com/success',
    'failUrl' => 'https://your-site.com/fail',
    'statusPageType' => 'STATUS_TIMER_PAGE',
    'customerData' => ['senderCustomerId' => 'customer_id_1'],
];

// 2. Створюємо DTO об'єкт
$orderRequest = OrderRequestDTO::fromArray($orderData);

// 3. Створюємо OrderService
$orderService = new OrderService();
// Створюємо замовлення
/**
 * $orderRequestDto -> AlliancePay\Sdk\Payment\Dto\Order\OrderRequestDTO
 * $authDto -> AlliancePay\Sdk\Services\Authorization\Dto\AuthorizationDTO
 */
try {
    $response = $orderService->createOrder($orderRequest, $authDto);
} catch (\AlliancePay\Sdk\Exceptions\CreateOrderException $exception) {
    // 
}
```

