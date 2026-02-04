---
description: Налаштування платіжного модля перед початком роботи.
---

# Функціонал та опис платіжного модуля

### Шлях до налаштуваннь модуля&#x20;

В адмін панелі "Extensions"->"Extensions"->"Payments" -> "Alliance Payment"

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Інтерфейс налаштування модуля

&#x20;В параметрах вказуєте данні, що були отримані співробітником банку. \
\
В полі `Alliance API URL` потрібно вказати значення -  [https://api-ecom-prod.bankalliance.ua](https://api-ecom-prod.bankalliance.ua)

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Провірити статус замовлення

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

### Перегляд транзації

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

### Історія замовлення&#x20;

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

### Чекаут&#x20;

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### Сторінка оплати

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

### Виконання повернення

{% tabs %}
{% tab title="OpenCart 3.0" %}
Для виконання поверення потрібно перейти в деталі замовлення&#x20;

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Де буде знаходитись клавіші "Повне повернення коштів" та "Часткове повернення"

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Повне повернення коштів&#x20;

При натисканні з'явиться спливаюче вікно з повідомленням про успішне здійснення повного поверення коштів&#x20;

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

В деталях замовлення кожен з товарів буде відмічений іконкою, як повернутий та в історії замовлення з'явиться новий запис про повне повернення коштів

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Часткове поверення&#x20;

В деталях замовлення потрібно обрати за які товари буде виконанне часткове поверення&#x20;

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

Після натискання на клавішу "Часткове поверненя", з'явиться вікно з підтвердженням&#x20;

<div align="center"><figure><img src="../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure></div>

Після чого з'явиться вікно з підтвердженням&#x20;

<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

В деталях платежу товари будуть відмічені, як повернуті&#x20;

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



### Перегляд деталей повернень&#x20;

Додатково є вкладка "Returns", де можна переглянути деталі по виконаним поверненням

Повернення прив'язане до кожного товару, тому кожен рядок відображає за який саме товар було виконане поверення&#x20;

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

Натиснувши на редагувати ![](<../../.gitbook/assets/image (8) (1).png>) , відкривається деталі поверення де можна переглянути інформацію про користувача, переглянути\вказати причину поверення, змінити статус та змінити товар&#x20;

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="OpenCart 4.0" %}



{% endtab %}
{% endtabs %}
