# Налаштування та авторизація

{% stepper %}
{% step %}
### Переходимо у налаштування модуля&#x20;

За шляхом "Компоненти" -> "Payment Methods"

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Створюємо платіжний метод&#x20;

Натискаємо на клавішу "Створити"

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Після у новому вікні, потрібно заповнити поля `Payment Name`, `Sef Alias` та обрати `Payment Method == VM - Alliance Pay`&#x20;

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

Після чого потрібно натиснути клавішу "Зберегти", щоб вікрилась можливість налаштовувати вкладку Configuration
{% endstep %}

{% step %}
### Налаштування конфігурації, платіжного методу

У вкладенці Configuration потрібно буде додатково вказати значення, що будуть надані співробітником банку

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Обов'язково, всі поля повинні бути заповненні, щоб платіжний плагін працював правильно
{% endhint %}

#### &#x20;**Опис полів:**

<table><thead><tr><th>Назва</th><th>Опис</th><th>Приклад</th></tr></thead><tbody><tr><td>Тип сторінки статусу</td><td>Визначає як буде виглядати сторінка після виконання оплати</td><td><p></p><p>Можливі значення : <br></p><ul><li><code>STATUS_TIMER_PAGE</code> - сторінка за замовчуванням, якщо мерчант не обрав бажаний тип, таймер редірект автоматично 1 хвилина відображення статус сторінки з автоматичним редіректом юзера на сайт мерчанта (редірект урл)</li><li><code>STATUS_REDIRECT_MERCHANT_PAGE</code> - одразу редірект на урл мерчанта</li><li><code>STATUS_PAGE</code> - редірект, на нашу статус сторіншку (завантажити квитанцію …)</li></ul></td></tr><tr><td>Тип платежу</td><td>Тип платежу<br>При роботі зі звичайною платіжною сторінкою потрібно обирати "PURCHASE"<br>При роботі з переказом між рахунками потрібьно обирати "A2A"</td><td>Можливі значення : <br>- PURCHASE<br>- A2A</td></tr><tr><td>API URL</td><td>URL на який будуть надходити API запити </td><td>Потрібно вказати : <br><a href="https://api-ecom-prod.bankalliance.ua"><code>https://api-ecom-prod.bankalliance.ua</code></a></td></tr><tr><td>Service Code</td><td>Унікальний ідентифікатор для авторизації</td><td>d86a0f72-0dfe-4102-ace7-78997d042b7f</td></tr><tr><td>Merchant ID</td><td>Унікальний ідентифікатор мерчанта</td><td>9a337b2b-4d97-4abe-9f95-cde229f9bd83</td></tr><tr><td>Private JWK</td><td>Приватний ключ, потрібен для виконання авторизації</td><td><p>Його потрібно згенерувати самостійно за <a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">інструкцією</a> та надати співробітнику банку</p><p>Приклад : </p><pre class="language-json"><code class="lang-json">{
    "kty": "EC",
    "d": "nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8",
    "use": "enc",
    "crv": "P-384",
    "x": "dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn",
    "y": "qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X",
    "alg": "ECDH-ES+A256KW"
}
</code></pre></td></tr><tr><td>Статуси змовлень</td><td>Потрібно самостійно вказати, яка логіка буде відбуватись при конкретному статусі платежа</td><td></td></tr></tbody></table>

{% hint style="warning" %}
Для кожного типу платежу реєструється унікальний термінал, що призначений для виконання конкретних операції \
Тому для A2A будуть інші значення `Merchant ID` та `Service Code`
{% endhint %}

{% hint style="warning" %}
Після налаштуванню усіх полів, обов'язково потрібно натиснути клавішу "Зберегти" і тільки після цього натиснути клавішу "Авторизуватись"
{% endhint %}
{% endstep %}

{% step %}
### Авторизація

Як тільки була натиснута клавіша "Авторизуватись", під клавішою повинен з'явитись надпис "Success!"

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>


{% endstep %}
{% endstepper %}
