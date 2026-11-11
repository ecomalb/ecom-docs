# Виконання повернень

Метод \`createRefund\` автоматично формує дату у потрібному форматі та ініціює запит на повернення коштів.

Ви можете ініціювати як повне, так і часткове повернення.

**Приклад виконання Refund:**

```
try {
    const refundResponse = await client.createRefund({
        operationId: 'ORIGINAL_OPERATION_ID', // ID успішної операції по створенню замовлення
        coinAmount: 500, // Сума повернення в копійках
        merchantComment: 'Повернення товару клієнтом'
    });
    console.log('Refund status:', refundResponse.status);
} catch (error) {
    console.error('Refund failed:', error);
}
```
