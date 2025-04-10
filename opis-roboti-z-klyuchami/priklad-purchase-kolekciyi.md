# Приклад PURCHASE колекції

1\. Authorize by virtual device — `{{url}}/api-gateway/authorize_virtual_device`\
Для запиту потрібен serviceCode, котрий ми передаємо Вам перед інтеграцією на проді. \
У відповідь повернеться зашифрований серверний ключ - serverPublicKey у форматі jwe, котрий буде потрібен для виконання кроку  2.&#x20;

2\. Decrypt auth response — `{{url}}/cipher/decrypt_by_jwk?message={{responseJwe}}`\
Запит декриптує відповідь банку на своїй стороні за допомогою приватного ключа - userPrivateKey (котрий Мерчант генерує за інструкцією [Процес генерації комунікаційних JWK ключів клієнта](https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta) ) , щоб отримати серверний ключ - serverPublicKey у відкритому вигляді, котрий буде потрібен для виконання кроків 5 та 8. \
На Продакшн середовищі, Мерчант самостійно повинен виконувати декриптування на своїй стороні.

3\. Encrypt card number —  `{{url}}/cipher/encrypt_by_jwk?message={{card_number}}`\
За допомогою платіжного ключа - paymentPublicKey, котрий Банк надає Мерчанту, відбувається криптування номеру картки клієнта.\
Для тестування можна скористатися допоміжним методом "/ecom/help/encrypt\_by\_jwk". \
На Продакшн середовищі, Мерчант самостійно повинен виконувати криптування на своїй стороні.

4\. Ecnrypt Date and Security cvv — `{{url}}/cipher/encrypt_by_jwk?message={{year_month_day}}`\
За допомогою платіжного ключа - paymentPublicKey, котрий Банк надає Мерчанту, виконується криптування терміну дії та cvvа. Передається у форматі: рік, місяць, cvva - "2603123"\
Для тестування можна скористатися допоміжним методом  "/ecom/help/encrypt\_ru\_jwk". \
На Продакшн середовищі, Мерчант самостійно повинен виконувати криптування на своїй стороні.

5\. Encrypt create purchase request body — `{{url}}/cipher/encrypt_by_jwk?message={{body_request}}`\
\{{body\_request\}} - повинно відповідати обов'язковим вхідним параметрам [PURCHASE](https://docs.merchant.alb.ua/platizhni-metodi-h2h/purchase/zapit-provedennya-purchase-krok-1)[ корок 1](https://docs.merchant.alb.ua/platizhni-metodi-h2h/purchase/zapit-provedennya-purchase-krok-1)\
За допомогою розкриптованого серверного ключа - serverPublicKey, котрий отримано на кроках 1 і 2, виконується криптування тіла запиту для створення платежу на стороні Мерчанта. \
У відповідь отримуємо  зашифроване тіло запиту - \{{encryptJweT\}}\
Для тестів допускається використання допоміжного методу "/ecom/help/encrypt\_ru\_jwk"

6\. Create Purchase — `{{url}}/ecom/execute_request/payments/v3/create/purchase`\
Запит відправляє зашифроване тіло запиту - \{{encryptJweT\}}, згенероване на кроці 5. \
У відповіді отримуємо зашифровану відповідь - \{{responseJwe\}}, котра буде потрібна для виконання кроку 7.

7\. Decrypt craet purchase response —  `{{url}}/cipher/decrypt_by_jwk?message={{responseJwe}}`\
Запит декриптує відповідь від банку за допомогою приватного ключа - userPrivateKey, (котрий Мерчант генерує за інструкцією [Процес генерації комунікаційних JWK ключів клієнта](https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta)).\
У відповідь отримуємо розшифровану тіло відповіді на запит у кроці 6.&#x20;

8\. Encrypt execute purchase request body — `{{url}}/cipher/encrypt_by_jwk?message={{body_request}}`\
\{{body\_request\}} - повинно відповідати обов'язковим вхідним параметрам [PURCHASE крок 2 ](https://docs.merchant.alb.ua/platizhni-metodi-h2h/purchase/zapit-provedennya-purchase-krok-2)\
За допомогою розкриптованого серверного ключа - serverPublicKey, котрий отримано на кроках 1 і 2, виконується криптування тіла запиту на проведення платежу. \
У відповідь отримуємо  зашифроване тіло запиту - \{{encryptJweT\}}\
Для тестів допускається використання допоміжного методу "/ecom/help/encrypt\_by\_jwk"

9\. Execute Purchase — `{{url}}/ecom/execute_request/payments/v1/execute/purchase`\
Запит відправляє зашифроване тіло запиту - \{{encryptJweT\}}, згенероване на кроці 8. \
У відповіді отримуємо зашифровану відповідь - \{{responseJwe\}}, котра буде потрібна для виконання кроку 10.

10\. Decrypt execute purchase response — `{{url}}/cipher/decrypt_by_jwk?message={{responseJwe}}`\
Запит декриптує відповідь від банку за допомогою приватного ключа - userPrivateKey, (котрий Мерчант генерує за інструкцією [Процес генерації комунікаційних JWK ключів клієнта](https://docs.merchant.alb.ua/autentifikaciya#proces-generaciyi-komunikaciinikh-jwk-klyuchiv-kliyenta)).\
У відповідь отримуємо розшифровану тіло відповіді на запит у кроці 9.  \
Для тестів дозволено використання допоміжного методу "/ecom/help/encrypt\_by\_jwk"
