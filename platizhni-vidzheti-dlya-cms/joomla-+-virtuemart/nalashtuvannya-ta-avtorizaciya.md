# Налаштування та авторизація

{% stepper %}
{% step %}
### Переходимо у налаштування модуля&#x20;

За шляхом "Компоненти" -> "Payment Methods"

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Створюємо платіжний метод&#x20;

Натискаємо на клавішу "Створити"

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Після у новому вікні, потрібно заповнити поля `Payment Name`, `Sef Alias` та обрати `Payment Method == VM - Alliance Pay`&#x20;

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Після чого потрібно натиснути клавішу "Зберегти", щоб вікрилась можливість налаштовувати вкладку Configuration
{% endstep %}

{% step %}
### Налаштування конфігурації, платіжного методу

У вкладенці Configuration потрібно буде додатково вказати значення, що будуть надані співробітником банку

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Обов'язково, всі поля повинні бути заповненні, щоб платіжний плагін працював правильно
{% endhint %}

#### &#x20;**Опис полів:**

* Поле `Тип сторінки статусу` має три доступні значення :
  * &#x20;  Сторінка з таймером (`STATUS_TIMER_PAGE`) - сторінка за замовчуванням, якщо мерчант не обрав бажаний тип, таймер редірект автоматично 1 хвилина відображення статус сторінки з автоматичним редіректом юзера на сайт мерчанта (редірект урл)
  * Перенаправлення на сторінку продавця (`STATUS_REDIRECT_MERCHANT_PAGE`)- одразу редірект на урл мерчанта
  * Сторінка статусу (`STATUS_PAGE)` - редірект, на нашу статус сторіншку (завантажити квитанцію …)
* Поле `API URL` потрібно вказати значення - [https://api-ecom-prod.bankalliance.ua](https://api-ecom-prod.bankalliance.ua/)
* Поля `Сервісний код (Service Code)` , `ID Мерчанта (Merchant Id)` будуть надані банком
* Поле `Authentication Key` , потрібно буде згенерувати самостійно відповідно до документації ([https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta](https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta)), де публічну частину потрібно буде передати співробітнику банку&#x20;
* В полях `Статус при успішному платежі`, `Статус при невдачі платежу`, `Статус при успішному поверненні`, `Статус при невдачі повернення`- потрібно обрати самостійно

{% hint style="warning" %}
Після налаштуванню усіх полів, обов'язково потрібно натиснути клавішу "Зберегти" і тільки після цього натиснути клавішу "Авторизуватись"
{% endhint %}
{% endstep %}

{% step %}
### Авторизація

Як тільки була натиснута клавіша "Авторизуватись", під клавішою повинен з'явитись надпис "Success!"

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>


{% endstep %}
{% endstepper %}
