---
description: '{{url}}/ecom/execute_request/payments/v4/account_to_card'
---

# A2C

Максимальна сума запиту операції А2С становить 29999.00 грн.&#x20;

Перевищення граничної суми супроводжуєтсья помилкою:

```json
ERROR: @Payment coin amount exceeds the limit
```

**Вхідні параметри:**

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="135">Формат даних</th><th width="92.7900390625">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статусоперації якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>encryptedCardNumber</td><td>номер картки отримувача зашифрованый в JWE за допомогою платіжного ключа</td><td>string</td><td>Так</td><td>5473670000000304 (розшифрованний вид)</td></tr><tr><td>coinAmount</td><td>сума платежу в копійках</td><td>int</td><td>Так</td><td>2000</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string</td><td>Ні</td><td>https://merchant.notification_url</td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>comment</td><td>Додаткова інформація про платіж</td><td>string</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>Призначення платежу</td><td>string</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>senderAccount</td><td>Рахунок відправника</td><td>string</td><td>Ні</td><td>2900000000000</td></tr><tr><td>customerData</td><td>об'єкт з customer даними</td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Ні</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td>IP адреса відправника</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>індекс відправника</td><td>string (50)</td><td>Ні</td><td>49000</td></tr><tr><td>recipientCustomerId</td><td>Id клієнта отримувача</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>recipientFirstName</td><td>ім'я отримувача </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>recipientLastName</td><td>прізвище отримувача</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>recipientMiddleName</td><td>по-батькові отримувача</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>recipientEmail</td><td>пошта отримувача</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>recipientСountry</td><td>країна отримувача</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>recipientRegion</td><td>область отримувача</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>recipientСity</td><td>місто отримувача</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>recipientStreet</td><td>вулиця отримувача</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>recipientAdditionalAddress</td><td>додаткові дані адреси отримувача (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>recipientItn</td><td>іпн отримувача<br><br>У разі, якщо фізична особа офіційно відмовилась від отримання ІПН, необхідно передавати альтернативний параметр — <code>recipientPassport</code> з коректними паспортними даними отримувача.</td><td>string (20)</td><td>Так, якщо не вказан recipientPassport</td><td>123456789</td></tr><tr><td>recipientPassport</td><td>паспорт отримувача</td><td>string (255)</td><td>Так, якщо не вказан recipientItn</td><td>АН123456</td></tr><tr><td>recipientIp</td><td>IP адреса клієнта отримувача</td><td>string (50)</td><td>Ні</td><td>123.12.12.12</td></tr><tr><td>recipientPhone</td><td>номер телефону отримувача</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>recipientBirthday</td><td>день народження отримувача</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>recipientGender</td><td>Гендер отримувача</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>recipientZipCode</td><td>індекс отримувача</td><td>string (50)</td><td>Ні</td><td>49000</td></tr></tbody></table>

**Вихідні параметри:**

