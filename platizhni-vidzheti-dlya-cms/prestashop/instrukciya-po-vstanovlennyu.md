# Інструкція по встановленню

### Платіжний віджет PrestaShop:

{% file src="../../.gitbook/assets/prestashop-alliancepay-v.1.0.0.zip" %}



{% stepper %}
{% step %}
### Завантажте архів з плагіном та встановіть&#x20;

Відкрийте _"Модулі" → "Менеджер модулів"_

<figure><img src="../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

_Натисність "Завантажити модуль"_ та виберіть архів

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;
{% endstep %}

{% step %}
### Активація модулю

Оберіть категорію "Оплата"

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Повинен відобразитись модуль з назвою "AlliancePay v1.0.0 – Alliance Dgtl."

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Потрібно обрати модуль та натиснути "Увімкнути"

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

### Вимоги до серверу де встановлювати платіжний модуль <a href="#vimogi-do-serveru-de-vstanovlyuvati-platizhnii-modul" id="vimogi-do-serveru-de-vstanovlyuvati-platizhnii-modul"></a>

1. Версія PHP 7.4 або вище
2. Для дешифрування і комунікації з Ecom, платіжний модуль використовує наступну бібліотеку - [GitHub - kelvinmo/simplejwt: A simple JSON web token library written in PHP.](https://github.com/kelvinmo/simplejwt) , яка вбудована в сам модуль
3. На сервері повинно бути ввімкнено розширення для пхп - **gmp** \[для роботи бібліотеки simplejwt]
4. На сервері повинно бути ввімкнено розширення для пхп - **hash** \[для роботи бібліотеки simplejwt]
5. На сервері повинно бути ввімкнено розширення для пхп - **openssl** \[для роботи бібліотеки simplejwt]
6. На сервері повинно бути ввімкнено розширення для пхп - **sodium** \[для роботи бібліотеки simplejwt]

