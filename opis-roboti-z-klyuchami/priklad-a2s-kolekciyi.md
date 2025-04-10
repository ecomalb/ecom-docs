# Приклад А2С колекції

1\. Authorize by virtual device  —`{{url}}/api-gateway/authorize_virtual_device` \
Для запиту потрібен serviceCode, котрий ми передаємо Вам перед інтеграцією на проді.\
У відповідь повернеться зашифрований серверний ключ - serverPublicKey у форматі jwe, котрий буде потрібен для виконання кроку 2. \
На тесті, він вже присутній в даних колекції.

2\. Decrypt auth response — `{{url}}/cipher/decrypt_by_jwk?message={{responseJwe}}`\
Запит декриптує відповідь банку на своїй стороні за допомогою приватного ключа - userPrivateKey (котрий Мерчант генерує за інтрукцією [Процес генерації комунікаційних JWK ключів клієнта](https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta) ) , щоб отримати серверний ключ - serverPublicKey у відкритому вигляді, котрий буде потрібен для виконання крок 4.\
На Продакшн середовищі, Мерчант самостійно повинен виконувати декриптування на своїй стороні.

3\. A2C card number encrypt — `{{url}}/cipher/encrypt_by_jwk?message={{card_number}}`\
За допомогою платіжного ключа - paymentPublicKey, котрий Банк надає Мерчанту, відбувається криптування номеру картки клієнта.\
Для тестування можна скористатися допоміжним методом "/ecom/help/encrypt\_by\_jwk". \
На Продакшн середовищі, Мерчант самостійно повинен виконувати криптування на своїй стороні.

4\. A2C encrypt body — `{{url}}/cipher/encrypt_by_jwk?message={{body_request}}`\
\{{body\_request\}} - повинно відповідати обов'язковим вхідним параметрам [A2C](https://docs.merchant.alb.ua/platizhni-metodi-h2h/a2c)\
За допомогою серверного ключа - serverPublicKey, котрий отриманий на кроках 1 і 2, відбувається криптування тіла запиту на проведення платежу на стороні Мерчанта.\
У відповіді отримуємо зашифроване тіло запиту - \{{encryptJweT\}}, котре буде потрібне для виконання кроку 5.\
Для тестів допускається використання допоміжного методу "/ecom/help/encrypt\_ru\_jwk"

5\. A2C v3 — `{{url}}/ecom/execute_request/payments/v3/account_to_card`\
Запит відправляє зашифроване тіло - \{{encryptJweT\}}, згенероване на кроці 4. \
У відповіді отримуємо зашифровану відповідь - \{{responseJwe\}}, котра буде потрібна для виконання кроку 6.

6\. A2C v3 decrypt result — `{{url}}/cipher/decrypt_by_jwk?message={{responseJwe}}`\
Запит декриптує відповідь від банку за допомогою приватного ключа - userPrivateKey, (котрий Мерчант генерує за інструкцією [Процес генерації комунікаційних JWK ключів клієнта](https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta)).\
У відповідь отримуємо розшифровану тіло відповіді на запит у кроці 5.&#x20;
