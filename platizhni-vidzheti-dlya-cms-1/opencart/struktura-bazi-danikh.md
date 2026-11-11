---
description: >-
  Таблиці платежів, повернень і підписок, відмінності OpenCart 3 та 4 і
  зберігання параметрів Авторизації 2.0.
---

# Структура бази даних

Модулі AlliancePay зберігають дані платежів, повернень і підписок у таблицях OpenCart. У назвах нижче не вказано префікс: до кожної таблиці додається значення `DB_PREFIX` вашого магазину, наприклад `oc_alliance_checkout_integration_order`.

### Таблиці платіжного модуля

| Таблиця                                        | Призначення                                                                | OpenCart   |
| ---------------------------------------------- | -------------------------------------------------------------------------- | ---------- |
| `alliance_checkout_integration_order`          | Платіжні дані замовлення, статус, ідентифікатори операцій і дані callback. | 3.0 та 4.0 |
| `alliance_integration_order_refund`            | Історія операцій повернення коштів.                                        | 3.0 та 4.0 |
| `alliance_checkout_integration_order_callback` | Службова таблиця, яку створює ініціалізація БД модуля OpenCart 4.          | 4.0        |

Для звичайних платежів OpenCart 3 створює дві таблиці — замовлень і повернень; OpenCart 4 — три таблиці, наведені вище. Таблиці підписок описано окремо нижче.

В обох версіях обробник callback оновлює `alliance_checkout_integration_order` і зберігає отримані дані в полі `callback_data`. Для діагностики платежу використовуйте цей запис. Наявність окремої таблиці `alliance_checkout_integration_order_callback` в OpenCart 4 не означає, що вона є журналом усіх отриманих callback.

### Дані замовлення

Таблиця `alliance_checkout_integration_order`. Первинний ключ — `order_id`, ідентифікатор замовлення OpenCart.

| Поле                                              | Тип                                      | Опис                                                                      |
| ------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------- |
| `order_id`                                        | INT(11)                                  | Ідентифікатор замовлення OpenCart; PRIMARY KEY.                           |
| `merchant_request_id`, `merchant_id`              | VARCHAR(255)                             | Ідентифікатори запиту мерчанта та мерчанта.                               |
| `hpp_order_id`, `ecom_order_id`, `operation_id`   | VARCHAR(255)                             | Ідентифікатори HPP-замовлення, замовлення платформи та операції.          |
| `coin_amount`                                     | INT(11)                                  | Сума платежу в найменших одиницях валюти.                                 |
| `original_authorized_amount`                      | INT(11), NULL                            | Початкова сума авторизації.                                               |
| `currency_code`                                   | INT(3), NULL                             | Числовий код валюти.                                                      |
| `conversion_rate`                                 | DECIMAL(18,6) у 3.0; DECIMAL(20,6) у 4.0 | Курс конвертації, якщо його отримано у відповіді; допускає NULL.          |
| `hpp_pay_type`                                    | VARCHAR(50)                              | Тип платежу: PURCHASE, A2A або PREAUTH.                                   |
| `order_status`                                    | VARCHAR(50)                              | Статус замовлення на платіжній платформі.                                 |
| `payment_methods`                                 | TEXT                                     | Способи оплати для HPP-замовлення.                                        |
| `is_callback_returned`                            | BOOLEAN, DEFAULT FALSE                   | Ознака отримання callback.                                                |
| `callback_data`                                   | LONGTEXT                                 | Дані callback у форматі JSON, зокрема дані операцій.                      |
| `create_date`, `updated_at`, `expired_order_date` | DATETIME                                 | Дата створення, останнього оновлення та завершення строку дії замовлення. |

Додаткові індекси передбачено для `merchant_request_id`, `hpp_order_id` та `merchant_id`.

### Дані повернення коштів

Таблиця `alliance_integration_order_refund`. Кожне повернення має власний `refund_id` — первинний ключ з AUTO\_INCREMENT. Поле `order_id` пов’язує повернення із замовленням OpenCart; для одного замовлення може бути кілька записів повернення.

