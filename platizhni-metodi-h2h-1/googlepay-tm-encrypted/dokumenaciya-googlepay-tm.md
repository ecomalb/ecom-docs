# Докуменація GooglePay™

## Етап 1. **Ознайомлення**

Перед початком роботи з Google Pay™ API варто детально ознайомитися з офіційною документацією. Вона містить вимоги до використання сервісу, керівництва з інтеграції та контрольний список для перевірки коректності підключення.

1.  [Для розробників мобільних додатків](https://developers.google.com/pay/api/android/overview): містить інформацію про правила використання Google Pay™ API, бренду Google Pay™, [посібник користувача ](https://developers.google.com/pay/api/android/guides/brand-guidelines?hl=ru)та [контрольний список інтеграції](https://developers.google.com/pay/api/android/guides/test-and-deploy/integration-checklist?hl=ru).


2. [Для розробників вебсайтів](https://developers.google.com/pay/api/web/overview?authuser=0): включає правила застосування Google Pay™ API та його брендовані елементи, [посібник користувача](https://developers.google.com/pay/api/web/guides/brand-guidelines?hl=ru) та [контрольний список інтеграції](https://developers.google.com/pay/api/web/guides/test-and-deploy/integration-checklist?hl=ru).

[Для коректної інтеграції Google Pay™  API та отримання PaymentData ](https://developers.google.com/pay/api/web/guides/tutorial?authuser=0\&hl=ru)у ваш сайт або додаток необхідно:

* Використовувати вебсторінку з HTTPS-протоколом і дійсним TLS-сертифікатом.
* Налаштувати параметри:
  * allowPaymentMethods : CARD
  * tokenizationSpecification = { "type": "PAYMENT\_GATEWAY" }
  * allowedCardNetworks = \['MASTERCARD', 'VISA']
  * allowedCardAuthMethods = \['PAN\_ONLY', 'CRYPTOGRAM\_3DS']
  * gateway = timeproject
  * gatewayMerchantId — унікальний ідентифікатор магазину, що видається при підключенні до платіжного шлюзу AllianceBank.

3DS-верифікація для PAN\_ONLY виконується за замовчуванням.

## Етап 2. **Інтеграція вашого сайту або додатка з** Google Pay™ API **з платіжним шлюзом Alliance Bank**

Якщо інтеграція виконана коректно, на сторінці вашого сайту або у додатку відобразиться кнопка оплати. При натисканні користувач побачить спливаюче вікно з вибором картки, прив'язаної до облікового запису Google™.

**Приклад параметрів, які повертає Google Pay™ API описані в запиті:** [**Запит проведення платежу** ](https://app.gitbook.com/o/zBSkiJ3Oy2kvtv30JbMh/s/djW26z83WQoOq0ZjunWw/~/changes/129/platizhni-metodi-h2h/googlepay-encrypted/zapit-provedennya-platezhu)

## Етап 3. Активація способу оплати Google Pay™ для магазину та користувача&#x20;

* Якщо ваш інтернет-магазин вже інтегрований з Alliance Bank, зверніться до менеджера або напишіть запит на email: <mark style="color:orange;">`ecom.support@bankalliance.ua`</mark>
* Якщо інтеграція з Alliance Bank ще не виконана, також зверніться за вказаною електронною адресою <mark style="color:orange;">`ecom.support@bankalliance.ua`</mark>

## Етап 4. Обробка даних із параметру **"token"**

Є два способи обробки отриманого `token`:

1. **Розшифровка на стороні магазину** — дані розшифровуються перед передачею в Alliance Bank.
2. **Розшифровка на стороні Alliance Bank** — дані у незмінному вигляді передаються до Alliance Bank.

Для розшифровки [paymentData](https://developers.google.com/pay/api/web/guides/tutorial) Google™ рекомендує використовувати бібліотеку [**Tink**](https://github.com/google/tink).

[Опис використання бібілотеки Tink](https://developers.google.com/pay/api/processors/guides/implementation/using-tink)

## Етап 5. Перевірте відповідність інтеграціі по чек листу

* Ознайомтесь з [контрольним списком](https://developers.google.com/pay/api/web/guides/test-and-deploy/integration-checklist) та переконайтесь що всі етапи інтеграції сторінки оплати виконані.
* Ознайомтесь з [контрольним списком](https://developers.google.com/pay/api/web/guides/test-and-deploy/integration-checklist) і переконайтесь, що інтеграція Android-додатку відповідає вимогам.

## Етап 6. Запит доступу до робочої версії від спеціалістів Googl&#x65;**™**

* Подайте запит на доступ [для сайту](https://developers.google.com/pay/api/web/guides/test-and-deploy/request-prod-access?hl=ru).
* Подайте запит на доступ [для Android-додатку](https://developers.google.com/pay/api/android/guides/test-and-deploy/request-prod-access?hl=ru).

***

***

