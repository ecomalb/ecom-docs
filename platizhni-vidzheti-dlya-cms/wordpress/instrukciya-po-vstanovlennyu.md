# Інструкція по встановленню

Платіжний віджет WordPress:

{% embed url="https://github.com/alliancedigital-tech/alliancepay-woocommerce/releases" %}

1.  Завантажте архів плагіна й встановіть через _Плагіни → Додати новий → Завантажити плагін_.<br>

    <figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>
2. Активуйте плагін.
3. У меню Адмін‑панелі з’явиться пункт **AlliancePay**
4.  Потім перейдіть в налаштування Woocommerce і активуйте плагін. (скрін 2) woocommerce->settings->payments<br>

    <figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>
5. На сторінці оплати повинен бути шорткод \[woocommerce\_checkout]



## Вимоги

* WordPress 6.8.2+ (PHP 8.0+; рекомендовано PHP 8.2+; PHP-розширення: gmp, hash, openssl, sodium).
* WooCommerce version: 10.1.0 +
* Адміністративні права для доступу до плагіна.
* Параметри Авторизації 2.0: Merchant ID, приватний RSA-ключ для JWS у форматі PKCS#8 PEM і JWS Key ID (kid). Відкритий ключ потрібно зареєструвати в АТ «БАНК АЛЬЯНС».
* Синхронізований системний час сервера для перевірки часової мітки JWS та коректний часовий пояс WordPress для відображення дат.

### **Вимоги до серверу де встановлювати платіжний модуль**

* Для дешифрування і комунікації з ECOM, платіжний модуль використовує наступну бібліотеку - [GitHub - kelvinmo/simplejwt: A simple JSON web token library written in PHP.](https://github.com/kelvinmo/simplejwt) , яка вбудована в сам модуль
* На сервері повинно бути ввімкнено розширення для пхп - `gmp` **\[для роботи бібліотеки simplejwt]**
* На сервері повинно бути ввімкнено розширення для пхп - `hash` **\[для роботи бібліотеки simplejwt]**
* На сервері повинно бути ввімкнено розширення для пхп - `openssl` **\[для роботи бібліотеки simplejwt]**
* На сервері повинно бути ввімкнено розширення для пхп - `sodium` **\[для роботи бібліотеки simplejwt]**
