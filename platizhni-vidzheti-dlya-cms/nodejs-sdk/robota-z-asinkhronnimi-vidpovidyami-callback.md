# Робота з асинхронними відповідями Callback

Для автоматичної обробки повідомлень від платіжного шлюзу використовуйте метод `handleCallback`.

Він бере на себе перевірку валідності даних та їх дешифрування.



**Приклад використання (Express.js):**

```
app.post('/api/payment/callback', async (req, res) => {
    try {
        // Очікується, що req.body вже є розпарсеним JSON об'єктом
        const callbackDto = await client.handleCallback(req.body);
        
        if (callbackDto.orderStatus === 'SUCCESS') {
            // Обробіть успішний платіж у вашій системі
            console.log('Payment successful for order:', callbackDto.ecomOrderId);
        }
        
        // Повертаємо 200 OK сервісу AlliancePay
        res.status(200).send('OK');
    } catch (error) {
        // Логування помилки та відповідь з помилкою
        console.error('Callback handling error:', error);
        res.status(400).send('Error');
    }
});
```