| Параметр                   | Опис                                                                 | Формат даних | Приклад                                                                                                                                                                                                |
| -------------------------- | -------------------------------------------------------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                       | тип транзакції                                                       | string       | ACCOUNT\_2\_CARD                                                                                                                                                                                       |
| rrn                        | rrn номер транзакції в МПС                                           | string       | 2554256963                                                                                                                                                                                             |
| purpose                    | призначення платежу                                                  | string       | За товар                                                                                                                                                                                               |
| comment                    | коментар                                                             | string       | тест                                                                                                                                                                                                   |
| coinAmount                 | сума платежу                                                         | int          | 2000                                                                                                                                                                                                   |
| merchantId                 | Id мерчанту                                                          | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId                | Id транзакціі                                                        | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId            | Id транзакціі в системі Ecom                                         | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName               | найменування торговця                                                | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode               | код авторизаціі                                                      | string       | 39203                                                                                                                                                                                                  |
| status                     | статус транзакціі                                                    | string       | SUСCESS FAIL PENDING REQUIRED\_3DS DESIRED\_THREEDS\_MODE\_ERROR                                                                                                                                       |
| transactionType            | тип транзакції у цифровому значенні                                  | string       | 46                                                                                                                                                                                                     |
| merchantRequestId          | Id запиту мерчанта                                                   | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency        | валюта платежу                                                       | string       | 980                                                                                                                                                                                                    |
| merchantCommission         | сума комісії                                                         | string       | 2                                                                                                                                                                                                      |
| createDateTime             | дата створення платежу                                               | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime       | дата модифікаціі платежу                                             | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode                 | код відповіді                                                        | string       | 0                                                                                                                                                                                                      |
| responseCode               | деталі відповіді                                                     | string       | 0                                                                                                                                                                                                      |
| description                | опис відповіді                                                       | string       | approved                                                                                                                                                                                               |
| bankCode                   | назва банку емітента                                                 | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem              | назва мпс емітента                                                   | string       | MasterCard                                                                                                                                                                                             |
| productType                | тип продукту термінала                                               | string       | A2C                                                                                                                                                                                                    |
| notificationUrl            | url, на який відправлено CallBack                                    | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType         | тип оплати                                                           | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption     | ознака криптування данних CallBack                                   | string       | true/false Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані                                                                                                     |
| cardNumberMask             | маскований номер карти                                               | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode         | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні. | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode                | параметр який вказує, використовувася 3DS у покупці чи ні            | string       | MUST- проводимо оплату з 3DS MUST\_NOT- проводимо оплату без 3DS                                                                                                                                       |
| statusThreeDs              | статус проведення 3DS                                                | string       | Y - успіший 3ds N - не успішний 3ds                                                                                                                                                                    |
| threeDSServerTransId       | Id транзакціі в системі 3ds                                          | string       | b6c35fdb-28c1-454d-a2f3-51098c26bda4                                                                                                                                                                   |
| processingMerchantId       | Id мерчанту в ПЦ                                                     | string       | AE100000                                                                                                                                                                                               |
| processingTerminalId       | Id терміналу в ПЦ                                                    | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl             | url для редиректа клієнта на сторінку емітента для проходження 3DS   | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                    | під тип транзакціі                                                   | enum         | Можливі значення: NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається                                                                                          |
| senderCustomerId           | Id клієнта відправника                                               | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName            | ім'я відправника                                                     | string       | Іваненко                                                                                                                                                                                               |
| senderLastName             | прізвище відправника                                                 | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName           | по-батькові відправника                                              | string       | Іванович                                                                                                                                                                                               |
| senderEmail                | пошта відправника                                                    | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| senderCountry              | країна відправника                                                   | string       | Україна                                                                                                                                                                                                |
| senderRegion               | область відправника                                                  | string       | Київська                                                                                                                                                                                               |
| senderCity                 | місто відправника                                                    | string       | Київ                                                                                                                                                                                                   |
| senderStreet               | вулиця відправника                                                   | string       | Січових стрільців                                                                                                                                                                                      |
| senderAdditionalAddress    | додаткові дані адреси відправника (поверх, номер дому, квартира)     | string       | 23                                                                                                                                                                                                     |
| senderItn                  | іпн відправника                                                      | string       | 123456789                                                                                                                                                                                              |
| senderPassport             | паспорт відправника                                                  | string       | АН123456                                                                                                                                                                                               |
| senderIp                   | ip адреса відправника                                                | string       | 123.12.12.12                                                                                                                                                                                           |
| senderPhone                | номер телефону відправника                                           | string       | 380630000000                                                                                                                                                                                           |
| senderBirthday             | день народження відправника                                          | string       | 31.12.2000                                                                                                                                                                                             |
| senderGender               | гендер відправника                                                   | string       | M                                                                                                                                                                                                      |
| senderZipCode              | індекс відправника                                                   | string       | 12000                                                                                                                                                                                                  |
| senderBankCode             | назва банку емітента відправника                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| senderPaymentSystem        | назва мпс емітента відправника                                       | string       | MasterCard                                                                                                                                                                                             |
| senderCardNumberMask       | маскований номер карти відправника                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| recipientCustomerId        | Id клієнта відправника                                               | string       | 1258728c1                                                                                                                                                                                              |
| recipientFirstName         | ім'я отримувача                                                      | string       | Іваненко                                                                                                                                                                                               |
| recipientLastName          | прізвище отримувача                                                  | string       | Іван                                                                                                                                                                                                   |
| recipientMiddleName        | по-батькові отримувача                                               | string       | Іванович                                                                                                                                                                                               |
| recipientEmail             | пошта отримувача                                                     | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| recipientCountry           | країна отримувача                                                    | string       | Україна                                                                                                                                                                                                |
| recipientRegion            | область отримувача                                                   | string       | Київська                                                                                                                                                                                               |
| recipientCity              | місто отримувача                                                     | string       | Київ                                                                                                                                                                                                   |
| recipientStreet            | вулиця отримувача                                                    | string       | Січових стрільців                                                                                                                                                                                      |
| recipientAdditionalAddress | додаткові дані адреси отримувача (поверх, номер дому, квартира)      | string       | 23                                                                                                                                                                                                     |
| recipientItn               | іпн отримувача                                                       | string       | 123456789                                                                                                                                                                                              |
| recipientPassport          | паспорт отримувача                                                   | string       | АН123456                                                                                                                                                                                               |
| recipientIp                | ip адреса отримувача                                                 | string       | 123.12.12.12                                                                                                                                                                                           |
| recipientPhone             | номер телефону отримувача                                            | string       | 380630000000                                                                                                                                                                                           |
| recipientBirthday          | день народження отримувача                                           | string       | 31.12.2000                                                                                                                                                                                             |
| recipientGender            | гендер отримувача                                                    | string       | M                                                                                                                                                                                                      |
| recipientZipCode           | індекс отримувача                                                    | string       | 12000                                                                                                                                                                                                  |
| recipientBankCode          | назва банку емітента отримувача                                      | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| recipientPaymentSystem     | назва мпс емітента отримувача                                        | string       | MasterCard                                                                                                                                                                                             |
| recipientCardNumberMask    | маскований номер карти отримувача                                    | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |

