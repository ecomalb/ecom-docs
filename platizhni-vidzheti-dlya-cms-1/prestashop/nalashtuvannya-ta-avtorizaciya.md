# Налаштування та авторизація

{% stepper %}
{% step %}
### Переходимо в налаштування модулю&#x20;

Потрібно натиснути "Налаштувати"&#x20;

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Початкові налаштування&#x20;

Більшість полів до заповнення буде надано банком.&#x20;

#### Сторінка налаштувань :&#x20;

<figure><img src="../../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

#### Опис полів:&#x20;

{% hint style="info" %}
**Обов'язково, всі поля повинні бути заповнені, щоб платіжний плагін працював правильно**
{% endhint %}

<table><thead><tr><th>Назва</th><th>Опис</th><th>Приклад</th></tr></thead><tbody><tr><td>Включити модуль</td><td>Потрібен для роботи плагіну</td><td>Потрібно виставити значення "Так"</td></tr><tr><td>Назва платіжного метода на сторінці оплати</td><td>Назва, яка буде відображатись клієнту при виборі способу оплати</td><td>AlliancePay</td></tr><tr><td>Тип сторінки статусу</td><td>Визначає як буде виглядати сторінка після виконання оплати</td><td><p>Можливі значення : <br></p><ul><li><code>STATUS_TIMER_PAGE</code> - сторінка за замовчуванням, якщо мерчант не обрав бажаний тип, таймер редірект автоматично 1 хвилина відображення статус сторінки з автоматичним редіректом юзера на сайт мерчанта (редірект урл)</li><li><code>STATUS_REDIRECT_MERCHANT_PAGE</code> - одразу редірект на урл мерчанта</li><li><code>STATUS_PAGE</code> - редірект, на нашу статус сторіншку (завантажити квитанцію …)</li></ul></td></tr><tr><td>Тип платежу HPP</td><td><p><code>PURCHASE</code> — звичайний платіж із перенаправленням покупця на HPP (Hosted Payment Page). Кошти списуються після успішного підтвердження платежу.</p><p><code>A2A</code> — платіж account-to-account. Доступність залежить від того, чи підтримує мерчант цей тип платежу в налаштуваннях банку.</p><p><code>PREAUTH</code> — платіж із попередньою авторизацією: кошти тимчасово блокуються на рахунку клієнта. Подальше списання виконується окремою операцією <code>Completion</code> після підтвердження або створення рахунка.</p></td><td>Можливі значення : <br>- PURCHASE<br>- A2A<br>- PREAUTH</td></tr><tr><td>PreAuth expiration period</td><td>Період, протягом якого авторизація залишається дійсною.</td><td>2 hours<br>4 hours<br>6 hours<br>12 hours<br>1 day<br>2 days<br>7 days<br>14 days<br>28 days</td></tr><tr><td>PreAuth order state</td><td>Статус замовлення після успішної операції PREAUTH.</td><td>Очікується оплата банківським переказом</td></tr><tr><td>Completion trigger order state</td><td>Статус, за якого модуль може виконати операцію Completion і списати кошти.</td><td>Оплату прийнято</td></tr><tr><td>API URL</td><td>URL на який будуть надходити API запити </td><td>Потрібно вказати : <br><a href="https://api-ecom-prod.bankalliance.ua"><code>https://api-ecom-prod.bankalliance.ua</code></a></td></tr><tr><td>Сервісний код (Service Code)</td><td>Унікальний ідентифікатор для авторизації</td><td>d86a0f72-0dfe-4102-ace7-78997d042b7f</td></tr><tr><td>ID Мерчанта (Merchant Id)</td><td>Унікальний ідентифікатор мерчанта</td><td>9a337b2b-4d97-4abe-9f95-cde229f9bd83</td></tr><tr><td>Ключ авторизації (Private JWK)</td><td>Приватний ключ, потрібен для виконання авторизації</td><td><p>Його потрібно згенерувати самостійно за <a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">інструкцією</a> та надати співробітнику банку</p><p>Приклад : </p><pre class="language-json"><code class="lang-json">{
    "kty": "EC",
    "d": "nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8",
    "use": "enc",
    "crv": "P-384",
    "x": "dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn",
    "y": "qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X",
    "alg": "ECDH-ES+A256KW"
}
</code></pre></td></tr><tr><td>ID пристрою (Device Id)</td><td>Унікальний ідентифікатор пристрою. <br>Значення отримується після виконання авторизації</td><td>6c5e747f-a6c9-4087-b611-a29cfe7e8d7c</td></tr><tr><td>Токен оновлення (Refresh token)</td><td>Унікальний ідентифікатор токену. <br>Значення отримується після виконання авторизації</td><td>c54a25cf-cdd0-42dc-8843-2801f3d3c2b9</td></tr><tr><td>Токен авторизації (Auth token)</td><td>Унікальий ідентифікатор токену авторизації.<br>Значення отримується після виконання авторизації</td><td>8c469b31-6b51-4776-b222-19d57cbde444</td></tr></tbody></table>

{% hint style="warning" %}
Для кожного типу платежу реєструється унікальний термінал, що призначений для виконання конкретних операції \
Тому для A2A будуть інші значення `Merchant ID` та `Service Code`
{% endhint %}

{% hint style="warning" %}
Після налаштуванню усіх полів, обов'язково потрібно натиснути клавішу "Зберегти" і тільки після цього натиснути клавішу "Авторизуватись"
{% endhint %}

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}
