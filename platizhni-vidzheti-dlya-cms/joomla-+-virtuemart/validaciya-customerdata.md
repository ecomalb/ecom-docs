---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Валідація customerData

### Загальний опис логіки валідації <a href="#zagalnii-opis-logiki-validaciyi" id="zagalnii-opis-logiki-validaciyi"></a>

Перед відправкою даних, плагін формує масив у методі `prepareCustomerData()`, використовуючи платіжну адресу платника (об'єкт `BT` — BillTo) з VirtueMart. Після цього дані передаються в сервіс `ValidateCustomerData`.

<table data-header-hidden><thead><tr><th width="172"></th><th width="84"></th><th width="85"></th><th width="87"></th><th width="126"></th><th></th></tr></thead><tbody><tr><td><strong>Назва поля</strong></td><td><strong>Тип даних</strong></td><td><strong>Обов'язкове</strong></td><td><strong>Макс. довжина</strong></td><td><strong>Джерело даних у VirtueMart (BT / Моделі)</strong></td><td><strong>Особливі правила валідації та фільтрації</strong></td></tr><tr><td><strong>senderCustomerId</strong></td><td><code>string</code></td><td><strong>Так</strong></td><td>255</td><td><code>$bt->customer_number</code></td><td>Якщо порожнє, весь запис поля ігнорується.</td></tr><tr><td><strong>senderFirstName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>$bt->first_name</code></td><td><ol start="1"><li><strong>Регулярний вираз:</strong> Дозволені літери, цифри, дефіси, апострофи. Без спецсимволів по краях.</li></ol><p> </p><ol start="2"><li><strong>Не лише цифри:</strong> Блокується, якщо складається тільки з цифр.</li></ol><p> </p><ol start="3"><li><strong>Стоп-слова (частковий збіг):</strong> <code>NULL</code>, <code>3D SECURE</code>, <code>SURNAME</code>, <code>CARDHOLDER</code>, <code>UNKNOWN</code>. Якщо знайдено, поле видаляється.</li></ol></td></tr><tr><td><strong>senderLastName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>$bt->last_name</code></td><td>Аналогічно до <code>senderFirstName</code> (крім перевірки стоп-слів).</td></tr><tr><td><strong>senderMiddleName</strong></td><td><code>string</code></td><td>Ні</td><td>30</td><td><code>$bt->middle_name</code></td><td><strong>Нове поле.</strong> Проходить аналогічну валідацію, як і <code>senderLastName</code>.</td></tr><tr><td><strong>senderEmail</strong></td><td><code>string</code></td><td>Ні</td><td>256</td><td><code>$bt->email</code></td><td>Стандартне обрізання до 256 символів.</td></tr><tr><td><strong>senderCountry</strong></td><td><code>string</code></td><td>Ні</td><td>3</td><td><code>$country->country_num_code</code></td><td>Завантажується через <code>VmModel::getModel('country')</code> на основі ID країни платника. Передає числовий код ISO.</td></tr><tr><td><strong>senderRegion</strong></td><td><code>string</code></td><td>Ні</td><td>255</td><td><code>$state->state_name</code></td><td>Завантажується через <code>VmModel::getModel('state')</code> на основі ID регіону платника.</td></tr><tr><td><strong>senderCity</strong></td><td><code>string</code></td><td>Ні</td><td>25</td><td><code>$bt->city</code></td><td>Обрізається до 25 символів, якщо довше.</td></tr><tr><td><strong>senderStreet</strong></td><td><code>string</code></td><td>Ні</td><td>35</td><td><code>$bt->address_1</code></td><td>Обрізається до 35 символів, якщо довше.</td></tr><tr><td><strong>senderAdditionalAddress</strong></td><td><code>string</code></td><td>Ні</td><td>255</td><td><code>$bt->address_2</code></td><td>Обрізається до 255 символів, якщо довше.</td></tr><tr><td><strong>senderIp</strong></td><td><code>ip</code></td><td>Ні</td><td>—</td><td><code>$bt->ip_address</code></td><td><strong>Нова логіка:</strong> Перевіряється через PHP <code>FILTER_VALIDATE_IP</code>. Якщо IP невалідний — поле повністю видаляється із фінального масиву.</td></tr><tr><td><strong>senderPhone</strong></td><td><code>numeric_string</code></td><td>Ні</td><td>20</td><td><code>$bt->phone_1</code> або <code>$bt->phone_2</code></td><td>Фолбек: якщо <code>phone_1</code> порожній, береться <code>phone_2</code>. <strong>Фільтрація:</strong> Видаляються абсолютно всі нецифрові символи.</td></tr><tr><td><strong>senderZipCode</strong></td><td><code>string</code></td><td>Ні</td><td>50</td><td><code>$bt->zip</code></td><td>Обрізається до 50 символів, якщо довше.</td></tr></tbody></table>
