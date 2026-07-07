# Налаштування та авторизація



### Шлях до налаштуваннь модуля&#x20;

В адмін панелі "Extensions"->"Extensions"->"Payments" -> "Alliance Payment"

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Інтерфейс налаштування модуля

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Обов'язково, всі поля повинні бути заповнені, щоб платіжний плагін працював правильно**
{% endhint %}

<table><thead><tr><th>Назва</th><th>Опис</th><th>Приклад</th></tr></thead><tbody><tr><td>Alliance API URL</td><td>URL на який будуть надходити API запити </td><td>Потрібно вказати : <br><a href="https://api-ecom-prod.bankalliance.ua"><code>https://api-ecom-prod.bankalliance.ua</code></a></td></tr><tr><td>Merchant ID</td><td>Унікальний ідентифікатор мерчанта</td><td>9a337b2b-4d97-4abe-9f95-cde229f9bd83</td></tr><tr><td>Service Code</td><td>Унікальний ідентифікатор для авторизації</td><td>d86a0f72-0dfe-4102-ace7-78997d042b7f</td></tr><tr><td>Private JWK</td><td>Приватний ключ, потрібен для виконання авторизації</td><td><p>Його потрібно згенерувати самостійно за <a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">інструкцією</a> та надати співробітнику банку</p><p>Приклад : </p><pre class="language-json"><code class="lang-json">{
    "kty": "EC",
    "d": "nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8",
    "use": "enc",
    "crv": "P-384",
    "x": "dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn",
    "y": "qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X",
    "alg": "ECDH-ES+A256KW"
}
</code></pre></td></tr><tr><td>Parameter "x"</td><td>Конкретні значення приватно ключа </td><td><pre><code>"dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn"
</code></pre></td></tr><tr><td>Parameter "y"</td><td>Конкретні значення приватно ключа </td><td><pre><code>"qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X"
</code></pre></td></tr><tr><td>Parameter "d"</td><td>Конкретні значення приватно ключа </td><td><pre><code>"nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8"
</code></pre></td></tr><tr><td>HPP Payment Type</td><td>Тип платежу<br>При роботі зі звичайною платіжною сторінкою потрібно обирати "PURCHASE"<br>При роботі з переказом між рахунками потрібьно обирати "A2A"</td><td>Можливі значення : <br>- PURCHASE<br>- A2A</td></tr><tr><td>Page to redirect the user in case of successful payment</td><td>URL для редіректу клієнта при успішному виконанні операції  </td><td><a href="https://wp-tests.develop.bankalliance.ua/?page_id=6">https://wp-tests.develop.bankalliance.ua/?page_id=6</a></td></tr><tr><td>Page to redirect the user in case of payment error</td><td>URL для редіректу клієнта при неуспішному виконанні операції  </td><td><a href="https://wp-tests.develop.bankalliance.ua/?page_id=6">https://wp-tests.develop.bankalliance.ua/?page_id=6</a></td></tr></tbody></table>

{% hint style="warning" %}
Для кожного типу платежу реєструється унікальний термінал, що призначений для виконання конкретних операції \
Тому для A2A будуть інші значення `Merchant ID` та `Service Code`
{% endhint %}

Потім потрібно натиснути кнопку "Зберження" для успішної авторизації та роботи плагіна
