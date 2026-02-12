# Функціонал

### Процес створення замовлення

Після того як клієнт обрав товари, та перейшов на сторінку оплати, потрібно обрати спосіб оплати через "AlliancePay"

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

Після чого, покупця перенаправляє на платіжну сторінку з введення каркових даних&#x20;

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

### Перегляд замовлень в адмін панелі

Для того, щоб переглянути всі замовлення, потрібно перейти за шляхом `Компоненти → VirtueMart → Orders`

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

Перегляд деталей платежу, виконується при натисканні на значення в колонці `"Order number/Invoice"`&#x20;

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (56).png" alt="Деталі замовлення"><figcaption></figcaption></figure>

### Перевірка статусу замовлення

{% hint style="info" %}
У разі виникнення проблем з статусом замовлення, присутній функціонал ручної перевірки
{% endhint %}

В деталях платежу знаходиться розділ "**AlliancePay оновити транзакції та статуси**"

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

При натисканні на клавішу "Оновити", буде виконуватись перевірка статусу платежу

### Виконання повернень

В деталях платежу, можна знайти два розділа "**Часткове повернення коштів (Alliance)**" та "**Full Refund (AlliancePay)"**

{% hint style="info" %}
Обов'язково "Статус оплати" плтежу повинен мати "SUCCESS", що вказує на його успішність

![](<../../.gitbook/assets/image (59).png>)
{% endhint %}

{% tabs %}
{% tab title="Часткове повернення коштів" %}
Для виконання часткового поверення коштів, в розділі "**Часткове повернення коштів (Alliance)**", потрібно за допомогою чекбоксів, обрати ті товари за якими буде виконуватись поверення

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Тим самим система автоматично підрахуває суму по вибраним товарах

Після чого, потрібно натиснути кнопку "Виконати повернення для обраних товарів", відразу з'явиться вікно з повідомленям про успішне часткове повернення

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

В деталях платежу в розділі "**Історія транзакцій Alliance**", з'явиться новий платіж з типом операції "REFUND"

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>


{% endtab %}

{% tab title="Повне повернення коштів" %}
Для виконання повного повернення коштів, потрібно в розділі "**Full Refund (AlliancePay)**"

натиснути кнопку **"Execute Order Refund"**

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Після чого в розділі "**Історія транзакцій Alliance**" з'явиться новий платіж з типом операції "REFUND"

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

А також в розділі "Items" кожен товар отримає статус "Refunded"

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
