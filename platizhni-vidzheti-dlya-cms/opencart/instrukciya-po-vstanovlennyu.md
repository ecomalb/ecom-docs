# Інструкція по встановленню

### Платіжний віджет OpenCart:&#x20;

{% tabs %}
{% tab title="OpenCart 3.0" %}
{% file src="../../.gitbook/assets/alliance.ocmod.zip" %}
{% endtab %}

{% tab title="OpenCart 4.0" %}
{% file src="../../.gitbook/assets/alliance.ocmod (1).zip" %}
{% endtab %}
{% endtabs %}

## Покрокова інструкція, встановлення платіжного віджета:&#x20;

### 1.  В адмінці "OpenCart" в розділі “Extensions“ -> "Installer" потрібно завантажити архів, що вказаний вище

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

### 2. В розділі “Extensions“ -> "Extensions' потрібно активувати і налаштувати модуль

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## Вимоги до серверу де встановлювати платіжний модуль

1. Платіжний модуль розроблено тільки для версії OpenCart 4.X. Тобто версія повинна бути 4.0.0 або вище (особисто я розробляв і тестував на версії 4.1.0.0)
2. Версія php 8.0 або вище
3. Для дешифрування і комунікації з ЕКом платіжний модуль використовує наступну бібліотеку - [GitHub - kelvinmo/simplejwt: A simple JSON web token library written in PHP.](https://github.com/kelvinmo/simplejwt) , яка вбудована в сам модуль
4. На сервері повинно бути ввімкнено розширення для пхп - **gmp** \[для роботи бібліотеки simplejwt]
5. На сервері повинно бути ввімкнено розширення для пхп - **hash** \[для роботи бібліотеки simplejwt]
6. На сервері повинно бути ввімкнено розширення для пхп - **openssl** \[для роботи бібліотеки simplejwt]
7. На сервері повинно бути ввімкнено розширення для пхп - **sodium** \[для роботи бібліотеки simplejwt]
8. GuzzleHttp потребує модуль. В Opencart 4.1.0 він наче йде з коробки але потрібно це тестувати на різних версіях
