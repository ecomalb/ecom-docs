# Налаштування та авторизація



### Шлях до налаштуваннь модуля&#x20;

В адмін панелі "Extensions"->"Extensions"->"Payments" -> "Alliance Payment"

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Інтерфейс налаштування модуля

<figure><img src="../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Обов'язково, всі поля повинні бути заповнені, щоб платіжний плагін працював правильно**
{% endhint %}

<table><thead><tr><th>Назва</th><th>Опис</th><th>Приклад</th></tr></thead><tbody><tr><td>Alliance API URL</td><td>URL на який будуть надходити API запити </td><td>Потрібно вказати : <br><a href="https://api-ecom-prod.bankalliance.ua"><code>https://api-ecom-prod.bankalliance.ua</code></a></td></tr><tr><td>Parameter "x"</td><td>Конкретні значення приватно ключа </td><td><pre><code>"dTV0I2RU5DZHVfaIQPp3svUb-Vaxwfn1WDeNUY11L3ch4vZtbdbcBc7fvK76QsDn"
</code></pre></td></tr><tr><td>Parameter "y"</td><td>Конкретні значення приватно ключа </td><td><pre><code>"qL9X0zvaXtQx_KyBZHg16qiol9lahscW-k7FBwmAf-bpYdE7-fruH9wUQWpKw14X"
</code></pre></td></tr><tr><td>Parameter "d"</td><td>Конкретні значення приватно ключа </td><td><pre><code>"nmxbG1KJ9zmekBZfJWPwG8ZJLmhKHJVsXfXIFrHkRM_Uy9z7E7ppvpvfDF62_mx8"
</code></pre></td></tr><tr><td>Service Code</td><td>Унікальний ідентифікатор для авторизації</td><td>d86a0f72-0dfe-4102-ace7-78997d042b7f</td></tr><tr><td>Merchant ID</td><td>Унікальний ідентифікатор мерчанта</td><td>9a337b2b-4d97-4abe-9f95-cde229f9bd83</td></tr><tr><td>HPP Payment Type</td><td>Тип платежу<br>При роботі зі звичайною платіжною сторінкою потрібно обирати "PURCHASE"<br>При роботі з переказом між рахунками потрібьно обирати "A2A"<br>При резервування коштів та фактичного списання зарезервованої суми "PREAUTH"</td><td>Можливі значення : <br>- PURCHASE<br>- A2A<br>- PREAUTH</td></tr><tr><td>PREAUTH expiration period</td><td>Період, протягом якого успішна PREAUTH-операція залишається активною та може бути завершена за допомогою Completion.</td><td>Період може становити від <strong>2 годин до 28 днів</strong>. Completion необхідно виконати до завершення встановленого періоду PREAUTH.</td></tr><tr><td>Page to redirect the user in case of payment error</td><td>URL для редіректу клієнта при неуспішному виконанні операції  </td><td><a href="https://wp-tests.develop.bankalliance.ua/?page_id=6">https://wp-tests.develop.bankalliance.ua/?page_id=6</a></td></tr><tr><td>Page to redirect the user in case of successful payment</td><td>URL для редіректу клієнта при успішному виконанні операції  </td><td><a href="https://wp-tests.develop.bankalliance.ua/?page_id=6">https://wp-tests.develop.bankalliance.ua/?page_id=6</a></td></tr><tr><td>Payment module status</td><td>Включання модуля </td><td><p>Можливі значення : </p><ul><li>Enabled</li><li>Disabled</li></ul></td></tr><tr><td>Order Statuses</td><td>Розділ де визначаються статуси для кожного сценарію.</td><td>Потрібно самостійно обрати</td></tr></tbody></table>

{% hint style="warning" %}
Для кожного типу платежу реєструється унікальний термінал, що призначений для виконання конкретних операції \
Тому для A2A будуть інші значення `Merchant ID` та `Service Code`
{% endhint %}

Потім потрібно натиснути кнопку "Зберження" для успішної авторизації та роботи плагіна
