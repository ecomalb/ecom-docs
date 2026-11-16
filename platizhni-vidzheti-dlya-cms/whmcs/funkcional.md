# Функціонал

### Разова оплата <a href="#section-1" id="section-1"></a>

Під час оформлення замовлення покупець вибирає **AlliancePay Bank** і переходить на платіжну сторінку банку (HPP).

![Вибір AlliancePay Bank під час оформлення замовлення](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FPXBHH7bRed5frSR7TsdM%2Fimage.png?alt=media\&token=2b9d64bc-1552-47a5-a306-71d75fcafef3)

![Платіжна сторінка банку для оплати рахунку](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2F8PZ0aHTWRSRx1VjB7Bx2%2Fimage.png?alt=media\&token=31d39d31-835c-494c-aa76-446bb2e734d3)

### Замовлення, транзакції та повернення <a href="#section-2" id="section-2"></a>

**1.** У **Orders → List All Orders** знайдіть замовлення. Натисніть номер у стовпці **ID**, щоб відкрити його картку.

![Перехід до списку замовлень WHMCS](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2Faw3T8SeXdU6g2g7vZvcf%2Fimage.png?alt=media\&token=96779634-7373-4c61-ab1a-c27e72cefafc)

![Вибір замовлення за номером](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FZ1B3WPyHQNEbcS7rd9Nq%2Fimage.png?alt=media\&token=afdc0693-a0de-4411-b22d-3a9af636ce71)

**2.** Для перевірки платежу відкрийте **Billing → Transaction List**. Кнопка **Check Order** відкриває відомості про операцію в новій вкладці.

![Список транзакцій у меню Billing](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FG8Aqm1ptrusIjImjzQJB%2Fimage.png?alt=media\&token=24eade5b-1ce6-4dd2-a6af-0ad4cdc57df9)

![Деталі операції після вибору Check Order](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FJz4sruzKc0Pa8NkVagpG%2Fimage.png?alt=media\&token=80a49923-86ff-43e4-87a8-7d7c07524d2f)

**3.** Якщо потрібно одночасно скасувати замовлення й повернути оплату, відкрийте його картку та виберіть **Cancel & Refund**. Перевірте повідомлення про результат у картці замовлення й окремий запис повернення в деталях транзакції.

![Дія Cancel & Refund у картці замовлення](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FuTAGSjcK2HZhhLN8Y2Cj%2Fimage.png?alt=media\&token=5f687b6d-8a93-46db-91ce-1407fcaf565f)

![Повідомлення про успішне повернення](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FflIqx5cJCBbMg3K2NzZs%2Fimage.png?alt=media\&token=779a310d-994f-4fed-8358-cdf29a132445)

![Запис про повернення в деталях транзакції](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FLdW4runyHHuZYHwMCtlr%2Fimage.png?alt=media\&token=d008b6e2-2f63-4479-8be4-3ab9af71f03d)

### Резервування коштів і підтвердження списання <a href="#section-3" id="section-3"></a>

Для резервування коштів виберіть у шлюзі **Payment Type → PREAUTH** і задайте **Pre-Auth Expiration Period**. Після підтвердження на HPP банк резервує кошти. Для списання зарезервованої суми адміністратор виконує **Completion** до закінчення строку резервування.

**1.** Відкрийте **Billing → Invoices** і виберіть рахунок, за яким покупець здійснив передавторизацію.

![Перехід до рахунків у меню Billing](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FJB6p1jhIGBUiuhLAcYQg%2Fimage.png?alt=media\&token=149fa5e7-7a7b-454c-b672-e030368ff735)

**2.** У **Manage invoice** перевірте статус рахунку **UNPAID** і повідомлення про успішне резервування коштів.

**3.** Натисніть **Підтвердити списання (Completion)**. Дочекайтеся відповіді банку й перевірте в **Transactions** запис **COMPLETION**, його ідентифікатор, баланс і статус рахунку.

**4.** Якщо запит завершився помилкою або відповідь не надійшла, спочатку звірте стан транзакції та строк резервування. Успішний запит повторювати не потрібно.

### Підписки AlliancePay <a href="#alliancepay" id="alliancepay"></a>

Для продажу підписки потрібні ввімкнений перемикач **Enable Subscriptions**, рекурентний продукт із ціною в UAH, активований модуль **AlliancePay Subscriptions** і синхронізований план для вибраного платіжного циклу. Якщо підписки у шлюзі вимкнено, покупець не побачить кнопку підписки, а AlliancePay буде приховано для рекурентних продуктів.

#### Підготуйте виставлення рахунків <a href="#section-4" id="section-4"></a>

