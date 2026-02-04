# Функціонал

### Процес створення замовлення

Після того як клієнт обрав товари, та перейшов на сторінку оплати, потрібно обрати спосіб оплати через "Alliance Pay"

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Після чого, покупця перенаправляє на платіжну сторінку з введення каркових даних&#x20;

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

### Перегляд замовлень в адмін панелі

Для того, щоб переглянути всі замовлення, потрібно перейти за шляхом `Sales → Orders`

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Перегляд деталей замовлення, виконується через клавішу "View"

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### Перевірка статусу замовлення

{% hint style="info" %}
У разі виникнення проблем з статусом замовлення, присутній функціонал ручної перевірки
{% endhint %}

В деталях платежу знаходиться розділ "Payment & Shipping Method"

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

При натисканні на клавішу "Check Payment Status", буде виконуватись перевірка статусу замовлення

### Виконання повернень

Для виконання повернення потрібно перейти в деталі платежі та переходимо у "Invoices"&#x20;

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

І переходимо у деталі накладної через "View"

{% hint style="info" %}
Обов'язково status накладної повинен бути "Paid", що вказує на його успішність
{% endhint %}

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

В деталях накладної потрібно створити документ з поверненням натиснувши на "Credit Memo"

Після чого в розділі "Items to Refund", потрібно обрати всі товари в стовпці "Qty to Refund"

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Після чого натиснути клавішу **"Refund"**

{% hint style="warning" %}
Refund Offline не створить запит в API Alliance банк для повернення коштів, це стандартний процесс для Online\Offline платіжних методів
{% endhint %}

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Після виконання повернення в деталях замовлення з'явиться нова операція з типом "Refund", та в колонці "Item Status" зміниться на "Refunded"

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
