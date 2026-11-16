# Налаштування та авторизація

### Валюта платежів <a href="#section-1" id="section-1"></a>

Відкрийте **Configuration → System Settings → Currencies** і перевірте, що в таблиці є валюта з кодом `UAH`. Якщо магазин виставляє рахунки в іншій валюті, перевірте курс гривні та виберіть **UAH** у полі шлюзу **Convert To For Processing**. Для планів підписки ціни продукту також задаються у гривнях.

![Валюта UAH у списку валют WHMCS](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2Fwe07uydlfjbUWSo11ghN%2Fwhmcs-ua-01-currencies.png?alt=media\&token=d9fd8dfd-8ef1-446c-9dc4-33852978ea8b)

### Реєстрація ключа JWS <a href="#jws" id="jws"></a>

Шлюз підписує запити приватним RSA-ключем мерчанта за алгоритмом `RS256`. Для підключення потрібні **Merchant ID**, приватний ключ і **JWS Key ID** (`kid`), який банк присвоїв відповідному публічному ключу.

**1.** Згенеруйте пару ключів RSA. Мінімальна довжина ключа — 2048 біт.

```sh
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out merchant_private.pem
openssl rsa -in merchant_private.pem -pubout -out merchant_public.pem
```

**2.** Передайте банку файл **merchant\_public.pem** для реєстрації. Приватний файл **merchant\_private.pem** зберігайте у себе. Для шлюзу потрібен PEM у форматі PKCS#8 без парольної фрази, з першим рядком `-----BEGIN PRIVATE KEY-----`. Якщо наявний RSA-ключ починається з `-----BEGIN RSA PRIVATE KEY-----`, перетворіть його у PKCS#8.

```sh
openssl pkcs8 -topk8 -nocrypt -in old_key.pem -out merchant_private.pem
```

**3.** Перевірте вихідний HTTPS-доступ сервера до API банку, синхронізацію часу та наявність PHP-розширень `openssl`, `sodium`, `gmp` і `hash`.

### Параметри шлюзу <a href="#section-2" id="section-2"></a>

Відкрийте **Configuration → System Settings → Payment Gateways → Manage Existing Gateways → AlliancePay Bank**.

| Поле у WHMCS                   | Що вказати                                                                                                                                                                        |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Show on Order Form**         | Увімкніть, щоб покупець міг вибрати AlliancePay під час оформлення замовлення.                                                                                                    |
| **Display Name**               | Назва способу оплати для покупця, наприклад **AlliancePay Bank**.                                                                                                                 |
| **API Base URL**               | Адреса API, яку банк надав для вашого тестового або робочого середовища.                                                                                                          |
| **Merchant ID**                | Ідентифікатор мерчанта для відповідного термінала.                                                                                                                                |
| **JWS Private Key**            | Увесь вміст `merchant_private.pem`, включно з початковим і кінцевим рядками та переносами.                                                                                        |
| **JWS Key ID**                 | Ідентифікатор `kid` зареєстрованого ключа у форматі UUID.                                                                                                                         |
| **Authentication Key**         | Застаріле поле. Для підпису JWS достатньо двох полів вище. Заповнюйте **Authentication Key** лише за окремою вказівкою банку.                                                     |
| **Payment Type**               | `PURCHASE` — разова оплата на платіжній сторінці, `A2A` — переказ з рахунку на рахунок за наявності відповідного термінала, `PREAUTH` — резервування з подальшим списанням.       |
| **Pre-Auth Expiration Period** | Для `PREAUTH` виберіть строк резервування коштів: `2h`, `4h`, `6h`, `12h`, `1d`, `2d`, `7d`, `14d` або `28d`.                                                                     |
| **Status Page Type**           | `STATUS_TIMER_PAGE` — сторінка результату з поверненням до магазину за таймером, `STATUS_REDIRECT_MERCHANT_PAGE` — одразу до магазину, `STATUS_PAGE` — сторінка результату банку. |
| **Enable Subscriptions**       | Увімкніть для продажу підписок. Їхній розклад визначає план продукту.                                                                                                             |
| **Convert To For Processing**  | Для обробки платежу в гривнях із рахунку в іншій валюті виберіть **UAH**.                                                                                                         |

![Поля шлюзу AlliancePay Bank для підпису JWS, вибору типу платежу та ввімкнення підписок](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FdjW26z83WQoOq0ZjunWw%2Fuploads%2FPWC4i3tpf9OsrBBFgjE1%2Fwhmcs-ua-02-gateway-settings.png?alt=media\&token=fe6a15c6-4b28-4d12-984f-5fd7bb208dcd)

Натисніть **Save Changes**. Щоб перевірити підключення, оформте тестовий рахунок, проведіть оплату в тестовому середовищі та звірте результат у **Billing → Transaction List**.

### Якщо підпис або перевірка відповіді не проходить <a href="#section-3" id="section-3"></a>

Підпис запиту створює мерчант. Для перевірки відповіді або повідомлення банку модуль використовує публічний ключ банку та алгоритм `ES256`. Він знаходить ключ за `kid` у заголовку JWS через `/ecom/keys/public_key/get_v1` і кешує його на одну годину.

| Повідомлення або ознака                             | Що перевірити                                                                                  |
| --------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `JWS Private Key (PEM) is not configured.`          | Заповніть **JWS Private Key** і збережіть налаштування.                                        |
| `JWS Key ID (kid) is not configured.`               | Введіть виданий банком **JWS Key ID**.                                                         |
| `JWS signing failed`                                | Перевірте тип RSA, формат PKCS#8, відсутність парольної фрази та цілісність скопійованого PEM. |
| Банк повернув `401`                                 | Звірте середовище, **Merchant ID**, відповідність `kid` приватному ключу й час на сервері.     |
| `JWS callback verification failed` у **Module Log** | Перевірте доступність API публічних ключів банку та повідомлення про перевірку підпису.        |
