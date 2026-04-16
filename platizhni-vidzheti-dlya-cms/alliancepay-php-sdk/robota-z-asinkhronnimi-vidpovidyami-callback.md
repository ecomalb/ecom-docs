# Обробка зворотних викликів (Callback/Webhook)

Для автоматичної обробки повідомлень від платіжного шлюзу (Webhooks) використовуйте `CallbackHandler`. Це дозволяє вашій системі дізнатися про успішну оплату в реальному часі.

**Важливо:**

Якщо ваша система має змогу отримати тіло запиту та серіалізувати JSON в масив тоді слід передавати в метод `handle()` другий параметр `$payload`. Якщо ні то метод `handle()` автоматично отримає тіло `php://input`

```php
$bodyJson = file_get_contents('php://input');
$payload = json_decode($bodyJson, true);
```

**Приклад використання :**

```php
use AlliancePay\Sdk\Payment\Callback\CallbackHandler;
use AlliancePay\Sdk\Payment\Dto\Callback\CallbackDTO;

// Отримуємо сирі дані від AlliancePay (JSON)
$bodyJson = file_get_contents('php://input');
$payload = json_decode($bodyJson, true);

$callbackHandler = new CallbackHandler();

try {
    // Обробка вхідних даних з перевіркою підпису
    /** @var CallbackDTO $callback */
    $callback = $callbackHandler->handle($authDto, $payload);
    
    // Якщо обробка успішна, повертаємо 200 OK сервісу AlliancePay
    http_response_code(200);
    echo 'OK';
} catch (\Exception $e) {
    // Логування помилки та відповідь з помилкою
    http_response_code(400);
    echo 'Error';
}
```