| Основні поля                                                               | Опис                                                                                               |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `refund_id`, `order_id`                                                    | Ідентифікатори запису повернення та замовлення.                                                    |
| `operation_id`, `ecom_operation_id`, `merchant_request_id`                 | Ідентифікатори операції повернення та запиту мерчанта.                                             |
| `original_operation_id`, `original_ecom_operation_id`, `rrn_original`      | Посилання на початкову платіжну операцію.                                                          |
| `coin_amount`, `original_coin_amount`, `transaction_currency`              | Сума повернення, початкова сума та валюта операції. Суми зберігаються в найменших одиницях валюти. |
| `status`, `type`, `transaction_type`                                       | Статус і тип операції.                                                                             |
| `action_code`, `response_code`, `description`, `transaction_response_info` | Результат обробки та діагностична інформація.                                                      |
| `purpose`, `comment`                                                       | Призначення та коментар до повернення.                                                             |
| `create_date_time`, `modification_date_time`                               | Дата створення й останньої зміни операції.                                                         |

### Таблиці підписок

В OpenCart 3 ці таблиці створюються під час встановлення окремого модуля **Alliance Підписки**. В OpenCart 4 їх створює платіжний модуль методом `initSubscriptionTables()`.

| Таблиця                                      | Призначення                                                                                                                                                                 |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `alliance_subscription_plan_template`        | Шаблони планів: код, назва, категорія та правила `rules_template`.                                                                                                          |
| `alliance_subscription_plan`                 | Плани для товарів: `product_id`, `template_id`, `provider_plan_id`, унікальний `plan_key`, правила `rules`, версія, активність і стан синхронізації.                        |
| `alliance_subscription`                      | Оформлені підписки: замовлення, покупець, план, `provider_order_id`, знімок правил `rules_snapshot`, статус і `callback_data`.                                              |
| `alliance_scheduled_payment`                 | Платежі за розкладом: підписка, ідентифікатор платежу провайдера, статус, запланована й фактична дати виконання, `operation_id` та кількість повторних спроб `retry_count`. |
| `alliance_subscription_plan_version_history` | Історія зміни планів: попередня й нова версії та правила, дата набуття чинності, причина й автор зміни.                                                                     |
| `alliance_subscription_audit_log`            | Журнал дій із планами: тип події `action`, пов’язані ідентифікатори та подробиці `details`.                                                                                 |

#### Відмінності полів OpenCart 3 і 4

| Призначення                                    | OpenCart 3.0               | OpenCart 4.0                    |
| ---------------------------------------------- | -------------------------- | ------------------------------- |
| Ідентифікатор плану та посилання на план       | `plan_id`                  | `subscription_plan_id`          |
| Первинний ключ запланованого платежу           | `scheduled_payment_row_id` | `scheduled_payment_id`          |
| Ідентифікатор запланованого платежу провайдера | `scheduled_payment_id`     | `provider_scheduled_payment_id` |
| Первинний ключ історії версій                  | `history_id`               | `version_history_id`            |
| Первинний ключ журналу аудиту                  | `audit_id`                 | `audit_log_id`                  |
| Дати створення й оновлення в таблицях підписок | `created_at`, `updated_at` | `date_added`, `date_modified`   |

В OpenCart 3 для контролю сум також використовуються `amount_review_flag` у підписці та `expected_coin_amount`, `actual_coin_amount`, `amount_mismatch_flag` у запланованому платежі. Ці поля не входять до наведеної схеми OpenCart 4.

### Налаштування Авторизації 2.0

Параметри модуля зберігаються у стандартній таблиці налаштувань OpenCart `setting` з префіксом магазину, у групі `payment_alliance`. Окрема таблиця для JWS-авторизації не створюється.

| Ключ налаштування                  | Призначення                                         |
| ---------------------------------- | --------------------------------------------------- |
| `payment_alliance_jws_private_key` | Приватний RSA-ключ для підпису JWS.                 |
| `payment_alliance_jws_key_id`      | Ідентифікатор ключа `kid`, зареєстрованого в банку. |

Заповнення цих параметрів описано в розділі [Налаштування та авторизація](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/opencart/nalashtuvannya-ta-avtorizaciya).

### Валідація customerData

### Загальний опис логіки валідації <a href="#zagalnii-opis-logiki-validaciyi" id="zagalnii-opis-logiki-validaciyi"></a>

