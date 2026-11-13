---
description: >-
  Як покупець оплачує замовлення та оформлює підписку і як мерчант перевіряє
  операції, списує зарезервовані кошти й виконує повернення.
---

# Функціонал

### Разова оплата та A2A

Покупець додає товари в кошик і на кроці **Review & Payments** вибирає спосіб оплати, назву якого задано в полі **Title**. Після натискання **Place Order** Magento відкриває платіжну сторінку банку (HPP).

![Вибір Alliance Pay та кнопка Place Order під час оформлення](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2Fk0UulY64jaIkLjh8JLxi%2Fmagento2-checkout.png?alt=media\&token=375dc095-a184-4f56-afa3-f509d3433231)

Для `PURCHASE` покупець завершує разову оплату на HPP. Для `A2A` він проходить доступний на HPP сценарій переказу з рахунку на рахунок. A2A потребує підтримки з боку термінала та базової валюти магазину UAH.

Подальший перехід залежить від **Status Payment Page Type**. Після повернення до магазину покупець може побачити підтвердження замовлення.

![Підтвердження успішної оплати після повернення до магазину](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FQz1doIEgYw5MqR60fmWa%2Fmagento2-success.png?alt=media\&token=6c9dd82e-8ab6-4861-bea2-4f158acd73e7)

### Перевірка замовлення

Відкрийте **Sales → Orders**, знайдіть замовлення й натисніть **View**. Колонка **Status** показує статус замовлення в Magento. Після callback модуль застосовує статус, налаштований для відповідного результату операції.

![Статус замовлення й дія View у Sales → Orders](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FPMcNk6qMLGbykokuohhy%2Fmagento2-orders.png?alt=media\&token=81f2dd3b-89d6-4414-83e4-8c6d853b2036)

У картці замовлення перейдіть до **Payment & Shipping Method → Alliance Payment Status**. Якщо callback ще не надійшов, натисніть **Check Payment Status**. У **Payment Operations** перевірте дату, статус, ідентифікатор і тип операції.

![Check Payment Status і таблиця Payment Operations](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FeSuML6MVhERjTt1yaGHY%2Fmagento2-operations.png?alt=media\&token=a884d8d8-0c9c-4440-b157-260435ce41b2)

### PREAUTH — резервування та списання

У режимі `PREAUTH` після успішної авторизації банк резервує кошти на строк, заданий у полі **PreAuth Expiration Period**. Щоб списати кошти, створіть рахунок у Magento до завершення цього строку.

У **Sales → Orders** відкрийте замовлення з успішною операцією PREAUTH. Натисніть **Invoice**.

![Дія Invoice у картці замовлення](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2Fg6Xrv13JYDY66M9uHi4A%2Fmagento2-orderdetail.png?alt=media\&token=cff9f14e-67df-4202-87b7-6e21ff2bd7f7)

На сторінці **New Invoice** перевірте позиції та **Grand Total**. У полі **Amount** виберіть **Capture Online** і натисніть **Submit Invoice**. Magento надішле банку запит на списання (`COMPLETION`).

![Capture Online і Submit Invoice на сторінці рахунку](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FbrodPG0KvaOrx454BN8P%2Fmagento2-capture.png?alt=media\&token=aac7971c-22f2-4b57-a0d6-2e480cdfe11c)

Перевірте операцію в картці замовлення. Після успішного списання Magento застосовує **PreAuth Capture Success Order Status**.

### Повернення коштів

Відкрийте **Sales → Orders → View → Invoices**. Знайдіть рахунок зі статусом **Paid** і натисніть **View**. Для повернення через банк почніть оформлення **Credit Memo** із цього рахунку.

![Дата рахунку та поле Transaction ID](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2F4I4pcd66xhLE0W7oKWIZ%2Fmagento2-invoice.png?alt=media\&token=398e3c00-a752-487b-a9e8-b449b5756e9a)

Перевірте товари, кількість і суму повернення. Натисніть **Refund**, щоб надіслати запит в AlliancePay. Кнопка **Refund Offline** лише реєструє повернення в Magento. Кошти покупцеві в такому разі потрібно повернути окремо.

Відкрийте документ у **Credit Memos** і звірте результат з операцією `REFUND` у **Payment Operations**.

![Документ Credit Memo зі статусом Refunded](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FsIbwOX4MyoL7HfokPBU9%2Fmagento2-refund.png?alt=media\&token=dd68564e-3487-47a8-88a3-c779aaaa4a6a)

### Підписки та рекурентні платежі

Починаючи з версії 1.7.0 для підписки доступний окремий платіжний метод **AlliancePay Subscriptions**. Покупець оформлює підписку на HPP, а банк виконує наступні списання за правилами плану.

#### Створення шаблону та плану

Відкрийте **Subscriptions → Plan Templates → Add New Template**. Вкажіть унікальний **Code**, назву **Name** і **Category Indicator**. Додайте щонайменше одне правило для розкладу.

![Шаблони планів і кнопка Add New Template](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FIJ0nn3jHJ4iidHRk0L3w%2Fmagento2-templates.png?alt=media\&token=599aab29-6959-4c78-9956-1060fe133e08)

Для кожного правила задайте діапазон **Payment # From / Payment # To**, інтервал (**Interval Value** і **Day**, **Week** або **Month**), суму в мінімальних одиницях валюти та валюту. Для гривні суму вказують у копійках.

У **Subscriptions → Subscription Plans → Create Plan** знайдіть товар за назвою чи SKU. Виберіть шаблон або заповніть правила вручну. Перевірте індикатор категорії, назву, опис і натисніть **Create Plan**. Після синхронізації перевірте статус плану та **Sync Status**. Якщо бачите `ERROR`, перевірте причину помилки синхронізації.

#### Оформлення покупцем

Покупець входить до облікового запису, на сторінці товару вибирає **Subscribe & Save** і план у **Choose a plan**. Для разової покупки доступний **Buy once**. Підписку оформлюють окремим кошиком.

На кроці оплати покупець вибирає **AlliancePay Subscriptions** і натискає **Place Order**. На HPP він прив’язує картку та проходить перший платіж. Після успішного callback підписка переходить із `PENDING` в `ACTIVE`. В особистому кабінеті покупець може переглянути й скасувати власну підписку.

#### Зміна ціни та керування планом

| Дія                            | Коли використовувати                                                                                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Reprice                        | Для зміни правил чинного плану. Заповніть New Rules, Applies From і Reason, підтвердьте повідомлення клієнтів. Дата має враховувати Reprice Lead Time. |
| Replace Plan For New Customers | Для нових покупців. Вкажіть New Plan Name та нові правила. Чинні підписки продовжують діяти на попередньому плані.                                     |
| Archive                        | Для архівації плану. У банку план отримує статус ARCHIVED, у Magento — CANCELED.                                                                       |

#### Підписки та заплановані платежі

У **Subscriptions → Subscriptions** відкрийте підписку. Дія **Diagnostics** отримує актуальні операції з банку. **Cancel** скасовує підписку. У **Subscriptions → Scheduled Payments** доступні заплановані платежі та дія **Run Now** для ручного запуску списання.

Результат звірки суми має окремий статус. `OK` означає збіг із правилами плану, `MISMATCH` — розбіжність, `SKIPPED` — звірку виконати не вдалося. Права на перегляд, зміну ціни, скасування та ручний запуск налаштовують у **System → Permissions → User Roles → Role Resources → Alliance Pay → Subscriptions**.
