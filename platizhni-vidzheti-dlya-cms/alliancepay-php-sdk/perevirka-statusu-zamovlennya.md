# Перевірка статусу замовлення

Якщо вам потрібно вручну перевірити поточний стан транзакції (наприклад, за кроном або якщо користувач закрив сторінку оплати), використовуйте клас `AlliancePay\Sdk\Payment\Order\CheckOrderData`.

#### Приклад перевірки статусу: <a href="#priklad-perevirki-statusu" id="priklad-perevirki-statusu"></a>

Для перевірки достатньо мати `hppOrderId` та об'єкт авторизації.

```php
use AlliancePay\Sdk\Payment\Order\CheckOrderData;

// 1. Ініціалізація сервісу перевірки
$checkService = new CheckOrderData();

// 2. Виклик методу перевірки
// Перший аргумент - ідентифікатор замовлення hppOrderId
// Другий аргумент - ваш збережений об'єкт AuthorizationDTO
try {
    /** @var AlliancePay\Sdk\Payment\Dto\Order\OrderDataResponseDTO $orderStatus */
    $orderStatus = $checkService->checkOrderData('HPP_ORDER_ID', $authDto);
} catch (\Exception $e) {
    echo "Помилка при перевірці статусу: " . $e->getMessage();
}
```
