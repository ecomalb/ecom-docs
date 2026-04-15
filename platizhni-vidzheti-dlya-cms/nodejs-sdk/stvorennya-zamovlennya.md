# Створення замовлення

Для створення платежу використовуйте метод `createOrder`.

SDK автоматично додає ваш `merchantId` та генерує унікальний `merchantRequestId` для кожного запиту.



**Приклад коду:**

```
const orderData = {
    coinAmount: 10050, // Сума в копійках
    hppPayType: 'PURCHASE',
    paymentMethods: ['CARD', 'APPLE_PAY', 'GOOGLE_PAY'],
    successUrl: '[https://your-site.com/success](https://your-site.com/success)',
    failUrl: '[https://your-site.com/fail](https://your-site.com/fail)',
    statusPageType: 'STATUS_TIMER_PAGE',
    customerData: { senderCustomerId: 'customer_id_1' },
};

try {
    const response = await client.createOrder(orderData);
    console.log('Redirect to payment:', response.redirectUrl);
} catch (error) {
    console.error('Order creation failed:', error);
}
```
