# Авторизація

Для роботи з SDK необхідно створити екземпляр класу `AllianceBankClient`. Він автоматично керує станом токенів та їх оновленням за допомогою `RetryHttpClient` та внутрішнього сервісу авторизації.

Приклад ініціалізації:

```
import { AllianceBankClient, AllianceSDKConfig } from '@alliancepay/sdk-nodejs';

const config: AllianceSDKConfig = {
    authentificationData: {
        baseUrl: '[https://api-ecom-prod.bankalliance.ua/](https://api-ecom-prod.bankalliance.ua/)', // Базовий URL сервісу надається банком
        merchantId: 'YOUR_MERCHANT_ID', 
        serviceCode: 'YOUR_SERVICE_CODE', 
        authenticationKey: 'YOUR_AUTH_KEY' // Надається банком
    },
    // ВАЖЛИВО: Використовуйте цей колбек для збереження оновлених токенів у вашій базі даних
    onTokenUpdate: async (updatedAuth) => {
        // Наприклад: await db.saveAuthToken(updatedAuth);
    }
};

const client = new AllianceBankClient(config);
```

**Особливість архітектури:**

SDK використовує Lazy Loading (ліниву ініціалізацію).

Внутрішні сервіси створюються лише в момент першого виклику, що робить клієнт максимально легким та економить пам'ять.
