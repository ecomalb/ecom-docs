# Встановлення

{% embed url="https://github.com/alliancedigital-tech/alliancepay-php-sdk/releases" %}

### Технічні вимоги <a href="#tekhnichni-vimogi" id="tekhnichni-vimogi"></a>

Перед початком роботи переконайтеся, що ваше серверне середовище відповідає наступним вимогам:

* **PHP:** версія `8.0` або вище.
* **Composer:** для керування залежностями.
* **Обов'язкові розширення PHP:**
  * `sodium`
  * `hash`
  * `gmp`
  * `openssl`

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
