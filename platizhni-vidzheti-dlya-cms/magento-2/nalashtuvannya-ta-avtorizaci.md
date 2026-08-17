# Налаштування та авторизаці

{% stepper %}
{% step %}
### Перехід у налаштуванню модулю

Для того, щоб налаштувати платіжний модуль "Alliance Payment"

Для цього потрібно :&#x20;

* Перейти в панель адмістрування Magento 2
* Перейти за шляхом \
  `Stores → Configuration → Sales → Payment Methods → Alliance Payment`&#x20;

<figure><img src="../../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Початкові налаштування&#x20;

Вікно з відображенням усіх налаштуваннь&#x20;

<figure><img src="../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

Опис та значення полів:

<table data-header-hidden><thead><tr><th width="135">Нзва</th><th>Опис</th><th width="221">Можливі опції для вибору</th></tr></thead><tbody><tr><td>Enabled</td><td>Включення та відключення модуля.</td><td>Yes<br>No</td></tr><tr><td>Title</td><td>Назва платіжного метода яка буде відображатись на сторінці оплати (checkout payment step)</td><td>текстове поле</td></tr><tr><td>Status Payment Page Type</td><td><ul><li><code>STATUS_TIMER_PAGE</code> - сторінка за замовчуванням, якщо мерчант не обрав бажаний тип, таймер редірект автоматично 1 хвилина відображення статус сторінки з автоматичним редіректом юзера на сайт мерчанта (редірект урл)</li><li><code>STATUS_REDIRECT_MERCHANT_PAGE</code> - одразу редірект на урл мерчанта</li><li><code>STATUS_PAGE</code> - редірект, на нашу статус сторінку</li></ul></td><td>Можливі значення : <br>- STATUS_TIMER_PAGE<br>-STATUS_REDIRECT_MERCHANT_PAGE<br>- STATUS_PAGE</td></tr><tr><td>Payment Type</td><td><code>PURCHASE</code> - звичайні платежі з редіректом на HPP (Hosted Payment Page).<br><code>A2A</code> - платежі account_2_account , обліковий запис мерчанта має підтримувати це в налаштуваннях.<br><code>PREAUTH</code> - платежі з преавторизацією (холдуванням коштів на рахунку клієнта) та подальшим списанням через створення рахунку в Magento</td><td>Можливі значення : <br>- PURCHASE<br>- A2A<br>- PreAuth</td></tr><tr><td>API URL</td><td>URL API Alliance банка який надається банком.<br><a href="https://api-ecom-prod.bankalliance.ua/">https://api-ecom-prod.bankalliance.ua/</a></td><td>текстове поле</td></tr><tr><td>Service Code</td><td>Сервісний код який надається Alliance банком.</td><td>текстове поле</td></tr><tr><td>Marchant Id</td><td>ID мерчанта який надається Alliance банком.</td><td> </td></tr><tr><td>Authorization key</td><td>Генерується на стороні мерчанта по інструкції<br><a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">Аутентифікація | AlliancePay</a></td><td>текстове поле</td></tr><tr><td>Device Id</td><td>Заповнюється автоматично після авторизації</td><td>текстове поле(не активне)</td></tr><tr><td>Refresh Token</td><td>Заповнюється автоматично після авторизації</td><td>текстове поле(не активне)</td></tr><tr><td>PreAuth Expiration Period</td><td>Значення на який час будуть заморожені кошти на рахунку клієнта</td><td>2 hours<br>4 hours<br>6 hours<br>12 hours<br>1 day<br>2 days<br>7 days<br>14 days<br>28 days</td></tr><tr><td>PreAuth Created Order Status</td><td>Статус замовлення в Magento 2 після успішної операції PREAUTH.</td><td>Дропдаун з можливістю вибору статусу ордера</td></tr><tr><td>PreAuth Capture Success Order Status</td><td>Статус на який змінеться замовлення в Magento 2 після виклику списання коштів (операція COMPLETION після створення рахунку).</td><td>Дропдаун з можливістю вибору статусу ордера</td></tr><tr><td>Successful Payment Order Status</td><td>Статус в який ордер переходить автоматично після <strong>оплати</strong></td><td>Дропдаун з можливістю вибору відображення успішного статусу ордера</td></tr><tr><td>Failed Payment Order Status</td><td>Статус в який ордер переходить автоматично після <strong>помилки оплати</strong></td><td>Дропдаун з можливістю вибору відображення неуспішного статусу ордера</td></tr><tr><td>Successful Refund Order Status</td><td>Статус в який ордер переходить автоматично після <strong>повернення коштів</strong></td><td>Дропдаун з можливістю вибору відображення успішного статусу повернення</td></tr><tr><td>Failed Refund Order Status</td><td>Статус в який ордер переходить автоматично після після <strong>помилки повернення коштів</strong></td><td>Дропдаун з можливістю вибору відображення неуспішного статусу повернення</td></tr><tr><td>Enable Payment Logs</td><td>Включення та відключення додаткового логування помилок та даних в<br>&#x3C;MAGENTO_ROOT>/var/log/alliance_payment.log</td><td>Yes<br>No</td></tr></tbody></table>
{% endstep %}

{% step %}
### Авторизація

Після того, як усі поля були заповненні, потрібно зберегти налаштування, та виконати авторизацію для того, щоб з'явились поля `Device Id`, `Refresh Token`&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>


{% endstep %}
{% endstepper %}



