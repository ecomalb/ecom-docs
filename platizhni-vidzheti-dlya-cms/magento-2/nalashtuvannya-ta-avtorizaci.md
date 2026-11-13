---
description: >-
  Як підключити AlliancePay через JWS, вибрати тип оплати та налаштувати статуси
  замовлень і підписки в Magento 2.
---

# Налаштування та авторизація

У панелі Magento відкрийте **Stores → Configuration → Sales → Payment Methods → Alliance Payment**. Підготуйте адресу API для вашого середовища, Merchant Id і реквізити для підпису запитів.

### Підключення через Авторизацію 2.0 (JWS)

Починаючи з версії 1.6.0 модуль підписує запити до AlliancePay алгоритмом `RS256`. Підготуйте пару RSA-ключів. Передайте банку публічний ключ і отримайте його ідентифікатор `kid`. Приватний ключ залишається у мерчанта.

| Поле в Magento  | Що вказати                                                                                                                                       |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| API URL         | Базову адресу API, яку банк надав для вибраного середовища.                                                                                      |
| Merchant Id     | Ідентифікатор мерчанта у цьому середовищі.                                                                                                       |
| JWS Private Key | Повний приватний RSA-ключ у форматі PEM (PKCS#8). Збережіть переноси рядків і межі `-----BEGIN PRIVATE KEY-----` та `-----END PRIVATE KEY-----`. |
| JWS Key ID      | Значення `kid`, під яким банк зареєстрував відповідний публічний ключ.                                                                           |

![Поля API URL, Merchant Id, JWS Private Key і JWS Key ID у Magento](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2Fuigl46W8JeEmea5NoxVm%2Fmagento2-jws.png?alt=media\&token=1a0f56b4-c641-4b1f-a5fe-12480f846c43)

### Налаштування способу оплати

У **Enabled** виберіть **Yes**. У **Title** введіть назву, яку побачить покупець під час оформлення замовлення, наприклад **Alliance Pay**.

Поле **Status Payment Page Type** визначає, куди потрапить покупець після оплати. `STATUS_PAGE` показує результат на сторінці банку, `STATUS_TIMER_PAGE` повертає до магазину за таймером, а `STATUS_REDIRECT_MERCHANT_PAGE` одразу відкриває сторінку магазину.

У **Payment Type** виберіть режим, доступний для вашого термінала. `PURCHASE` — разова оплата, `A2A` — переказ з рахунку на рахунок, `PREAUTH` — резервування з подальшим списанням. Для A2A банк має підключити цей режим, а базовою валютою магазину має бути **UAH**.

![Увімкнення Alliance Pay, тип сторінки результату та вибір PREAUTH](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FF9ArBLvGWa51HqT12MyG%2Fmagento2-payment.png?alt=media\&token=241011a8-935e-42c3-9526-1f21f4ba88f5)

#### Параметри PREAUTH

| Поле                                 | Коли застосовується                                                                     |
| ------------------------------------ | --------------------------------------------------------------------------------------- |
| PreAuth Expiration Period            | Строк резервування. Доступні 2, 4, 6 або 12 годин та 1, 2, 7, 14 або 28 днів.           |
| PreAuth Created Order Status         | Статус замовлення після успішного резервування, наприклад Pending.                      |
| PreAuth Capture Success Order Status | Статус замовлення після успішного списання через рахунок Magento, наприклад Processing. |

#### Статуси оплати й повернення

У **Successful Payment Order Status** та **Failed Payment Order Status** задайте статуси замовлення для успішної та невдалої оплати. У **Successful Refund Order Status** та **Failed Refund Order Status** окремо задайте статуси для результатів повернення. На ілюстрації показано приклад налаштувань магазину.

![Строк резервування, статуси замовлень і журнал платежів](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FVtXJ4It6BBGxeTjJUYNv%2Fmagento2-states.png?alt=media\&token=5f555471-39f7-46e7-ab30-04c299eb28c8)

### Налаштування підписок

Починаючи з версії 1.7.0 відкрийте секцію **Alliance Subscriptions** у налаштуваннях платіжних методів. **Reprice Lead Time (days)** задає мінімальний строк між масовою зміною ціни та набуттям чинності новими правилами. Типове значення — 30 днів.

**Recurring Payment Amount Field Path** задає шлях до суми в об’єкті операції з callback рекурентного платежу. Модуль використовує її для звірки з планом. Типовий шлях у модулі — `coinAmount`. Перед зміною звірте шлях із фактичним форматом повідомлення провайдера.

![Налаштування строку зміни ціни та звірки суми підписки](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FUSLLAJlhgJ3Z56cUXAh2%2Fmagento2-subconfig.png?alt=media\&token=75abca73-ba46-4da6-8c2a-120eda877907)

### Збереження та перевірка

Натисніть **Save Config** та очистіть кеш конфігурації Magento. Створіть тестове замовлення у відповідному середовищі й перевірте операцію в **Sales → Orders → View → Alliance Payment Status**.

Модуль перевіряє підпис JWS у повідомленнях банку за його публічним ключем. Якщо перевірка підпису callback завершується помилкою, модуль відхиляє оновлення. Для діагностики використовуйте **Enable Payment Logs** і журнал `var/log/alliance_payment.log`.
