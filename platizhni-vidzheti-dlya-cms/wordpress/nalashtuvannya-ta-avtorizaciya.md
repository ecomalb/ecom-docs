# Налаштування та авторизація

## 1. Початкові налаштування

Перейдіть до _AlliancePay → Налаштування_ і заповніть всі поля. Зверніть уагу, що деякі поля надаються банком і **настисніть кнопку зберегти і тільки після цього виконуйте авторизацію.**

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Обов'язково, всі поля повинні бути заповнені, щоб платіжний плагін працював правильно**
{% endhint %}

<table><thead><tr><th>Назва</th><th>Опис</th><th>Приклад</th></tr></thead><tbody><tr><td>Base URL API</td><td>URL на який будуть надходити API запити </td><td>Потрібно вказати : <br><a href="https://api-ecom-prod.bankalliance.ua"><code>https://api-ecom-prod.bankalliance.ua</code></a></td></tr><tr><td>Merchant ID</td><td>Унікальний ідентифікатор мерчанта</td><td>9a337b2b-4d97-4abe-9f95-cde229f9bd83</td></tr><tr><td>Service Code</td><td>Унікальний ідентифікатор для авторизації</td><td>d86a0f72-0dfe-4102-ace7-78997d042b7f</td></tr><tr><td>Private JWK</td><td>Приватний ключ, потрібен для виконання авторизації</td><td><p>Його потрібно згенерувати самостійно за <a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">інструкцією</a> та надати співробітнику банку</p><p>Приклад : </p><pre class="language-json"><code class="lang-json">{
    "kty": "EC",
    "d": "nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8",
    "use": "enc",
    "crv": "P-384",
    "x": "dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn",
    "y": "qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X",
    "alg": "ECDH-ES+A256KW"
}
</code></pre></td></tr><tr><td>HPP Payment Type</td><td>Тип платежу<br>При роботі зі звичайною платіжною сторінкою потрібно обирати "PURCHASE"<br>При роботі з переказом між рахунками потрібьно обирати "A2A"</td><td>Можливі значення : <br>- PURCHASE<br>- A2A</td></tr><tr><td>Device ID</td><td>Унікальний ідентифікатор пристрою. <br>Значення отримується після виконання авторизації</td><td>6c5e747f-a6c9-4087-b611-a29cfe7e8d7c</td></tr><tr><td>Refresh Token</td><td>Унікальний ідентифікатор токену. <br>Значення отримується після виконання авторизації</td><td>c54a25cf-cdd0-42dc-8843-2801f3d3c2b9</td></tr><tr><td>Success URL</td><td>URL для редіректу клієнта при успішному виконанні операції  </td><td><a href="https://wp-tests.develop.bankalliance.ua/?page_id=6">https://wp-tests.develop.bankalliance.ua/?page_id=6</a></td></tr><tr><td>Fail URL</td><td>URL для редіректу клієнта при неуспішному виконанні операції  </td><td><a href="https://wp-tests.develop.bankalliance.ua/?page_id=6">https://wp-tests.develop.bankalliance.ua/?page_id=6</a></td></tr></tbody></table>

{% hint style="warning" %}
Для кожного типу платежу реєструється унікальний термінал, що призначений для виконання конкретних операції \
Тому для A2A будуть інші значення `Merchant ID` та `Service Code`
{% endhint %}

## 2. Авторизація пристрою

* Натисніть **Переавторизувати зараз**
* Після успіху з’явиться _Токен дійсний до:_ — дата/час дії токена.

**Важливо.** Токен дійсний 24 години; автоматичне поновлення виконується кожні \~12 годин. Ви також можете натиснути _Переавторизувати зараз_, щоб оновити токен вручну.

## 3. Часовий пояс і точність часу

Переконайтеся, що у _Налаштування → Загальні → Часовий пояс_ вибрано **Київ**. У плагіні дата `tokenExpiration` парситься та показується у локальному часі сайту.
