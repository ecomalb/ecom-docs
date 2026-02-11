---
description: '{{url}}/ecom/execute_request/payments/v3/apple_pay/card_to_account'
---

# Запит проведення C2A Крок 1

**Вхідні JSON параметри:**

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="290">Формат даних</th><th width="62">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>Об’єкт paymentData, який необхідно закриптувати платіжним ключем</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td>applicationPrimaryAccountNumber</td><td>номер рахунку картки, з якої фінансується ця транзакція</td><td>string</td><td>Так</td><td>4420642424203999</td></tr><tr><td>applicationExpirationDate</td><td>Термін дії картки у форматі YYMMDD</td><td>string</td><td>Так</td><td>261001</td></tr><tr><td>currencyCode</td><td>Цифровий код валюти ISO 4217</td><td>string</td><td>Так</td><td>980</td></tr><tr><td>transactionAmount</td><td>сума платежу в копійках</td><td>string</td><td>Так</td><td>2000</td></tr><tr><td>cardholderName</td><td>Ім'я власника картки</td><td>string</td><td>Ні</td><td>Іванченко Петро</td></tr><tr><td>deviceManufacturerIdentifier</td><td>Hex-encoded device manufacturer identifier</td><td>string</td><td>Так</td><td>1</td></tr><tr><td>paymentDataType</td><td> </td><td>string</td><td>Так</td><td>3DSecure</td></tr><tr><td>paymentData</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td>onlinePaymentCryptogram</td><td>Криптограма платежу у форматі Base64</td><td>string</td><td>Так</td><td>AVn0rK8BiDxN2D/w2j8LMAABAAA=</td></tr><tr><td>eciIndicator</td><td>ECI indicator</td><td>string(1)</td><td>Ні</td><td>7</td></tr><tr><td>Додаткові дані для проведення платежу</td><td> </td><td> </td><td> </td><td> </td></tr><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статус операції якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>desiredThreeDSMode</td><td>Ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string (50)</td><td>Так</td><td><p>За замовчуванням SHOULD</p><p>Можливі значення:</p><ul><li>MUST - мерчант вимагає проведення платежу з 3DS</li><li>MUST_NOT - примусова операція без 3DS</li><li>SHOULD - якщо картка підтримує 3DS, то робимо перевірку</li></ul></td></tr><tr><td>resultRedirectUrl</td><td>Url для редиректа клієнта після проходження 3DS аутентифікації</td><td>string (1000)</td><td>Ні</td><td><a href="https://support.google.com/"><img src="https://support.google.com/favicon.ico" alt="">Google Help</a></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td><a href="https://merchant.notification_url/">https://merchant.notification_url</a></td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+00:00</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>recipientAccount</td><td>Рахунок отримувача</td><td>string</td><td>Ні</td><td>2900000000000</td></tr><tr><td>customerData</td><td>об'єкт з customer даними</td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Так</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Так</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td><code class="expression">space.vars.senderIP_description</code></td><td>string (50) </td><td>Ні</td><td><code class="expression">space.vars.senderIP_example</code></td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>індекс відправника</td><td>string (50)</td><td>Ні</td><td>49000</td></tr><tr><td>recipientCustomerId</td><td>Id клієнта отримувача</td><td>string (255)</td><td>Ні</td><td>1258728c1</td></tr><tr><td>recipientFirstName</td><td>ім'я отримувача </td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>recipientLastName</td><td>прізвище отримувача</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>recipientMiddleName</td><td>по-батькові отримувача</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>recipientEmail</td><td>пошта отримувача</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>recipientСountry</td><td>країна отримувача</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>recipientRegion</td><td>область отримувача</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>recipientСity</td><td>місто отримувача</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>recipientStreet</td><td>вулиця отримувача</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>recipientAdditionalAddress</td><td>додаткові дані адреси отримувача (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>recipientItn</td><td>іпн отримувача</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>recipientPassport</td><td>паспорт отримувача</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>recipientIp</td><td><code class="expression">space.vars.recipientIP_desctiption</code></td><td>string (50)</td><td>Ні</td><td><code class="expression">space.vars.recipientIP_example</code></td></tr><tr><td>recipientPhone</td><td>номер телефону отримувача</td><td>string (50)</td><td>Ні</td><td>380630000000</td></tr><tr><td>recipientBirthday</td><td>день народження отримувача</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>recipientGender</td><td>Гендер отримувача</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>recipientZipCode</td><td>індекс отримувача</td><td>string (50)</td><td>Ні</td><td>49000</td></tr></tbody></table>

