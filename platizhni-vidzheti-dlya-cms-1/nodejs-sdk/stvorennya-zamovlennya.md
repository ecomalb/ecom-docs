# Створення замовлення

Для створення платежу використовуйте метод `createOrder`.

SDK автоматично додає ваш `merchantId` та генерує унікальний `merchantRequestId` для кожного запиту.

{% hint style="info" %}
Детальніше про опис параметрів масиву `orderData` можна ознайомитись тут :  [Створення замовлення HPP](https://docs.merchant.alb.ua/platizhni-metodi-hpp/stvorennya-zamovlennya/stvorennya-zamovlennya)
{% endhint %}

**Приклад коду:**

```javascript
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

>
>
> **A2A платіж:** Якщо `hppPayType` = `A2A`, необхідно змінити наступні параметри:
>
> * `'directType'` => `'BANK_LINK'` _(для hppPayType PURCHASE використовується `'REDIRECT'`)_
> * `'priorityBankCode'` => `'ALL_BANKS'`
> * `'merchantComment'` => `'Comment for merchant'` _(обов'язково для A2A)_
