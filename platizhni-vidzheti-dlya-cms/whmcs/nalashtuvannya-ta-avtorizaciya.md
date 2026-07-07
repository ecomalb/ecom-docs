# Налаштування та авторизація

### Активація модуля в адмін-панелі <a href="#id-2.-aktivaciya-modulya-v-admin-paneli" id="id-2.-aktivaciya-modulya-v-admin-paneli"></a>

Після встановлення модуля, у вкладенці "Addons", перейти на сторінку "Apps & Integrations"

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Перехід на вкладку "Browse" та вибираємо з категорій "Payments"

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

В розділі "Additional apps" знайти плагін AlliancePay Payment Gateway

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Активувати плагін&#x20;

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Налаштування параметрів <a href="#id-3.-nalashtuvannya-parametriv" id="id-3.-nalashtuvannya-parametriv"></a>

Після активації вас автоматично перекине на вкладку **Manage Existing Gateway** де потрібно буде заповнити необхідні поля :&#x20;

<figure><img src="../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

Опис полів :&#x20;

<table><thead><tr><th>Назва</th><th>Опис</th><th>Приклад</th></tr></thead><tbody><tr><td>Show on Order Form</td><td>Перемикач для відображення платіжного метода на сторінці</td><td>Можливі значення : <br>"Так" або "Ні"</td></tr><tr><td>Display Name</td><td>Назва платіжного метода на сторінці оплати</td><td>AlliancePay Bank</td></tr><tr><td>API Base URL</td><td>URL на який будуть надходити API запити </td><td>Потрібно вказати : <br><a href="https://api-ecom-prod.bankalliance.ua"><code>https://api-ecom-prod.bankalliance.ua</code></a></td></tr><tr><td>Payment Type</td><td>Тип платежу<br>При роботі зі звичайною платіжною сторінкою потрібно обирати "PURCHASE"<br>При роботі з переказом між рахунками потрібьно обирати "A2A"</td><td>Можливі значення : <br>- PURCHASE<br>- A2A</td></tr><tr><td>Status Page Type</td><td>Визначає як буде виглядати сторінка після виконання оплати</td><td><p></p><p>Можливі значення : <br></p><ul><li><code>STATUS_TIMER_PAGE</code> - сторінка за замовчуванням, якщо мерчант не обрав бажаний тип, таймер редірект автоматично 1 хвилина відображення статус сторінки з автоматичним редіректом юзера на сайт мерчанта (редірект урл)</li><li><code>STATUS_REDIRECT_MERCHANT_PAGE</code> - одразу редірект на урл мерчанта</li><li><code>STATUS_PAGE</code> - редірект, на нашу статус сторіншку (завантажити квитанцію …)</li></ul></td></tr><tr><td>Merchant ID</td><td>Унікальний ідентифікатор мерчанта</td><td>9a337b2b-4d97-4abe-9f95-cde229f9bd83</td></tr><tr><td>Service Code</td><td>Унікальний ідентифікатор для авторизації</td><td>d86a0f72-0dfe-4102-ace7-78997d042b7f</td></tr><tr><td>Authentication Key</td><td>Приватний ключ, потрібен для виконання авторизації</td><td><p>Його потрібно згенерувати самостійно за <a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">інструкцією</a> та надати співробітнику банку</p><p>Приклад : </p><pre class="language-json"><code class="lang-json">{
    "kty": "EC",
    "d": "nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8",
    "use": "enc",
    "crv": "P-384",
    "x": "dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn",
    "y": "qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X",
    "alg": "ECDH-ES+A256KW"
}
</code></pre></td></tr></tbody></table>

{% hint style="warning" %}
Для кожного типу платежу реєструється унікальний термінал, що призначений для виконання конкретних операції \
Тому для A2A будуть інші значення `Merchant ID` та `Service Code`
{% endhint %}



Після заповнення всіх полів, потрібно натиснути на кнопку "Save Changes"

### Налаштування конвертації <a href="#id-4.-nalashtuvannya-konvertaciyi" id="id-4.-nalashtuvannya-konvertaciyi"></a>

Оскільки банк AlliancePay приймає платежі виключно у **гривні (UAH)**, необхідно правильно налаштувати поведінку системи, якщо ваша базова валюта відмінна від гривні (наприклад, USD).

{% hint style="warning" %}
Якщо в системі дефолтна валюта сайта гривня то додатково нічого робити не потрібно, якщо дефолтна валюта USD або EUR тоді в полі **Convert To For Processing** виставляємо UAH (Валюта має бути налаштована в System Settings → Currencies).&#x20;

<img src="../../.gitbook/assets/image (7).png" alt="" data-size="original">

<img src="../../.gitbook/assets/image (8).png" alt="" data-size="original">


{% endhint %}



1. Знайдіть поле **Convert To For Processing**.
2. У випадаючому списку виберіть **UAH**.
3. Це налаштування змусить WHMCS автоматично перераховувати суму інвойсу за внутрішнім курсом перед відправкою клієнта на сторінку оплати.

### Завершення налаштування <a href="#id-5.-zavershennya-nalashtuvannya" id="id-5.-zavershennya-nalashtuvannya"></a>

1. Натисніть кнопку **Save Changes** (Зберегти зміни).
2. Після збереження внизу сторінки в розділі **Usage Notes** (Інформація про сесію) має з’явитися статус підключення. Якщо дані заповнені вірно, система відобразить інформацію про активну сесію та токени.