У **Configuration → System Settings → Automation Settings → Billing Settings** задайте **Invoice Generation** так, щоб рахунок існував до списання банком. Для інтеграції орієнтуйтеся на випередження у 3–7 днів. Якщо на момент списання рахунку ще немає, модуль позначить платіж `NEEDS_REVIEW`. [Довідка WHMCS про строки виставлення рахунків](https://docs.whmcs.com/8-12/system/automation/automation-settings/)

У **Configuration → System Settings → General Settings → Invoices** вимкніть **Continuous Invoice Generation** і ввімкніть **Automatic Subscription Management** згідно з інструкцією модуля. На знімку другий перемикач знятий. Під час тестового скасування сервісу звірте статус підписки в банку.

![Вкладка Invoices із параметрами Continuous Invoice Generation і Automatic Subscription Management](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2Fu1LeGimj2w9vXqCtaCfm%2Fwhmcs-ua-03-invoice-settings.png?alt=media\&token=30247d4d-b6f6-49c2-9297-08aa7baeda9b)

#### Налаштуйте продукт <a href="#section-5" id="section-5"></a>

**1.** У **Configuration → System Settings → Products/Services** відкрийте продукт і перейдіть на вкладку **Pricing**.

**2.** Виберіть **Payment Type → Recurring**. У рядку **UAH** увімкніть потрібні цикли й задайте ціну для кожного. Для продукту з типом **One Time** підписка недоступна.

**3.** Якщо потрібна одноразова плата за підключення, задайте **Setup Fee**. Вона додається до першого платежу. Наприклад, за щомісячної ціни 12 грн і плати за підключення 1 грн перший платіж становить 13 грн, наступні — по 12 грн.

**4.** У налаштуваннях групи продукту перевірте **Available Payment Gateways**. Позначте **AlliancePay**, щоб покупець міг вибрати цей шлюз у кошику.

![Рекурентний продукт із ціною у гривнях і платою за підключення](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2F0FSYcSKWJrVIGwaZi8VO%2Fwhmcs-ua-04-product-pricing.png?alt=media\&token=e11bafee-e5d4-4c50-93d3-863b69300037)

#### Активуйте модуль підписок <a href="#section-6" id="section-6"></a>

У **Configuration → System Settings → Addon Modules** знайдіть **AlliancePay Subscriptions** і натисніть **Activate**.

![AlliancePay Subscriptions у переліку додаткових модулів](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2F57yd223TLwMzWY6kT50D%2Fwhmcs-ua-06-addon-activate.png?alt=media\&token=253574b1-e6f3-4bb4-8567-941bc16bf10c)

Натисніть **Configure** і заповніть параметри.

| Параметр                       | Значення                                                                                                                             |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Default Category Indicator** | Значення `categorySubcategoryIndicator`, отримане від банку. Модуль підставить його у форму нового плану.                            |
| **Privileged Admin Role IDs**  | Ідентифікатори ролей через кому. Початкове значення — `1`. Ці ролі можуть змінювати ціну, архівувати плани та запускати **Run Now**. |
| **Access Control**             | Позначте ролі адміністраторів, яким потрібен доступ до модуля.                                                                       |

Натисніть **Save Changes**. Модуль створює таблиці `alliance_sub_*` під час активації або першого відкриття налаштувань шлюзу.

![Налаштування категорії та адміністративних ролей у модулі підписок](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FIh42OqxSY6DjJi3NM7QS%2Fwhmcs-ua-07-addon-configure.png?alt=media\&token=a082ab83-ee87-4723-bf15-f1bf46e387ff)

#### Створіть план <a href="#section-7" id="section-7"></a>

**1.** Відкрийте **Addons → AlliancePay Subscriptions → Новий план**. Виберіть продукт, платіжний цикл і натисніть **Далі**.

![Перший крок створення плану — товар і платіжний цикл](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FB0ZVDo3kxRav2xvhkrWA%2Fwhmcs-ua-08-new-plan-step1.png?alt=media\&token=dcaff472-bf1a-43a2-b65f-43bfd7b2e974)

**2.** Звірте перший і наступні платежі у гривнях, інтервал, **Назву**, **Опис** та **Category indicator**. Натисніть **Створити план у банку**.

![Другий крок — розклад, суми платежів і підтвердження створення плану](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2F1AxVX9jKZGIoR27DQ50V%2Fwhmcs-ua-08-new-plan-step2.png?alt=media\&token=5e54912c-e2ff-44ca-9884-871b68a5f25d)

#### Перевірте результат <a href="#section-8" id="section-8"></a>

Відкрийте вкладку **Плани**. Для плану, доступного покупцям, перевірте три значення: **Статус — ACTIVE**, **Синхр. — OK**, **Новим клієнтам — так**. Якщо банк уже створив план, але синхронізація безстрокового розкладу завершилася зі статусом **ERROR**, натисніть **Повторити синхронізацію** для цього плану.

![Список планів зі статусом, станом синхронізації та кількістю активних підписок](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FTzAt8DXLe82blr5KEaJN%2Fwhmcs-ua-10-plans-list.png?alt=media\&token=839fec67-2905-4ffb-8b7e-807fb777ddef)

Натисніть **Дані з банку**. Модуль отримає актуальні дані провайдера. Зіставте версію плану, суми й інтервали в таблиці правил із локальним розкладом. Лічильник банку може також охоплювати підписки, оформлені поза WHMCS.

![Деталі плану з локальним розкладом, даними банку й результатом звірки правил](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2F7W7qVsBdPO5LSCDvK1Lo%2Fwhmcs-ua-11-plan-details.png?alt=media\&token=0b702b35-3a3e-4fd9-885a-e9e39c05c226)
