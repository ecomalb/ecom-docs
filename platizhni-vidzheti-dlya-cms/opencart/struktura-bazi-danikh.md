# Структура бази даних

## Цей модуль додає 2 таблиці в БД:&#x20;

* [**`alliance_checkout_integration_order`**](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/opencart/struktura-bazi-danikh#struktra-tablici-alliance_checkout_integration_order)&#x20;
* [**`alliance_checkout_integration_order_callback`**](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/opencart/struktura-bazi-danikh#struktra-tablici-alliance_checkout_integration_order_callback)&#x20;

### Структра таблиці **`alliance_checkout_integration_order`**

<figure><img src="../../.gitbook/assets/image (12) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Структра таблиці **`alliance_checkout_integration_order_callback`**

<figure><img src="../../.gitbook/assets/image (14) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Валідація customerData

### Загальний опис логіки валідації <a href="#zagalnii-opis-logiki-validaciyi" id="zagalnii-opis-logiki-validaciyi"></a>

Перед відправкою запиту на створення замовлення (`CREATE_ORDER`), дані клієнта проходять фільтрацію в методі `validateCustomerData()`.

> **Важливо для розробників:** > Якщо поле не проходить хоча б одне правило валідації, воно **повністю видаляється** з фінального масиву `customerData`, а подія логується в системний лог OpenCart (`Payment Aggregation Error...`). Винятком є обов'язкові поля — їхня відсутність або невалідність також призведе до видалення, що може спричинити помилку на стороні платіжного шлюзу.

&#x20;

<table data-header-hidden><thead><tr><th width="144">Назва поля</th><th width="82">Тип даних</th><th width="77">Обов'язкове</th><th width="96">Макс. довжина</th><th>Звідки береться в OpenCart (Джерело)</th><th>Особливі правила валідації та фільтрації</th></tr></thead><tbody><tr><td><strong>senderCustomerId</strong></td><td><code>string</code></td><td><strong>Так</strong></td><td>255</td><td><code>customer_id</code> замовлення. Якщо покупець гість: <code>'guest_' . order_id</code> або <code>uniqid()</code>.</td><td>Немає додаткових фільтрів.</td></tr><tr><td><strong>senderFirstName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>firstname</code> з адреси платника.</td><td><ol start="1"><li><strong>Регулярний вираз:</strong> Дозволені літери (укр/анг/рус), цифри, пробіли, дефіси, апострофи. Пробіли/дефіси не можуть бути на початку чи в кінці.</li></ol><p> </p><ol start="2"><li><strong>Не лише цифри:</strong> Не може складатися тільки з цифр.</li></ol><p> </p><ol start="3"><li><strong>Стоп-слова (case-insensitive):</strong> <code>NULL</code>, <code>3D SECURE</code>, <code>SURNAME</code>, <code>CARDHOLDER</code>, <code>UNKNOWN</code>.</li></ol></td></tr><tr><td><strong>senderLastName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>lastname</code> з адреси платника.</td><td><ol start="1"><li><strong>Регулярний вираз:</strong> Аналогічно до <code>senderFirstName</code>.</li></ol><p> </p><ol start="2"><li><strong>Не лише цифри:</strong> Не може складатися тільки з цифр.</li></ol></td></tr><tr><td><strong>senderEmail</strong></td><td><code>string</code></td><td>Ні</td><td>256</td><td><code>email</code> з даних замовлення.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderCountry</strong></td><td><code>string</code></td><td>Ні</td><td>3</td><td><code>payment_iso_code_2</code> або <code>shipping_iso_code_2</code>.</td><td><strong>Трансформація:</strong> Двозначний код країни (Alpha-2) конвертується в <strong>цифровий код країни</strong> (Numeric ISO) через <code>AllianceCountryCodeProvider</code>.</td></tr><tr><td><strong>senderRegion</strong></td><td><code>string</code></td><td>Ні</td><td>255</td><td><code>payment_zone</code> або <code>shipping_zone</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderCity</strong></td><td><code>string</code></td><td>Ні</td><td>25</td><td><code>payment_city</code> або <code>shipping_city</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderStreet</strong></td><td><code>string</code></td><td>Ні</td><td>35</td><td><code>payment_address_1</code> або <code>shipping_address_1</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderAdditionalAddress</strong></td><td><code>string</code></td><td>Ні</td><td>255</td><td><code>payment_address_2</code> або <code>shipping_address_2</code>.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderIp</strong></td><td><code>string</code></td><td>Ні</td><td>50</td><td><code>ip</code> замовлення або <code>REMOTE_ADDR</code> з сервера.</td><td>Стандартна перевірка довжини.</td></tr><tr><td><strong>senderPhone</strong></td><td><code>numeric_string</code></td><td>Ні</td><td>20</td><td><code>telephone</code> з даних замовлення.</td><td><strong>Попередня фільтрація:</strong> Зі строки видаляються всі нецифрові символи (<code>+</code>, <code>-</code>, <code>(</code>, <code>)</code>, пробіли) перед перевіркою довжини.</td></tr><tr><td><strong>senderZipCode</strong></td><td><code>string</code></td><td>Ні</td><td>50</td><td><code>payment_postcode</code> або <code>shipping_postcode</code>.</td><td>Стандартна перевірка довжини.</td></tr></tbody></table>

<br>