**Вихідні параметри**

| Параметр                   | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| -------------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                       | тип транзакції                                                           | string       | CARD\_2\_ACCOUNT                                                                                                                                                                                       |
| rrn                        | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                    | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                    | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount                 | сума платежу в копійках                                                  | int          | 2000                                                                                                                                                                                                   |
| merchantId                 | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId                | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId            | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName               | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode               | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                     | статус транзакціі                                                        | string       | SUСCESS FAIL PENDING REQUIRED\_3DS DESIRED\_THREEDS\_MODE\_ERROR                                                                                                                                       |
| transactionType            | тип транзакції у цифровому значенні                                      | string       | 62                                                                                                                                                                                                     |
| merchantRequestId          | Id запиту мерчанта                                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency        | валюта платежу                                                           | string       | 980                                                                                                                                                                                                    |
| merchantCommission         | сума комісії                                                             | string       | 2                                                                                                                                                                                                      |
| createDateTime             | дата створення платежу                                                   | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime       | дата модифікаціі платежу                                                 | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode                 | код відповіді                                                            | string       | 0                                                                                                                                                                                                      |
| responseCode               | деталі відповіді                                                         | string       | 0                                                                                                                                                                                                      |
| description                | опис відповіді                                                           | string       | approved                                                                                                                                                                                               |
| bankCode                   | назва банку емітента                                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem              | назва мпс емітента                                                       | string       | MasterCard                                                                                                                                                                                             |
| productType                | тип продукту термінала                                                   | string       | C2A                                                                                                                                                                                                    |
| notificationUrl            | url, на який відправлено CallBack                                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType         | тип оплати                                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption     | ознака криптування данних CallBack                                       | string       | true/false Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані                                                                                                     |
| cardNumberMask             | маскований номер карти                                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode         | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.     | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode                | параметр який вказує, використовувася 3DS у покупці чи ні                | string       | MUST- проводимо оплату з 3DS MUST\_NOT- проводимо оплату без 3DS                                                                                                                                       |
| statusThreeDs              | статус проведення 3DS                                                    | string       | Y - успіший 3ds N - не успішний 3ds                                                                                                                                                                    |
| threeDSServerTransId       | Id транзакціі в системі 3ds                                              | string       | b6c35fdb-28c1-454d-a2f3-51098c26bda4                                                                                                                                                                   |
| acsTransId                 | Id транзакціі в системі ACS                                              | string       | 3e17fabb-71e6-498e-8794-ef8c95c5ba6f                                                                                                                                                                   |
| dsTransId                  | Id транзакціі згенерований Directory Server                              | string       | 12ebc556-82d3-4e35-9fb8-77ac18b050ea                                                                                                                                                                   |
| eci                        | Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції | string       | 02                                                                                                                                                                                                     |
| processingMerchantId       | Id мерчанту в ПЦ                                                         | string       | AE100000                                                                                                                                                                                               |
| processingMerchantId       | Id терміналу в ПЦ                                                        | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl             | url для редиректа клієнта на сторінку емітента для проходження 3DS       | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                    | під тип транзакціі                                                       | enum         | Можливі значення: NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається                                                                                          |
| senderCustomerId           | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName            | ім'я відправника                                                         | string       | Іваненко                                                                                                                                                                                               |
| senderLastName             | прізвище відправника                                                     | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName           | по-батькові відправника                                                  | string       | Іванович                                                                                                                                                                                               |
| senderEmail                | пошта відправника                                                        | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| senderCountry              | країна відправника                                                       | string       | Україна                                                                                                                                                                                                |
| senderRegion               | область відправника                                                      | string       | Київська                                                                                                                                                                                               |
| senderCity                 | місто відправника                                                        | string       | Київ                                                                                                                                                                                                   |
| senderStreet               | вулиця відправника                                                       | string       | Січових стрільців                                                                                                                                                                                      |
| senderAdditionalAddress    | додаткові дані адреси відправника (поверх, номер дому, квартира)         | string       | 23                                                                                                                                                                                                     |
| senderItn                  | іпн відправника                                                          | string       | 123456789                                                                                                                                                                                              |
| senderPassport             | паспорт відправника                                                      | string       | АН123456                                                                                                                                                                                               |
| senderIp                   | <code class="expression">space.vars.senderIP_description</code>          | string       | <code class="expression">space.vars.senderIP_example</code>                                                                                                                                            |
| senderPhone                | номер телефону відправника                                               | string       | 380630000000                                                                                                                                                                                           |
| senderBirthday             | день народження відправника                                              | string       | 31.12.2000                                                                                                                                                                                             |
| senderGender               | гендер відправника                                                       | string       | M                                                                                                                                                                                                      |
| senderZipCode              | індекс відправника                                                       | string       | 12000                                                                                                                                                                                                  |
| senderBankCode             | назва банку емітента відправника                                         | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| senderPaymentSystem        | назва мпс емітента відправника                                           | string       | MasterCard                                                                                                                                                                                             |
| senderCardNumberMask       | маскований номер карти відправника                                       | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| recipientCustomerId        | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| recipientFirstName         | ім'я отримувача                                                          | string       | Іваненко                                                                                                                                                                                               |
| recipientLastName          | прізвище отримувача                                                      | string       | Іван                                                                                                                                                                                                   |
| recipientMiddleName        | по-батькові отримувача                                                   | string       | Іванович                                                                                                                                                                                               |
| recipientEmail             | пошта отримувача                                                         | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| recipientCountry           | країна отримувача                                                        | string       | Україна                                                                                                                                                                                                |
| recipientRegion            | область отримувача                                                       | string       | Київська                                                                                                                                                                                               |
| recipientCity              | місто отримувача                                                         | string       | Київ                                                                                                                                                                                                   |
| recipientStreet            | вулиця отримувача                                                        | string       | Січових стрільців                                                                                                                                                                                      |
| recipientAdditionalAddress | додаткові дані адреси отримувача (поверх, номер дому, квартира)          | string       | 23                                                                                                                                                                                                     |
| recipientItn               | іпн отримувача                                                           | string       | 123456789                                                                                                                                                                                              |
| recipientPassport          | паспорт отримувача                                                       | string       | АН123456                                                                                                                                                                                               |
| recipientIp                | <code class="expression">space.vars.recipientIP_desctiption</code>       | string       | <code class="expression">space.vars.recipientIP_example</code>                                                                                                                                         |
| recipientPhone             | номер телефону отримувача                                                | string       | 380630000000                                                                                                                                                                                           |
| recipientBirthday          | день народження отримувача                                               | string       | 31.12.2000                                                                                                                                                                                             |
| recipientGender            | гендер отримувача                                                        | string       | M                                                                                                                                                                                                      |
| recipientZipCode           | індекс отримувача                                                        | string       | 12000                                                                                                                                                                                                  |
| recipientBankCode          | назва банку емітента отримувача                                          | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| recipientPaymentSystem     | назва мпс емітента отримувача                                            | string       | MasterCard                                                                                                                                                                                             |
| recipientCardNumberMask    | маскований номер карти отримувача                                        | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |

