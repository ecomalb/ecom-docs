---
description: >-
  PREAUTH дозволяє заморозити кошти на картці клієнта без їх фактичного
  списання. Кошти утримуються до моменту виконання COMPLETION або закінчення
  терміну дії авторизації.
---

# PreAuth and Completion NodeJS SDK

## Попередня авторизація (PREAUTH) <a href="#id-5.-poperednya-avtorizaciya-preauth" id="id-5.-poperednya-avtorizaciya-preauth"></a>

Для ініціювання передайте `hppPayType: 'PREAUTH'` у метод `createOrder`. SDK автоматично встановить `preAuthExpDate` — поточний час плюс 2 години 30 секунд — якщо поле не передано явно.

{% hint style="info" %}
`preAuthExpDate` є необов'язковим. При ручному передаванні використовуйте формат `YYYY-MM-DD HH:mm:ss.SS±HH:MM`, наприклад `2025-11-13 15:01:54.56+02:00`. Значення має бути не раніше ніж через 2 години та не пізніше ніж через 28 днів від поточного моменту.
{% endhint %}

**Приклад ініціювання PREAUTH:**

```js
const orderData = {
    coinAmount: 25000, // Сума в копійках
    hppPayType: 'PREAUTH',
    paymentMethods: ['CARD'],
    successUrl: 'https://your-site.com/success',
    failUrl: 'https://your-site.com/fail',
    statusPageType: 'STATUS_TIMER_PAGE',
    customerData: { senderCustomerId: 'customer_id_1' },
};
try {
    const response = await client.createOrder(orderData);
    console.log('Redirect to payment page:', response.redirectUrl);
    console.log('HPP Order ID:', response.hppOrderId);
} catch (error) {
    console.error('PREAUTH order creation failed:', error);
}
```

Після успішної авторизації сервіс надішле callback з `operation.type === 'PREAUTH'`. Збережіть `operation.operationId` з callback — він знадобиться для виконання COMPLETION.



## Завершення авторизації (COMPLETION)

**COMPLETION** списує кошти, заморожені попередньою PREAUTH-операцією. Сума списання може відрізнятися від суми попередньої авторизації не більше ніж на **±20%**.

Метод `createCompletion` приймає два аргументи:

1. об'єкт із `originalOperationId`, `coinAmount` та опціональним `notificationUrl`;
2. `originalCoinAmount` — суму оригінальної PREAUTH-операції в копійках для перевірки допустимого діапазону.

SDK автоматично додає `merchantId`, `merchantRequestId` та `date`.

**Приклад виконання COMPLETION:**

```js
import { CompletionAmountException, AllianceSdkException } from '@alliancepay/sdk-nodejs';

const originalCoinAmount = 25000;

try {
    const completionResponse = await client.createCompletion(
        {
            originalOperationId: 'PREAUTH_OPERATION_ID',
            coinAmount: 24000, // Допустимий діапазон: 20000–30000
            notificationUrl: '<redacted URL>',
        },
        originalCoinAmount
    );

    console.log('Completion status:', completionResponse.status);
    console.log('ecomOperationId:', completionResponse.ecomOperationId);
    console.log('Original PREAUTH operationId:', completionResponse.preauthOperationId);
    console.log('Original PREAUTH amount (coins):', completionResponse.preauthCoinAmount);
} catch (error) {
    if (error instanceof CompletionAmountException) {
        console.error('Amount out of allowed range:', error.message);
    } else if (error instanceof AllianceSdkException) {
        console.error(`Bank Error Code: ${error.code}`);
        console.error(`Message: ${error.message}`);
    } else {
        console.error('Unexpected error:', error);
    }
}
```

