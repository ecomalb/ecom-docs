# Встановлення

Інструкція для релізу v1.5.0. Підготуйте PHP 8.0 або новішої версії та Composer. Пакет вимагає розширення `curl` і `json`. Для підпису RS256 і перевірки підписів банку переконайтеся, що криптографічна бібліотека підтримує потрібні алгоритми у вашому середовищі.

### Встановлення через Composer

Виконайте команди в корені застосунку. Перша додає офіційний репозиторій, друга встановлює пакет під назвою з його `composer.json`.

```bash
composer config repositories.alliancepay vcs https://github.com/alliancedigital-tech/alliancepay-php-sdk
composer require alliance/alliancepay-payment-sdk:1.5.0
composer check-platform-reqs
composer show alliance/alliancepay-payment-sdk
```

### Перевірка автозавантаження

Якщо застосунок ще не підключає автозавантажувач Composer, додайте його у точці входу. Для скрипта, розташованого в корені проєкту, перевірка виглядає так.

```php
require __DIR__ . '/vendor/autoload.php';

if (!class_exists(\AlliancePay\Sdk\Services\Authorization\Dto\AuthorizationDTO::class)) {
    throw new RuntimeException('Перевірте встановлення SDK та шлях до vendor/autoload.php.');
}
```

Потім перейдіть до сторінки «Авторизація» та підготуйте конфігурацію мерчанта. Вимоги й вихідний код можна звірити з [маніфестом v1.5.0](https://github.com/alliancedigital-tech/alliancepay-php-sdk/blob/v1.5.0/composer.json) та [релізами SDK](https://github.com/alliancedigital-tech/alliancepay-php-sdk/releases).