**Приклад об’єкту paymentData**

```json
{
"applicationPrimaryAccountNumber":"{{applePayCardNumber}}",
"applicationExpirationDate":"{{applePayDate}}",
"currencyCode":"980",
"transactionAmount":"100",
"cardholderName":"{{cardholderName}}",
"deviceManufacturerIdentifier":"1255548888hfhhbbk",
"paymentDataType":"3DSecure",
"paymentData":{
"onlinePaymentCryptogram":"AVn0rK8BiDxN2D/w2j8LMAABAAA=",
"eciIndicator":"7"}
}
```

**Приклад тіла запиту**

```json
{
    "paymentData": "{{encryptedPaymentData}}", 
    "merchantRequestId": "{{requestUUIDT}}",
    "desiredThreeDSMode": "MUST_NOT",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "resultRedirectUrl": "",
    "purpose": "purpose",
    "comment": "comment",
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
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

**Приклад тіла відповіді без 3DS**

```json
{
    "type": "CARD_2_ACCOUNT",
    "rrn": "410209187456",
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712826505345NY4bmiIDrE5",
    "ecomOperationId": "21931655-17db-44e3-bd2f-212cbf5069c9",
    "merchantName": null,
    "approvalCode": null,
    "status": "SUCCESS",
    "transactionType": 62,
    "merchantRequestId": "586fc1f5-f647-4800-94e1-a9e65a68d424",
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
    "productType": "C2A",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": "APPLE_PAY",
    "notificationEncryption": false,
    "senderCardNumberMask": null,
    "desiredThreeDSMode": "MUST_NOT",
    "threeDSMode": "MUST_NOT",
    "statusThreeDs": null,
    "threeDSServerTransId": null,
    "redirect3dsUrl": null,
    "recipientAccount": null,
    "senderCustomerId": null,
    "senderFirstName": "FirstName",
    "senderLastName": "Name",
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": "Ukraine",
    "senderRegion": null,
    "senderCity": "City",
    "senderStreet": "Str.",
    "senderAdditionalAddress": null,
    "senderItn": null,
    "senderPassport": null,
    "senderIp": null,
    "senderPhone": null,
    "senderBirthday": null,
    "senderGender": null,
    "senderZipCode": null,
    "senderBankCode": null,
    "senderPaymentSystem": null,
    "recipientCustomerId": null,
    "recipientFirstName": null,
    "recipientLastName": null,
    "recipientMiddleName": null,
    "recipientEmail": null,
    "recipientCountry": null,
    "recipientRegion": null,
    "recipientCity": null,
    "recipientStreet": null,
    "recipientAdditionalAddress": null,
    "recipientItn": null,
    "recipientPassport": null,
    "recipientIp": null,
    "recipientPhone": null,
    "recipientBirthday": null,
    "recipientGender": null,
    "recipientZipCode": null
}
```

**Приклад тіла відповіді з 3DS**

```json
{
    "type": "CARD_2_ACCOUNT",
    "rrn": null,
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712826655741bHtPOJY9BvI",
    "ecomOperationId": "92f0ccdd-48fb-43d8-9ee4-f4bd2e295f86",
    "merchantName": null,
    "approvalCode": null,
    "status": "REQUIRED_3DS",
    "transactionType": 62,
    "merchantRequestId": "45f336e8-f58d-43d5-9cdd-c3a06ba794c5",
    "transactionCurrency": "980",
    "merchantCommission": null,
    "createDateTime": "2024.09.19 15:29:25.675",
    "modificationDateTime": "2024.09.19 15:29:25.675",
    "transactionResponseInfo": {
        "actionCode": null,
        "responseCode": null,
        "description": null
    },
    "bankCode": null,
    "paymentSystem": null,
    "productType": "C2A",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": "APPLE_PAY",
    "notificationEncryption": false,
    "senderCardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "a011f12f-ddfa-4629-b786-4aa427f7210f",
    "redirect3dsUrl": null,
    "recipientAccount": null,
    "senderCustomerId": null,
    "senderFirstName": "FirstName",
    "senderLastName": "Name",
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": "Ukraine",
    "senderRegion": null,
    "senderCity": "City",
    "senderStreet": "Str.",
    "senderAdditionalAddress": null,
    "senderItn": null,
    "senderPassport": null,
    "senderIp": null,
    "senderPhone": null,
    "senderBirthday": null,
    "senderGender": null,
    "senderZipCode": null,
    "senderBankCode": null,
    "senderPaymentSystem": null,
    "recipientCustomerId": null,
    "recipientFirstName": null,
    "recipientLastName": null,
    "recipientMiddleName": null,
    "recipientEmail": null,
    "recipientCountry": null,
    "recipientRegion": null,
    "recipientCity": null,
    "recipientStreet": null,
    "recipientAdditionalAddress": null,
    "recipientItn": null,
    "recipientPassport": null,
    "recipientIp": null,
    "recipientPhone": null,
    "recipientBirthday": null,
    "recipientGender": null,
    "recipientZipCode": null
}
```
