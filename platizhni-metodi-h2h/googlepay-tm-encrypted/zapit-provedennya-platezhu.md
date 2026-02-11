---
description: '{{url}}/ecom/execute_request/payments/v1/google_pay/token/purchase'
---

# Запит проведення платежу

**Вхідні параметри:**

<table><thead><tr><th>Параметр</th><th>Опис</th><th width="274">Формат даних</th><th width="59">Обов'язковість</th><th>Приклад</th></tr></thead><tbody><tr><td>googlePayPaymentData</td><td> Основний об'єкт із даними платежу Google Pay</td><td>JSON-об'єкт </td><td> Так</td><td>{ ... } </td></tr><tr><td>apiVersion</td><td>Версія Google Pay API</td><td>int</td><td>Так</td><td>2</td></tr><tr><td>apiVersionMinor</td><td>Мінорна версія API</td><td>int</td><td>Так</td><td>0</td></tr><tr><td>paymentMethodData</td><td>Інформація про платіжний метод</td><td>JSON-об'єкт</td><td>Так</td><td>{ ... } </td></tr><tr><td>description</td><td>Опис платіжного методу</td><td>string</td><td>Так</td><td>"Mastercard •••• 9079"</td></tr><tr><td>info</td><td>Додаткові деталі про карту</td><td>JSON-об'єкт</td><td>Так</td><td>{ ... } </td></tr><tr><td>assuranceDetails</td><td>Дані про верифікацію карти</td><td>JSON-об'єкт</td><td>Так</td><td>{ ... } </td></tr><tr><td>accountVerified</td><td>Чи верифіковано акаунт</td><td>boolean</td><td>Так</td><td>true</td></tr><tr><td>cardHolderAuthenticated</td><td>Чи аутентифіковано власника картки</td><td>boolean</td><td>Так</td><td>false</td></tr><tr><td>cardDetails</td><td>Останні чотири цифри картки</td><td>string</td><td>Так</td><td>"9079"</td></tr><tr><td>cardNetwork</td><td>Платіжна система картки</td><td>string</td><td>Так</td><td>"MASTERCARD"</td></tr><tr><td>tokenizationData</td><td>Дані про токенізацію</td><td>JSON-об'єкт</td><td>Так</td><td>{ ... } </td></tr><tr><td>token</td><td>Токен платежу</td><td> string</td><td> Так</td><td> "{...}"</td></tr><tr><td>type</td><td>Тип токенізації (наприклад, платіжний шлюз)</td><td>string</td><td>Так</td><td>"PAYMENT_GATEWAY"</td></tr><tr><td>merchantInfo</td><td>Інформація про продавця</td><td>JSON-об'єкт</td><td>Так</td><td>{ ... } </td></tr><tr><td>merchantId</td><td>Ідентифікатор продавця</td><td>string</td><td>Так</td><td>"1234567890"</td></tr><tr><td>gateway</td><td>Назва платіжного шлюзу</td><td>string</td><td>Так</td><td>"timeproject"</td></tr><tr><td>environment</td><td>Середовище для тестування або продакшн</td><td>string</td><td>Так</td><td>"TEST"</td></tr><tr><td>merchantRequestId</td><td>унікальний ідентифікатор згенерований системою мерчанта, використовується для можливості дізнатися статус операції якщо запит закінчився невідомою помилкою чи дісконектом</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>merchantId</td><td>Id мерчанту згенерований в Єкомі</td><td>string(36)</td><td>Так</td><td>137d9304-0368-11ed-b939-0242ac120002</td></tr><tr><td>transactionAmount</td><td>Сума платежу в копійках</td><td>string</td><td>Так</td><td>2000</td></tr><tr><td>desiredThreeDSMode</td><td>Ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.</td><td>string (50)</td><td>Так</td><td>За замовчуванням SHOULD</td></tr><tr><td>resultRedirectUrl</td><td>Url для редиректа клієнта після проходження 3DS аутентифікації</td><td>string (1000)</td><td>Ні</td><td><a href="https://support.google.com/"><img src="https://support.google.com/favicon.ico" alt="">Google Help</a></td></tr><tr><td>notificationUrl</td><td>url, на який буде відправлено CallBack</td><td>string (1000)</td><td>Ні</td><td><a href="https://merchant.notification_url/">https://merchant.notification_url</a></td></tr><tr><td>notificationEncryption</td><td>ознака криптування данних CallBack</td><td>string</td><td>Ні</td><td><p>true/false</p><p>Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані</p></td></tr><tr><td>date</td><td>дата та час платежу</td><td>string</td><td>Так</td><td>{{currentdateT}}.00+03:00</td></tr><tr><td>comment</td><td>додаткова опис операції яку заповнює клієнт мерчанта</td><td>string (1000)</td><td>Ні</td><td>///5555.25412</td></tr><tr><td>purpose</td><td>призначення платежу яке заповнює мерчант</td><td>string (255)</td><td>Ні</td><td>За товар</td></tr><tr><td>merchantComment</td><td>додаткова інформація\коментар мерчанта по замовленню</td><td><p>string(255) </p><p>a-zA-Z0-9 ,.;:@#$%'-=+1,256$</p></td><td>Ні</td><td>merchant Comment id 1258728c1</td></tr><tr><td>customerData</td><td>об'єкт з customer даними</td><td>object</td><td>Так</td><td></td></tr><tr><td>senderCustomerId</td><td>Id клієнта відправника</td><td>string (255)</td><td>Так</td><td>1258728c1</td></tr><tr><td>senderFirstName</td><td>ім'я відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іваненко</td></tr><tr><td>senderLastName</td><td>прізвище відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іван</td></tr><tr><td>senderMiddleName</td><td>по-батькові відправника</td><td><p>string (30)</p><ul><li>значення не може містити виключно цифри</li><li>не може містити крапки та інші спецсимволи</li><li>дозволено приймати тільки літерно-цифрові значення</li><li>може приймати пробіл та дефіс, але НЕ може складатися виключно з “ “ или “-“</li><li>дефіс чи пробіл може бути всередині, але не може бути на початку чи кінці</li><li>Для символу апострофу використовуйте єдиний доступний символ utf8 - '<br>який в:<br>utf 16 - u0027<br>utf32 - 00000027</li></ul></td><td>Ні</td><td>Іванович</td></tr><tr><td>senderEmail</td><td>пошта відправника</td><td>string (256)</td><td>Ні</td><td><a href="mailto:mail@gmail.com">mail@gmail.com</a></td></tr><tr><td>senderСountry</td><td>країна відправника</td><td>string (3) ISO 3166, 804 (Ukraine)</td><td>Ні</td><td>804</td></tr><tr><td>senderRegion</td><td>область відправника</td><td>string (255)</td><td>Ні</td><td>Київська</td></tr><tr><td>senderСity</td><td>місто відправника</td><td>string (25)</td><td>Ні</td><td>Київ</td></tr><tr><td>senderStreet</td><td>вулиця відправника</td><td>string (35)</td><td>Ні</td><td>Січових стрільців</td></tr><tr><td>senderAdditionalAddress</td><td>додаткові дані адреси відправника (поверх, номер дому, квартира)</td><td>string (255)</td><td>Ні</td><td>23</td></tr><tr><td>senderItn</td><td>іпн відправника</td><td>string (20)</td><td>Ні</td><td>123456789</td></tr><tr><td>senderPassport</td><td>паспорт відправника</td><td>string (255)</td><td>Ні</td><td>АН123456</td></tr><tr><td>senderIp</td><td><code class="expression">space.vars.senderIP_description</code></td><td>string (50)</td><td>Ні</td><td><code class="expression">space.vars.senderIP_example</code></td></tr><tr><td>senderPhone</td><td>номер телефону відправника</td><td>string (20)</td><td>Ні</td><td>380630000000</td></tr><tr><td>senderBirthday</td><td>день народження відправника</td><td>string (50)</td><td>Ні</td><td>31.12.2000</td></tr><tr><td>senderGender</td><td>Гендер відправника</td><td>string (50)</td><td>Ні</td><td>Male/Female</td></tr><tr><td>senderZipCode</td><td>індекс відправника</td><td>string (50)</td><td>Ні</td><td>49000</td></tr></tbody></table>

