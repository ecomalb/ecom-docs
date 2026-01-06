# Функціонал



### **Список ордерів**

В список ордерів додається нова колонка “AlliancePay payment status“. Якщо платіж був через AlliancePay то в цій колонці в списку до замовлення буде кнопка “Статус платежу“. Зверніть увагу, що якщо немає Callback по замовленню, то підсвідчується "Немає колбеку від AlliancePay". Провірьте "Статус платежу""

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Деталі ордеру**

Callback отримано, тоді дані беруться з локальної БД, в яку ми зберегли колбек

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

Callback не отримано, тоді дані беруться прямим запитом на еКом

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **Сторінка оплати**

На сторінці оплати обов'язково повинен бути шорт код `[woocommerce_checkout]`. На чекауті з'явиться вибір оплати **AlliancePay**

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

Віджет оплати:

<figure><img src="../../.gitbook/assets/image (11) (1) (1).png" alt=""><figcaption></figcaption></figure>

після оплати, Ecom повинен прислати нам Callback про статус оплати і тоді ми фіналізуємо оплату вже на нашій стороні.