**Приклад тіла запиту**

```json
{
"encryptedCardNumber":"{{encryptedPanT}}",
"merchantId":"137d9304-0368-11ed-b939-0242ac120002",
"merchantRequestId":"{{requestUUIDT}}",
"purpose":"за товар",
"coinAmount": 120,
"notificationUrl":"https://api-ecom-prod.bankalliance.ua/mock",
"ecomComment": "string",
"senderAccount": "UA12305299260022119999",
"customerData": {
        "senderCustomerId": "1234567",
        "senderFirstName": "John",
        "senderLastName": "Doe",
        "senderMiddleName": "Fall",
        "senderEmail": "test@gmail.com",
        "senderCountry": "sender_country",
        "senderRegion": "sender_region",
        "senderCity": "sender_city",
        "senderStreet": "sender_street",
        "senderAdditionalAddress": "N 6",
        "senderItn": "12345",
        "senderPassport": "12345",
        "senderIp": "165.222.87.224",
        "senderPhone": "380967542344",
        "senderBirthday": "12/12/2000",
        "senderGender": "Male",
        "senderZipCode": "12345",
        "recipientCustomerId": "1234567",
        "recipientFirstName": "Yura",
        "recipientLastName": "Bura",
        "recipientMiddleName": "TestMiddle",
        "recipientEmail": "res@gmail",
        "recipientCountry": "804",
        "recipientRegion": "res_reg",
        "recipientCity": "res_dnipro",
        "recipientStreet": "res_street",
        "recipientAdditionalAddress": "res_addres",
        "recipientItn": "res_iin",
        "recipientPassport": "res_pasport",
        "recipientIp": "165.222.87.224",
        "recipientPhone": "380967542344",
        "recipientBirthday": "12/12/2000",
        "recipientGender": "Female",
        "recipientZipCode": "77777"
    },
"date": "{{currentdateT}}.00+00:00"
}
```

**Приклад тіла відповіді**

```json
{
    "type": "ACCOUNT_2_CARD",
    "rrn": "410208187340",
    "purpose": "за товар",
    "comment": null,
    "coinAmount": 120,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712822901491QtPAxAWOrrg",
    "ecomOperationId": "ff1ae4eb-d66d-467e-896d-01ed579bd040",
    "merchantName": null,
    "approvalCode": null,
    "status": "PENDING",
    "transactionType": 46,
    "merchantRequestId": "cf17607f-c1f8-4e8e-abb2-5fd1b3dd17ec",
    "transactionCurrency": "980",
    "merchantCommission": null,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": "Операція успішна"
    },
    "bankCode": null,
    "paymentSystem": null,
    "productType": "A2C",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": "CARD",
    "notificationEncryption": false,
    "senderAccount": "UA12305299260022119999",
    "recipientCardNumberMask": null,
    "senderCustomerId": null,
    "senderFirstName": "Petro",
    "senderLastName": "Petrenko",
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": "803",
    "senderRegion": null,
    "senderCity": "Kyiv",
    "senderStreet": "L.Ukrainki01",
    "senderAdditionalAddress": null,
    "senderItn": null,
    "senderPassport": null,
    "senderIp": null,
    "senderPhone": null,
    "senderBirthday": null,
    "senderGender": null,
    "senderZipCode": null,
    "recipientCustomerId": null,
    "recipientFirstName": "TestFirstname",
    "recipientLastName": "TestLastName",
    "recipientMiddleName": null,
    "recipientEmail": null,
    "recipientCountry": "803",
    "recipientRegion": null,
    "recipientCity": "Kyiv",
    "recipientStreet": "T. Shevchenka, 11",
    "recipientAdditionalAddress": null,
    "recipientItn": null,
    "recipientPassport": null,
    "recipientIp": null,
    "recipientPhone": null,
    "recipientBirthday": null,
    "recipientGender": null,
    "recipientZipCode": null,
    "recipientBankCode": null,
    "recipientPaymentSystem": null
}
```