**Вихідні параметри**

| Параметр                | Опис                                                                     | Формат даних | Приклад                                                                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| type                    | тип транзакції                                                           | string       | Purchase                                                                                                                                                                                               |
| rrn                     | rrn номер транзакції в МПС                                               | string       | 2554256963                                                                                                                                                                                             |
| purpose                 | призначення платежу                                                      | string       | За товар                                                                                                                                                                                               |
| comment                 | коментар                                                                 | string       | тест                                                                                                                                                                                                   |
| coinAmount              | сума платежу                                                             | int          | 2000                                                                                                                                                                                                   |
| merchantId              | Id мерчанту                                                              | string       | 137d9304-0368-11ed-b939-0242ac120002                                                                                                                                                                   |
| operationId             | Id транзакціі                                                            | string       | 1712844596346b9F-WwrWZpq                                                                                                                                                                               |
| ecomOperationId         | Id транзакціі в системі Ecom                                             | string       | 8c3303e9-7396-43b8-af4e-31d9facdde9b                                                                                                                                                                   |
| merchantName            | найменування торговця                                                    | string       | KB test terminal                                                                                                                                                                                       |
| approvalCode            | код авторизаціі                                                          | string       | 39203                                                                                                                                                                                                  |
| status                  | статус транзакціі                                                        | string       | SUСCESS FAIL PENDING REQUIRED\_3DS DESIRED\_THREEDS\_MODE\_ERROR                                                                                                                                       |
| transactionType         | тип транзакції у цифровому значенні                                      | string       | 35                                                                                                                                                                                                     |
| merchantRequestId       | Id запиту мерчанта                                                       | string       | 72837906-f526-4aef-8d11-58d80b44cb75                                                                                                                                                                   |
| transactionCurrency     | валюта платежу                                                           | string       | 980                                                                                                                                                                                                    |
| merchantCommission      | сума комісії                                                             | string       | 2                                                                                                                                                                                                      |
| createDateTime          | дата створення платежу                                                   | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| modificationDateTime    | дата модифікаціі платежу                                                 | string       | 2024.09.19 15:29:25.675                                                                                                                                                                                |
| actionCode              | код відповіді                                                            | string       | 0                                                                                                                                                                                                      |
| responseCode            | деталі відповіді                                                         | string       | 0                                                                                                                                                                                                      |
| description             | опис відповіді                                                           | string       | approved                                                                                                                                                                                               |
| bankCode                | назва банку емітента                                                     | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| paymentSystem           | назва мпс емітента                                                       | string       | MasterCard                                                                                                                                                                                             |
| productType             | тип продукту термінала                                                   | string       | PURCHASE                                                                                                                                                                                               |
| notificationUrl         | url, на який відправлено CallBack                                        | string       | [https://merchant.notification\_url/](https://merchant.notification_url/)                                                                                                                              |
| paymentServiceType      | тип оплати                                                               | string       | CARD/APPLE\_PAY/GOOGLE\_PAY                                                                                                                                                                            |
| notificationEncryption  | ознака криптування данних CallBack                                       | string       | true/false Якщо параметр не передано або передано false, то дані в CallBack будуть не закриптовані                                                                                                     |
| cardNumberMask          | маскований номер карти                                                   | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |
| desiredThreeDSMode      | ознака яка вказує, чи бажає мерчант використати 3DS в покупці чи ні.     | string       | MUST/SHOULD/MUST\_NOT                                                                                                                                                                                  |
| threeDSMode             | параметр який вказує, використовувася 3DS у покупці чи ні                | string       | MUST- проводимо оплату з 3DS MUST\_NOT- проводимо оплату без 3DS                                                                                                                                       |
| statusThreeDs           | статус проведення 3DS                                                    | string       | Y - успіший 3ds N - не успішний 3ds                                                                                                                                                                    |
| threeDSServerTransId    | Id транзакціі в системі 3ds                                              | string       | b6c35fdb-28c1-454d-a2f3-51098c26bda4                                                                                                                                                                   |
| acsTransId              | Id транзакціі в системі ACS                                              | string       | 3e17fabb-71e6-498e-8794-ef8c95c5ba6f                                                                                                                                                                   |
| dsTransId               | Id транзакціі в системі ACS                                              | string       | 12ebc556-82d3-4e35-9fb8-77ac18b050ea                                                                                                                                                                   |
| eci                     | Electronic Commerce Indicator Код, який вказує рівень безпеки транзакції | string       | 02                                                                                                                                                                                                     |
| processingMerchantId    | Id мерчанту в ПЦ                                                         | string       | AE100000                                                                                                                                                                                               |
| processingTerminalId    | Id терміналу в ПЦ                                                        | string       | AE100000                                                                                                                                                                                               |
| redirect3dsUrl          | url для редиректа клієнта на сторінку емітента для проходження 3DS       | string       | [https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA](https://api-ecom-release.develop.bankalliance.ua/threeDS/getRedirectHtml/1702047427621BHu5X99yDbA) |
| txnType                 | під тип транзакціі                                                       | enum         | Можливі значення: NONCVV/noncvv- при отриманні даного значення введення cvv та його перевірка не відбувається                                                                                          |
| senderCustomerId        | Id клієнта відправника                                                   | string       | 1258728c1                                                                                                                                                                                              |
| senderFirstName         | ім'я відправника                                                         | string       | Іваненко                                                                                                                                                                                               |
| senderLastName          | прізвище відправника                                                     | string       | Іван                                                                                                                                                                                                   |
| senderMiddleName        | по-батькові відправника                                                  | string       | Іванович                                                                                                                                                                                               |
| senderEmail             | пошта відправника                                                        | string       | [mail@gmail.com](mailto:mail@gmail.com)                                                                                                                                                                |
| senderCountry           | країна відправника                                                       | string       | Україна                                                                                                                                                                                                |
| senderRegion            | область відправника                                                      | string       | Київська                                                                                                                                                                                               |
| senderCity              | місто відправника                                                        | string       | Київ                                                                                                                                                                                                   |
| senderStreet            | вулиця відправника                                                       | string       | Січових стрільців                                                                                                                                                                                      |
| senderAdditionalAddress | додаткові дані адреси відправника (поверх, номер дому, квартира)         | string       | 23                                                                                                                                                                                                     |
| senderItn               | іпн відправника                                                          | string       | 123456789                                                                                                                                                                                              |
| senderPassport          | паспорт відправника                                                      | string       | АН123456                                                                                                                                                                                               |
| senderIp                | <code class="expression">space.vars.senderIP_description</code>          | string       | <code class="expression">space.vars.senderIP_example</code>                                                                                                                                            |
| senderPhone             | номер телефону відправника                                               | string       | 380630000000                                                                                                                                                                                           |
| senderBirthday          | день народження відправника                                              | string       | 31.12.2000                                                                                                                                                                                             |
| senderGender            | гендер відправника                                                       | string       | M                                                                                                                                                                                                      |
| senderZipCode           | індекс відправника                                                       | string       | 12000                                                                                                                                                                                                  |
| senderBankCode          | назва банку емітента відправника                                         | string       | BANK\_ALLIANCE                                                                                                                                                                                         |
| senderPaymentSystem     | назва мпс емітента відправника                                           | string       | MasterCard                                                                                                                                                                                             |
| senderCardNumberMask    | маскований номер карти відправника                                       | string       | 5573\*\*\*\*\*\*\*\*0304                                                                                                                                                                               |

**Приклад тіла запиту**

```json
{
    "googlePayPaymentData": {
        "apiVersion": 2,
        "apiVersionMinor": 0,
        "paymentMethodData": {
            "description": "Mastercard •••• 9079",
            "info": {
                "assuranceDetails": {
                    "accountVerified": true,
                    "cardHolderAuthenticated": false
                },
                "cardDetails": "9079",
                "cardNetwork": "MASTERCARD"
            },
            "tokenizationData": {
                "token": "{\"signature\":\"MEUCIQDaNH5qORDmyWCADBPPQdx0WLGzqP4l9gznr1P0C92JQIgcCC5sGVaHKcopWwx9qMQ+nJswxyk5LugcQng8cUQKPs\\u003d\",\"intermediateSigningKey\":{\"signedKey\":\"{\\\"keyValue\\\":\\\"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAE/uMFvqw3uWfiJfev8mveNhiQcRSVSzqynD1jo/WAKA1iXtyyoty/uzQBbRhFmnwRxRWJvSJiVe8Q3aMEePajgA\\\\u003d\\\\u003d\\\",\\\"keyExpiration\\\":\\\"1732261522591\\\"}\",\"signatures\":[\"MEUCIEr2AORUfr3tThPtgNAmtXX3kMXlxqQE5HfzFf/qCt5FAiEArM2taQdIa+t2ug2GxaXo7so9CcVSAXe5vfo/AATvHuU\\u003d\"]},\"protocolVersion\":\"ECv2\",\"signedMessage\":\"{\\\"encryptedMessage\\\":\\\"jOTMB2WrbkP7mV2PzNrz8TDM0vgoyfLfL5MoqkfyzNP1bSr5agnuxaTOH6zdUVNcqM1tI45H8/vZvMA7Atqk05iUteWMbMS8jcHdwbOXqXdHAmK2keUBJ1+WltKDfdcldTqRCVUbkb2zEOPS9O7x97EKshGcdOFMgy3rWkSDHOGYI2iU4fcu780LkZ2S9qOiQxugF77HyWF+R6eY6YONMftw1dbyLlifz1NQkRqiVuWZfY1haBFS54P23PTPg/z8LEndY/34DoHSPbErxtaweu5mzZmFhCvaNSurjdUQSG9ZnrRFS4sBsMDkdnKgtuDl/Dp8DWoKDGQ5N1KQHK6I429r5HQzGvZI/mpLGXjLS/IqKPYail0xFbQt/sKKJWslMuzgtPLdwOGJOaC3EiS9ASy7Xwjfsy8kmZiCMH0J6XFbDQPW1nYupMkCNmQbmV0xUhkPX1meGmJ/gGYw+r/c6NtQfBoU+pfaQUOuMPU5swdlArtCdfKve0NkPTgvXErz6sLwB/WTv1iWknescQC2skne7d3KUE5dQsUIKWDtlbStAZwHfRC9SrhqA9OF8Q\\\\u003d\\\\u003d\\\",\\\"ephemeralPublicKey\\\":\\\"BCWiEFk24pBKXyporPbi4AAqbKJNa9kV1XDAwJHxCkyDFwZaGKzdpgFfuOVXgZTOREohQXSowPvp+7Cf9Zq9xTI\\\\u003d\\\",\\\"tag\\\":\\\"7aO3dd8BrbM0xYGd8rlAdOEeUiT+vXYxCXedIM9nw/w\\\\u003d\\\"}\"}",
                "type": "PAYMENT_GATEWAY"
            },
            "type": "CARD"
        },
        "merchantInfo": {
            "merchantId": "1234567890",
            "gateway": "timeproject"
        }
    },
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "environment": "TEST",
    "resultRedirectUrl": "137d9304-0368-11ed-b939-0242ac120002",
    "notificationEncryption": false,
    "notificationUrl": "https://eocfzhqbfuebmke.m.pipedream.net",
    "merchantRequestId": "1df6672b-d198-469d-88ce-6dab74d7feb2",
    "coinAmount": 1000,
    "customerData": {
        "senderCustomerId": "34234234",
        "senderCountry": "234"
    },
    "comment": "comment",
    "purpose": "purpose",
    "desiredThreeDSMode": "MUST_NOT",
    "date": "2024-11-15 14:13:50.00+03:00",
    "merchantComment": "resultRedirectUrl",
    "browserInfo": {
        "browserAcceptHeader": "text/html,application/xhtmlxml,application/xml;q=0.9,image/avif,imagewebp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
        "browserUserAgent": "Mozilla/5.0(WindowsNT10.0;Win64;x64)AppleWebKit/537.36(KHTML,like,Gecko)Chrome/87.0.4280.66Safari/537.36",
        "browserLanguage": "en-US,en",
        "browserColorDepth": "24",
        "browserScreenHeight": "800",
        "browserScreenWidth": "1280",
        "browserTZ": "-180"
    }
}
```

**Приклад тіла відповіді без 3DS**

```json
{
    "type": "PURCHASE",
    "rrn": "410211187850",
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "1712836451574mxQBagrb76l",
    "ecomOperationId": "7fb11c16-918d-4bfb-83aa-00e7a8576f9c",
    "merchantName": null,
    "approvalCode": null,
    "status": "SUCCESS",
    "transactionType": 35,
    "merchantRequestId": "9a89759c-f500-461f-a0c7-69a5b678b89d",
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
    "productType": "PURCHASE",
    "notificationUrl": "https://api-ecom-prod.bankalliance.ua/mock",
    "paymentServiceType": "GOOGLE_PAY",
    "notificationEncryption": false,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST_NOT",
    "threeDSMode": "MUST_NOT",
    "statusThreeDs": null,
    "threeDSServerTransId": null,
    "redirect3dsUrl": null,
    "txnType": "null",
    "senderCustomerId": null,
    "senderFirstName": null,
    "senderLastName": null,
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": null,
    "senderRegion": null,
    "senderCity": null,
    "senderStreet": null,
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
    "senderCardNumberMask": null
}
```

**Приклад тіла відповіді з 3DS**

```json
{
    "type": "PURCHASE",
    "rrn": null,
    "purpose": "purpose",
    "comment": "comment",
    "coinAmount": null,
    "merchantId": "137d9304-0368-11ed-b939-0242ac120002",
    "operationId": "17128429092802o9koN8eABn",
    "ecomOperationId": "99261a33-cfae-4dfa-9396-812817b5dffb",
    "merchantName": null,
    "approvalCode": null,
    "status": "REQUIRED_3DS",
    "transactionType": 35,
    "merchantRequestId": "8bf3bc51-53e8-4d12-9e86-c13dd6af3b9e",
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
    "productType": "PURCHASE",
    "notificationUrl": "https://webhook.site/cbf8c83a-ee1e-47c6-899c-eca5731ff084",
    "paymentServiceType": "GOOGLE_PAY",
    "notificationEncryption": false,
    "cardNumberMask": null,
    "desiredThreeDSMode": "MUST",
    "threeDSMode": "MUST",
    "statusThreeDs": null,
    "threeDSServerTransId": "5d175446-df26-4ad0-a60c-cd8f95570c0c",
    "redirect3dsUrl": null,
    "txnType": "null",
    "senderCustomerId": null,
    "senderFirstName": null,
    "senderLastName": null,
    "senderMiddleName": null,
    "senderEmail": null,
    "senderCountry": null,
    "senderRegion": null,
    "senderCity": null,
    "senderStreet": null,
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
    "senderCardNumberMask": null
}
```
