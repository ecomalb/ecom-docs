# Авторизація

У релізі **v1.5.0** запити підписуються за схемою JWS. Створіть один екземпляр `AllianceBankClient` і використовуйте його для платежів, повернень та підписок.

### Параметри авторизації

Передайте наведені поля в об’єкті `authentificationData`. Назва цього параметра в SDK пишеться саме так.

| Поле            | Тип    | Опис                                                                                                                                                              |
| --------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `baseUrl`       | string | Обов’язково. Базова URL-адреса API для вашого середовища, надана банком.                                                                                          |
| `merchantId`    | string | Обов’язково. Ідентифікатор мерчанта.                                                                                                                              |
| `jwsPrivateKey` | string | Обов’язково. Вміст приватного RSA-ключа у форматі PKCS#8 PEM, включно з рядками BEGIN PRIVATE KEY / END PRIVATE KEY. Передавайте вміст файла, а не шлях до нього. |
| `jwsKeyId`      | string | Обов’язково. Ідентифікатор ключа (kid), зареєстрованого в банку. Має відповідати приватному ключу.                                                                |

### Ініціалізація клієнта

Приклад файла `alliance-client.js`. Запускайте його на сервері як ES-модуль: додайте `"type": "module"` до `package.json` або використовуйте розширення `.mjs`.

```javascript
import { readFileSync } from 'node:fs';
import { AllianceBankClient } from '@alliance-bank/payment-sdk';

function requiredEnv(name) {
    const value = process.env[name];
    if (!value) throw new Error(`Не задано змінну ${name}`);
    return value;
}

export const client = new AllianceBankClient({
    authentificationData: {
        baseUrl: requiredEnv('ALLIANCEPAY_API_URL'),
        merchantId: requiredEnv('ALLIANCEPAY_MERCHANT_ID'),
        jwsPrivateKey: readFileSync(
            requiredEnv('ALLIANCEPAY_JWS_PRIVATE_KEY_PATH'), 'utf8'
        ),
        jwsKeyId: requiredEnv('ALLIANCEPAY_JWS_KEY_ID'),
    },
});
```

Значення змінних задайте у серверному середовищі. Приватний ключ зберігайте поза публічною директорією сайту та репозиторієм.

### Що SDK виконує автоматично

* Підписує тіло запиту алгоритмом `RS256` і формує JWS-заголовок із `kid`, `ts`, `targetUrl` та `jti`.
* Надсилає JWS у тілі запиту та додає службові HTTP-заголовки.
* Для відповіді у форматі compact JWS отримує публічний ключ банку за `kid`, перевіряє підпис і розбирає дані.

У конфігурації цього релізу використовуються чотири поля з таблиці. Параметри `serviceCode`, `authenticationKey` і `onTokenUpdate` зі старої схеми авторизації до цієї конфігурації не належать.