Перед відправкою запиту на створення замовлення (`CREATE_ORDER`), дані клієнта проходять фільтрацію в методі `validateCustomerData()`.

> **Важливо для розробників:** > Якщо поле не проходить хоча б одне правило валідації, воно **повністю видаляється** з фінального масиву `customerData`, а подія логується в системний лог OpenCart (`Payment Aggregation Error...`). Винятком є обов'язкові поля — їхня відсутність або невалідність також призведе до видалення, що може спричинити помилку на стороні платіжного шлюзу.

&#x20;

<table data-header-hidden><thead><tr><th width="144">Назва поля</th><th width="82">Тип даних</th><th width="77">Обов'язкове</th><th width="96">Макс. довжина</th><th>Звідки береться в OpenCart (Джерело)</th><th>Особливі правила валідації та фільтрації</th></tr></thead><tbody><tr><td><strong>senderCustomerId</strong></td><td><code>string</code></td><td><strong>Так</strong></td><td>255</td><td><code>customer_id</code> замовлення. Якщо покупець гість: <code>'guest_' . order_id</code> або <code>uniqid()</code>.</td><td>Немає додаткових фільтрів.</td></tr><tr><td><strong>senderFirstName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>firstname</code> з адреси платника.</td><td><ol start="1"><li><strong>Регулярний вираз:</strong> Дозволені літери (укр/анг/рус), цифри, пробіли, дефіси, апострофи. Пробіли/дефіси не можуть бути на початку чи в кінці.</li></ol><p> </p><ol start="2"><li><strong>Не лише цифри:</strong> Не може складатися тільки з цифр.</li></ol><p> </p><ol start="3"><li><strong>Стоп-слова (case-insensitive):</strong> <code>NULL</code>, <code>3D SECURE</code>, <code>SURNAME</code>, <code>CARDHOLDER</code>, <code>UNKNOWN</code>.</li></ol></td></tr><tr><td><strong>senderLastName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>lastname</code> з адреси платника.</td><td><ol start="1"><li><strong>Регулярний вираз:</strong> Аналогічно до <code>senderFirstName</code>.</li></ol><p> </p><ol start="2"><li><strong>Не лише цифри:</strong> Не може складатися тільки з цифр.</li></ol></td></tr><tr><td><strong>senderEmail</strong></td><td><code>string</code></td><td>Ні</td><td>256</td><td><code>email</code> з даних замовлення.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderCountry</strong></td><td><code>string</code></td><td>Ні</td><td>3</td><td><code>payment_iso_code_2</code> або <code>shipping_iso_code_2</code>.</td><td><strong>Трансформація:</strong> Двозначний код країни (Alpha-2) конвертується в <strong>цифровий код країни</strong> (Numeric ISO) через <code>AllianceCountryCodeProvider</code>.</td></tr><tr><td><strong>senderRegion</strong></td><td><code>string</code></td><td>Ні</td><td>255</td><td><code>payment_zone</code> або <code>shipping_zone</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderCity</strong></td><td><code>string</code></td><td>Ні</td><td>25</td><td><code>payment_city</code> або <code>shipping_city</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderStreet</strong></td><td><code>string</code></td><td>Ні</td><td>35</td><td><code>payment_address_1</code> або <code>shipping_address_1</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderAdditionalAddress</strong></td><td><code>string</code></td><td>Ні</td><td>255</td><td><code>payment_address_2</code> або <code>shipping_address_2</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderIp</strong></td><td><code>string</code></td><td>Ні</td><td>50</td><td><code>ip</code> замовлення або <code>REMOTE_ADDR</code> з сервера.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderPhone</strong></td><td><code>numeric_string</code></td><td>Ні</td><td>20</td><td><code>telephone</code> з даних замовлення.</td><td><strong>Попередня фільтрація:</strong> Зі строки видаляються всі нецифрові символи (<code>+</code>, <code>-</code>, <code>(</code>, <code>)</code>, пробіли) перед перевіркою довжини.</td></tr><tr><td><strong>senderZipCode</strong></td><td><code>string</code></td><td>Ні</td><td>50</td><td><code>payment_postcode</code> або <code>shipping_postcode</code>.</td><td>Стандартна перевірка довжини.</td></tr></tbody></table>

<br>
