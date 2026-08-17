# Функціонал

## #Виконання оплати :

На сайті після того, як були обрані товари, та перейшли на етап оплати, можна обрати метод оплати "AllaincePay Bank"

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Платіжна сторінка матиме вигляд :&#x20;

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>



## Перегляд замовлень&#x20;

У вкладці "Orders" потрібно обрати розділ "List All Orders"

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

Для переходу в деталі замовлення потрібно натиснути на відповідний номер в колонці "ID"

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

## Перегляд транзакції

У вкладці "Billing" потрібно обрати розділ "Transaction List"

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Для перегляду статусу транзакції, потрібно натиснути "Check Order"

Після чого відкриється нове вікно в браузері з деталями транзакції

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

## Виконання повернення

В деталях замовлення, потрібно натиснути кнопку "Cancel & Refund"

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

Після виконання повернення, банер в деталях замовлення сповістить про його успішність

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

В деталях транзакції, з'явиться новий запис про виконане повернення&#x20;

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

## Виконання PreAuth платежу

Режим **PREAUTH** використовується для резервування (холдування) коштів на картці клієнта без їх негайного списання. Остаточне списання виконується окремою операцією **Completion** після підтвердження інвойсу в адміністративній панелі.

#### Налаштування PREAUTH <a href="#nalashtuvannya-preauth" id="nalashtuvannya-preauth"></a>

У налаштуваннях платіжного методу **AlliancePay Bank** виберіть:

* **Payment Type** — `PREAUTH`.
* **Pre-Auth Expiration Period** — строк, протягом якого кошти залишаються зарезервованими. Доступні значення: `2h`, `4h`, `6h`, `12h`, `1d`, `2d`, `7d`, `14d` або `28d`.
* **API Base URL**, **Merchant ID**, **Service Code** та **Authentication Key** — значення, надані Alliance Bank.

Після завершення строку **Pre-Auth Expiration Period** резервування може бути автоматично скасоване банком. Тому підтвердити списання потрібно до закінчення цього строку.

#### Процес оплати клієнтом <a href="#proces-oplati-kliyentom" id="proces-oplati-kliyentom"></a>

1. Клієнт оформлює замовлення та переходить на Hosted Payment Page (HPP).
2. Після успішної автентифікації банк резервує суму замовлення на рахунку клієнта.
3. Магазин отримує результат операції PREAUTH. На цьому етапі кошти ще **не списані**, а лише заблоковані.
4. Для завершення платежу адміністратор має підтвердити списання в інвойсі.

#### Підтвердження списання коштів <a href="#pidtverdzhennya-spisannya-koshtiv" id="pidtverdzhennya-spisannya-koshtiv"></a>

Підтвердження виконується в адміністративній панелі платіжної системи:

1. Відкрийте **Billing → Invoices**.\
   ![](<../../.gitbook/assets/image (113).png>)
2. Знайдіть інвойс, пов’язаний із платежем PREAUTH, і відкрийте його.
3. Перейдіть до **Manage invoice**.
4. Переконайтеся, що інвойс має статус **UNPAID**, а в інформаційному блоці зазначено, що кошти зарезервовано та не списано.
5. Натисніть **Підтвердити списання (Completion)**.
6. Дочекайтеся відповіді банку та перевірте результат операції в блоці **Transactions**.

Кнопка **Підтвердити списання (Completion)** виконує фінальне списання саме зарезервованої суми. Не натискайте її повторно, якщо попередній запит уже успішно виконано.

#### Результат операції <a href="#rezultat-operaciyi" id="rezultat-operaciyi"></a>

Після успішного Completion платіж переходить із PREAUTH у фінальний стан списання. В інвойсі оновлюється баланс і статус оплати, а в розділі **Transactions** з’являється запис про операцію **COMPLETION** із відповідним ідентифікатором транзакції.

Якщо операція не виконана, перевірте повідомлення про помилку, строк дії резервування та доступність суми. До отримання успішної відповіді банку не вважайте платіж остаточно списаним.
