# Перевірка стану замовлення

Якщо вам потрібно вручну перевірити поточний стан транзакції

(наприклад, за кроном або якщо користувач закрив сторінку оплати),

використовуйте метод \`checkOrderData\` з передачею `hppOrderId`.<br>

**Приклад перевірки статусу:**

```
try {
    const orderData = await client.checkOrderData('HPP_ORDER_ID_HERE');
    
    console.log('Current order status:', orderData.orderStatus);
    console.log('Operations history:', orderData.operations); // Масив усіх спроб оплати та повернень
} catch (error) {
    console.error('Status check failed:', error);
}
```
