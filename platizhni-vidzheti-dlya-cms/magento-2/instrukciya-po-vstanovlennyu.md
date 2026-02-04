# Інструкція по встановленню

Платіжний віджет Magento 2 :

{% file src="../../.gitbook/assets/magento2_alliance_pay_v1.0.0.zip" %}



{% stepper %}
{% step %}
### Створення необхідної структури папок&#x20;

```
mkdir -p app/code/Alliance/AlliancePay
```
{% endstep %}

{% step %}
### Завантажте/скопіюйте файли модуля в створену папку

```
Шлях має бути: app/code/Alliance/AlliancePay/registration.php
```
{% endstep %}

{% step %}
### Надайте правильні права доступу на файли (**опціонально**)

```
find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
```
{% endstep %}

{% step %}
### Встановіть залежності модуля

```
composer install
```
{% endstep %}

{% step %}
### Увімкніть модуль

```
php bin/magento module:enable Alliance_AlliancePay
```
{% endstep %}

{% step %}
### Оновіть систему

```
php bin/magento setup:upgrade
```
{% endstep %}

{% step %}
### Запустіть компіляцію

```
php bin/magento setup:di:compile
```
{% endstep %}

{% step %}
### Розгорніть статичні файли

```
php bin/magento setup:static-content:deploy -f
```
{% endstep %}

{% step %}
### Очистіть кеш

```
php bin/magento cache:flush
```
{% endstep %}
{% endstepper %}

### Технічні вимоги&#x20;

* Версія _**PHP**_ - 8.2
* Версія _**Magento 2**_ - 2.4
* Для дешифрування і комунікації з Ecom, платіжний модуль використовує наступну бібліотеку - [GitHub - kelvinmo/simplejwt: A simple JSON web token library written in PHP.](https://github.com/kelvinmo/simplejwt) , яка вбудована в сам модуль
* На сервері повинно бути ввімкнено розширення для _**PHP**_, **`gmp`, `hash`, `openssl`, `sodium`** \[для роботи бібліотеки `simplejwt`]
* Для отримання необхідного коду країни у форматі `ISO3166` потрібно встановити бібліотеку [league/iso3166](https://packagist.org/packages/league/iso3166) версія 4.3.3

<br>
