# Валідація customerData

Коли покупець натискає **Оплатити**, WHMCS передає POST-параметр `alliancepay_action=create_order`. Шлюз бере дані з `$params['clientdetails']`, формує `customerData` і передає замовлення до `OrderRequestDTO::fromArray($orderData)`.

| Поле customerData         | Тип             | Обов’язкове | Джерело у clientdetails   | Як шлюз формує значення                                                                                                            |
| ------------------------- | --------------- | ----------- | ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `senderCustomerId`        | string          | Так         | `userid`                  | Приводить ID авторизованого клієнта до рядка.                                                                                      |
| `senderFirstName`         | string          | Ні          | `firstname`               | Передає ім’я в SDK.                                                                                                                |
| `senderLastName`          | string          | Ні          | `lastname`                | Передає прізвище в SDK.                                                                                                            |
| `senderEmail`             | string          | Ні          | `email`                   | Передає електронну адресу.                                                                                                         |
| `senderCountry`           | string          | Ні          | `countrycode`             | Через `League\ISO3166` перетворює дволітерний код на числовий код ISO, наприклад `UA` → `804`. За відсутності коду пропускає поле. |
| `senderRegion`            | string          | Ні          | `state`                   | Передає назву області або штату.                                                                                                   |
| `senderCity`              | string          | Ні          | `city`                    | Передає назву міста.                                                                                                               |
| `senderStreet`            | string          | Ні          | `address1`                | Передає перший рядок адреси.                                                                                                       |
| `senderAdditionalAddress` | string          | Ні          | `address2`                | Передає другий рядок адреси.                                                                                                       |
| `senderZipCode`           | string          | Ні          | `postcode`                | Передає поштовий індекс.                                                                                                           |
| `senderPhone`             | numeric\_string | Ні          | `phonecc` і `phonenumber` | З’єднує код країни й номер без додаткового роздільника. SDK перевіряє, що результат складається із цифр.                           |

Очищення даних і перевірки `max_len`, `pattern` та `stop_words` виконує PHP SDK. Якщо створення DTO завершується винятком, шлюз записує помилку через `logModuleCall`. Покупець бачить загальне повідомлення, а адміністратор може перевірити деталі в **Module Log**.
