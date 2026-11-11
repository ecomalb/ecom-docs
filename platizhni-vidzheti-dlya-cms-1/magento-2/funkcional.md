# Функціонал

## Процес створення замовлення клієнтом на сайті  <a href="#proces-stvorennya-zamovlennya-kliyentom-na-saiti" id="proces-stvorennya-zamovlennya-kliyentom-na-saiti"></a>

1.  Додаємо товари в кошик та переходимо на сторінку оплати та натискаємо оформити замовлення (Place Order)

    <figure><img src="../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>
2.  Далі сайт перенаправляє покупця на HPP сторінку де клієнт проходить процес оплати<br>

    <figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>
3.  Після оплати Alliance банк повертає клієнта на сторінку зі статусом замовлення на сайті<br>

    <figure><img src="../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>



## Процес роботи з замовленням в адмін панелі <a href="#proces-roboti-z-zamovlennyam-v-admin-paneli" id="proces-roboti-z-zamovlennyam-v-admin-paneli"></a>

Переходимо в адмін панель на сторіку з замовленнями\
`Sales → Orders`

<figure><img src="../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

Після отримання callback замовлення переходе в статус який обрано в налаштуваннях в разі успішної оплати\
`Stores → Configuration → Sales → Payment Methods → Alliance Payment → Successful Payment Order Status`\
Переходимо до деталей замовлення → View

<figure><img src="../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Якщо замовлення створене за допомогою hppPayType PREAUTH , в такому разі потрібно створити Invoice (Рахунок).
{% endhint %}

Перейти в деталі замовлення та натиснути Invoice

<figure><img src="../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Прокрутити до низу і натиснути Submit Invoice\
Важливо при створенні рахунка має бути обовʼязково обрана опція Capture Online

<figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

В деталях замовлення знаходиться інформація по операціям.

{% hint style="warning" %}
В разі якщо callback не надійшов можна оновити інформацію вручну за допомогою кнопки Check Payment Status.
{% endhint %}

Якщо callback надійшов тоді вручну оновлювати не потрібно.

<figure><img src="../../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

### Виконання повернень

В разі необхідності повернення коштів в деталях замовлення переходимо в Invoices\
Обираємо Invoce і натискаємо → View

{% hint style="info" %}
&#x20;Виконати повернення можливо, коли операція успішна та Invoce буде в статусі Paid
{% endhint %}

<figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

Далі створюємо документ з поверненням Credit Memo

<figure><img src="../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

Обираємо продукти для повернення та натискаємо **Rfund**

{% hint style="info" %}
Refund Offline не створить запит в API Alliance банк для повернення коштів, це стандартний процесс для Online\Offline платіжних методів.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

Після створення повернення додається інформація по транзакції REFUND

<figure><img src="../../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>
