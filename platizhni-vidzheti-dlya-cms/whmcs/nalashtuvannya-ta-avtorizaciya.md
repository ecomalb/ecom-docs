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

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

| **Поле**               | **Опис**                                                                                                                                                                                                                                                                                                                               |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Display Name**       | <p>Назва платіжного методу, яку клієнт побачить на сторінці рахунку (наприклад: <em>Оплата карткою / Apple Pay / Google Pay</em>).<br>Дефолтне значення: AlliancePay Bank</p>                                                                                                                                                          |
| **API Base URL**       | <p>Посилання на API банку.<br>Потрібно вказати : <a href="https://api-ecom-prod.bankalliance.ua">https://api-ecom-prod.bankalliance.ua</a></p>                                                                                                                                                                                         |
| **Merchant ID**        | <p>Ваш унікальний ідентифікатор мерчанта в системі банку.<br>Буде надаватись банком</p>                                                                                                                                                                                                                                                |
| **Service Code**       | <p>Код сервісу для ідентифікації типу послуг.<br>Буде надаватись банком</p>                                                                                                                                                                                                                                                            |
| **Authentication Key** | <p>Приватна частина ключа, для авторизації. <br>Потрібно згенерувати відповідно до документації : <a href="https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta">Процес генерації ключів</a><br><i class="fa-square-info">:square-info:</i> Публічну частину потрібно надати банку</p> |

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
