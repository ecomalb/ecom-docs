# Авторизація

Для початку роботи необхідно ініціалізувати сесію авторизації. Для цього використовується клас `AuthorizationService`.

#### Приклад ініціалізації: <a href="#priklad-inicializaciyi" id="priklad-inicializaciyi"></a>

```php
use AlliancePay\Sdk\Services\Authorization\AuthorizationService;

$authService = new AuthorizationService();

$config = [
    'baseUrl' => 'https://api-ecom-prod.bankalliance.ua/', // Базовий URL сервісу надається банком
    'merchantId' => 'YOUR_MERCHANT_ID', // Надається банком
    'serviceCode' => 'YOUR_SERVICE_CODE', // Надається банком
    'authenticationKey' => 'YOUR_AUTH_KEY' // Надається банком
];

/** @var \AlliancePay\Sdk\Services\Authorization\Dto\AuthorizationDTO $authDto */
$authDto = $authService->initAuthorization($config);

// ВАЖЛИВО: Отриманий об'єкт $authDto необхідно зберегти у вашій базі даних.
// Він містить токени (authToken, refreshToken) та термін їх дії, 
// які будуть потрібні для всіх наступних запитів.
```

### **ВАЖЛИВО:**

#### Приклад збереження та відновлення обʼєкту авторизації `AuthorizationDTO`. <a href="#priklad-zberezhennya-ta-vidnovlennya-ob-yektu-avtorizaciyi-authorizationdto" id="priklad-zberezhennya-ta-vidnovlennya-ob-yektu-avtorizaciyi-authorizationdto"></a>

```php
// Отримання окремих параметрів обʼєкту якщо планується зберігати як окрему сутність.
    $baseUrl = $authDto->getBaseUrl();
    $merchantId = $authDto->getMerchantId();
    $serviceCode = $authDto->getServiceCode();
    $authenticationKey = $authDto->getAuthenticationKey();
    $refreshToken = $authDto->getRefreshToken();
    $authToken = $authDto->getAuthToken();
    $deviceId = $authDto->getDeviceId();
    $serverPublic = $authDto->getServerPublic();
    $tokenExpirationDateTime = $authDto->getTokenExpirationDateTime();

// або через JSON, якщо збереження відбувається в JSON строці
$jsonAuth = json_encode($authDto->toArray()); 

// Приклад відновлення
$authDto = AuthorizationDTO::fromArray(json_decode($jsonFromDb, true));
```

#### Робота з авторизаційними даними. <a href="#robota-z-avtorizaciinimi-danimi" id="robota-z-avtorizaciinimi-danimi"></a>

Якщо у вас є збережені авторизаційні дані вам потрібно відновити обʼєкт авторизації по вище описаному прикладу.

Важливо памʼятати якщо термін дії технічної сессії завершився тоді метод `initAuthorization()` оновить дані в обʼєкті (відбудеться запит і оновлення сесії) та його потрібно зберегти в своїй системі.

#### Структура об'єкта AuthorizationDTO: <a href="#struktura-obyekta-authorizationdto" id="struktura-obyekta-authorizationdto"></a>

**Після успішного виклику ви отримаєте об'єкт з наступними даними:**

* `baseUrl`, `merchantId`, `serviceCode`, `authenticationKey` — ваші конфігураційні дані.
* `authToken` — токен для поточних запитів.
* `refreshToken` — токен для оновлення авторизації.
* `deviceId`, `serverPublic` — технічні ідентифікатори.
* `tokenExpirationDateTime` — об'єкт DateTimeImmutable з часом закінчення дії токена.

Збережений об'єкт `AuthorizationDTO` є обов'язковим аргументом для виконання інших операцій в API:

* **create-order** `(/ecom/execute_request/hpp/v1/create-order)`: Створення нових платежів.
* **refund** `(/ecom/execute_request/payments/v3/refund)`: Повернення коштів.
* **operations** `(/ecom/execute_request/hpp/v1/operations)`: Перевірка статусу транзакцій.
