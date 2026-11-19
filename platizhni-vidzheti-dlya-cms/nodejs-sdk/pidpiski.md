# Підписки

Підписка пов’язує покупця з планом регулярних платежів. Використовуйте той самий `AllianceBankClient` із JWS-налаштуваннями. Нижче наведено методи та DTO релізу v1.5.0.

### Методи підписок

| Метод                                  | Призначення                                                |
| -------------------------------------- | ---------------------------------------------------------- |
| `createPlanWithInfiniteSchedule(data)` | Створює план і налаштовує безстрокову дію його версії.     |
| `updatePlanWithInfiniteSchedule(data)` | Оновлює план і налаштовує безстрокову дію нової версії.    |
| `updatePlanStatus(data)`               | Змінює статус плану: ACTIVE, PAUSED або ARCHIVED.          |
| `deletePlanVersion(data)`              | Видаляє вказану версію плану.                              |
| `getPlan(data)`                        | Отримує план, його версії та доступну статистику підписок. |
| `searchPlans(data)`                    | Шукає плани за назвою/статусом із пагінацією.              |
| `createSubscriptionOrder(data)`        | Створює замовлення підписки для покупця.                   |
| `cancelSubscriptionOrder(data)`        | Надсилає запит на скасування замовлення підписки.          |
| `triggerRecurringPayment(data)`        | Надсилає запит на ручний запуск повторного платежу.        |
| `handleSubscriptionCallback(rawBody)`  | Перевіряє compact JWS і повертає SubscriptionCallbackDTO.  |

### Поля плану PlanRequestDto

| Поле                           | Тип       | Опис                                                                          |
| ------------------------------ | --------- | ----------------------------------------------------------------------------- |
| `name`                         | string    | Обов’язково. Назва плану, від 1 до 255 символів.                              |
| `description`                  | string    | Обов’язково. Опис, від 1 до 1000 символів.                                    |
| `rules`                        | object\[] | Обов’язково. Непорожній масив правил регулярних платежів.                     |
| `categorySubcategoryIndicator` | string    | Необов’язково. Індикатор категорії/підкатегорії.                              |
| `planId`                       | string    | Обов’язково для updatePlanWithInfiniteSchedule. Ідентифікатор наявного плану. |
| `merchantId`                   | string    | SDK додає з налаштувань клієнта.                                              |

### Поля правила PlanRuleDto

| Поле                | Тип           | Опис                                                                                                                     |
| ------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `paymentNumberFrom` | number (ціле) | Обов’язково. Початковий номер платежу, мінімум 1.                                                                        |
| `paymentNumberTo`   | number (ціле) | Обов’язково. Останній номер платежу; не менший за paymentNumberFrom.                                                     |
| `intervalValue`     | number (ціле) | Обов’язково. Додатна величина інтервалу між платежами.                                                                   |
| `intervalUnit`      | string        | Обов’язково. DAY, WEEK або MONTH.                                                                                        |
| `coinAmount`        | number (ціле) | Обов’язково. Сума в копійках, мінімум 0. Нуль може використовуватися для безоплатного початкового періоду.               |
| `currency`          | string        | Обов’язково. У цьому DTO підтримується рядок "980" (UAH). Це рядок, на відміну від числового currencyCode у createOrder. |

### Створення плану і перевірка результату

```javascript
import { client } from './alliance-client.js';

const result = await client.createPlanWithInfiniteSchedule({
    name: 'Premium',
    description: 'Щомісячна підписка Premium',
    rules: [
        {
            paymentNumberFrom: 1,
            paymentNumberTo: 1,
            intervalValue: 1,
            intervalUnit: 'MONTH',
            coinAmount: 0,
            currency: '980',
        },
        {
            paymentNumberFrom: 2,
            paymentNumberTo: 999,
            intervalValue: 1,
            intervalUnit: 'MONTH',
            coinAmount: 19900,
            currency: '980',
        },
    ],
});

const plan = result.getPlanResponse();

if (!result.isFullySuccessful()) {
    // План уже може існувати. Збережіть planId/versionId для звірки.
    console.error('План створено, але розклад не налаштовано повністю:', {
        planId: plan.planId,
        versionId: plan.versionId,
        error: result.getInfiniteScheduleError(),
    });
} else {
    console.log('План готовий:', plan.planId, plan.versionId);
}
```

Створення/оновлення виконується у два кроки: спочатку операція над планом, потім налаштування його версії з `infiniteVersion: true`. Якщо другий крок не вдався, метод повертає частковий результат. Перед пропозицією плану покупцям перевіряйте `isFullySuccessful()`. Не створюйте план повторно без звірки вже отриманого `planId`.

### Результат PlanLifecycleResult

| Метод                           | Тип результату  | Опис                                             |
| ------------------------------- | --------------- | ------------------------------------------------ |
| `isFullySuccessful()`           | boolean         | Чи успішно виконано обидва кроки.                |
| `getPlanResponse()`             | PlanResponseDto | План із planId, versionId та rules.              |
| `getInfiniteScheduleApplied()`  | boolean         | Чи застосовано безстрокову дію версії.           |
| `getInfiniteScheduleError()`    | string \| null  | Опис помилки другого кроку.                      |
| `getInfiniteScheduleRawError()` | unknown         | Початкова помилка другого кроку для діагностики. |

### Основні поля PlanResponseDto

| Поле                    | Тип           | Опис                                                         |
| ----------------------- | ------------- | ------------------------------------------------------------ |
| `planId`                | string        | Ідентифікатор плану у провайдера. Збережіть у своїй системі. |
| `versionId`             | number (ціле) | Ідентифікатор версії плану.                                  |
| `rules`                 | object\[]     | Правила плану у відповіді.                                   |
| `merchantId`            | string        | Необов’язково. Ідентифікатор мерчанта.                       |
| `name`                  | string        | Необов’язково. Назва.                                        |
| `description`           | string        | Необов’язково. Опис.                                         |
| `status`                | string        | Необов’язково. Статус плану.                                 |
| `appliesDateTimeFrom`   | string        | Необов’язково. Час початку дії.                              |
| `createdAt / updatedAt` | string        | Необов’язково. Час створення та оновлення.                   |

### Керування планами

| Поле         | Тип           | Опис                                                                                                    |
| ------------ | ------------- | ------------------------------------------------------------------------------------------------------- |
| `planId`     | string        | Обов’язково для getPlan, updatePlanStatus і deletePlanVersion.                                          |
| `status`     | string        | Обов’язково для updatePlanStatus: ACTIVE, PAUSED або ARCHIVED. Для searchPlans — необов’язковий фільтр. |
| `versionId`  | number (ціле) | Обов’язково для deletePlanVersion; додатний ідентифікатор версії.                                       |
| `page`       | number (ціле) | Необов’язково для searchPlans. Номер сторінки, починаючи з 0.                                           |
| `pageSize`   | number (ціле) | Необов’язково для searchPlans. Додатна кількість записів на сторінці.                                   |
| `name`       | string        | Необов’язково для searchPlans. Фільтр за назвою.                                                        |
| `merchantId` | string        | SDK додає для getPlan, searchPlans та updatePlanStatus.                                                 |

```javascript
const details = await client.getPlan({ planId: 'PLAN_ID' });
console.log(details.plan, details.versions);

const page = await client.searchPlans({
    name: 'Premium',
    status: 'ACTIVE',
    page: 0,
    pageSize: 20,
});
console.log(page.currentPage, page.plans);
```

`getPlan` повертає `plan`, `versions` і, за наявності, `subscriptionStatistics`. SDK нормалізує версії й правила, які банк може повертати як об’єкт із числовими ключами, у масиви. Дати у форматі банку можна розібрати експортованою функцією `parseBankDate`.

### Поля створення замовлення підписки

| Поле                | Тип           | Опис                                                                    |
| ------------------- | ------------- | ----------------------------------------------------------------------- |
| `planId`            | string        | Обов’язково. Ідентифікатор повністю налаштованого плану.                |
| `versionId`         | number (ціле) | Необов’язково. Додатний ідентифікатор версії плану.                     |
| `successUrl`        | string        | Обов’язково. URL повернення після успіху, до 1000 символів.             |
| `failUrl`           | string        | Обов’язково. URL повернення після помилки, до 1000 символів.            |
| `notificationUrl`   | string        | Необов’язково. URL callback підписок, до 255 символів.                  |
| `customerData`      | object        | Обов’язково. Дані покупця з постійним senderCustomerId у вашій системі. |
| `merchantId`        | string        | SDK додає з налаштувань.                                                |
| `merchantRequestId` | string        | SDK генерує для кожного виклику.                                        |

```javascript
const subscriptionOrder = await client.createSubscriptionOrder({
    planId: 'PLAN_ID',
    versionId: 1, // Реальна версія, отримана від API
    successUrl: 'https://your-site.com/subscription/success',
    failUrl: 'https://your-site.com/subscription/fail',
    notificationUrl: 'https://your-site.com/api/subscription/callback',
    customerData: { senderCustomerId: 'customer_id_1' },
});

console.log('ID замовлення підписки:', subscriptionOrder.hppOrderId);
if (subscriptionOrder.redirectUrl) {
    console.log('Посилання для покупця:', subscriptionOrder.redirectUrl);
}
```

### Поля відповіді SubscriptionOrderResponseDto

| Поле                | Тип    | Опис                                                                            |
| ------------------- | ------ | ------------------------------------------------------------------------------- |
| `hppOrderId`        | string | Ідентифікатор замовлення підписки. Збережіть для наступних операцій і callback. |
| `redirectUrl`       | string | Необов’язково. Посилання для оформлення підписки покупцем.                      |
| `merchantRequestId` | string | Необов’язково. Ідентифікатор запиту.                                            |
| `orderStatus`       | string | Необов’язково. Статус замовлення.                                               |
| `merchantId`        | string | Необов’язково. Ідентифікатор мерчанта.                                          |
| `createdAt`         | string | Необов’язково. Час створення.                                                   |

### Callback підписки

Передавайте початкове текстове тіло у `handleSubscriptionCallback`. Для підписаного маршруту вимагайте compact JWS, як у прикладі нижче. SDK також приймає JSON; сам розбір JSON не підтверджує справжність повідомлення.

`saveSubscriptionEventOnce` — функція вашого застосунку для перевірки й атомарного збереження. Вона має знайти підписку за `callback.data.hppOrderId`, звірити операцію з планом та не зараховувати один платіж повторно.

```javascript
// Використовуйте app та client із налаштувань вашого сервера.
import { saveSubscriptionEventOnce } from './subscription-store.js';

// Зареєструйте маршрут ДО app.use(express.json()).
app.post(
    '/api/subscription/callback',
    express.text({ type: '*/*', limit: '1mb' }),
    async (req, res) => {
        const rawBody = typeof req.body === 'string' ? req.body.trim() : '';
        if (!/^[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+$/.test(rawBody)) {
            return res.status(400).send('Очікується compact JWS');
        }

        let callback;
        try {
            callback = await client.handleSubscriptionCallback(rawBody);
        } catch {
            return res.status(400).send('Callback не пройшов перевірку');
        }

        try {
            await saveSubscriptionEventOnce(callback);
            return res.status(200).send('OK');
        } catch {
            return res.status(500).send('Не вдалося зберегти результат');
        }
    },
);
```

### Основні поля SubscriptionCallbackDTO.data

| Поле                       | Тип            | Опис                                                                                                    |
| -------------------------- | -------------- | ------------------------------------------------------------------------------------------------------- |
| `hppOrderId`               | string         | Ідентифікатор замовлення підписки. Обов’язковий у схемі.                                                |
| `hppPayType`               | string         | Необов’язково. Тип платежу.                                                                             |
| `orderStatus`              | string         | Необов’язково. Статус замовлення підписки.                                                              |
| `recurringTransactionType` | string \| null | Необов’язково. Ознака повторної операції. Для початкового платежу може бути відсутня, null або порожня. |
| `scheduledPaymentId`       | string \| null | Необов’язково. Ідентифікатор запланованого платежу.                                                     |
| `scheduledPayments`        | unknown        | Необов’язково. Дані розкладу; повна структура не обмежена поточною схемою.                              |
| `operation`                | object         | Необов’язково. Операція може бути відсутня у повідомленні, яке змінює лише статус.                      |
| `operation.operationId`    | string         | Необов’язково. Ідентифікатор операції для звірки та захисту від повторного нарахування.                 |
| `operation.type`           | string         | Необов’язково. Тип операції.                                                                            |
| `operation.status`         | string         | Необов’язково. Статус операції.                                                                         |
| `operation.coinAmount`     | number         | Необов’язково. Сума операції в копійках для гривневого плану.                                           |

Методи DTO: `isInitialPayment()` визначає початковий платіж; `getOperation()` повертає операцію або undefined; `has(field)` перевіряє наявність поля у вихідному повідомленні; `getRawPayload()` повертає вихідні дані; `reconcileAmount(expectedAmount)` звіряє суму. Якщо сума відсутня, звірка може повернути `ok: true` із попередженням — це не підтвердження оплати.

Для повідомлення без operation оновлюйте лише наявні поля статусу. Не стирайте попередню операцію та не трактуйте такий callback як новий платіж.

### Скасування та ручний повторний платіж

| Поле                | Тип    | Опис                                                                                                                 |
| ------------------- | ------ | -------------------------------------------------------------------------------------------------------------------- |
| `hppOrderId`        | string | Обов’язково в поточних DTO для cancelSubscriptionOrder і triggerRecurringPayment. Ідентифікатор замовлення підписки. |
| `merchantId`        | string | SDK додає з налаштувань.                                                                                             |
| `merchantRequestId` | string | SDK генерує для кожного виклику.                                                                                     |

У v1.5.0 схеми запитів цих двох методів пропускають додаткові поля, а відповіді не мають повністю зафіксованої структури. Перед використанням звірте контракт із банком і перевірте результат у тестовому середовищі. Наявність методу або HTTP 200 не гарантує потрібного бізнес-результату.

Після таймауту спочатку звірте попередню операцію: повторний виклик із новим `merchantRequestId` може створити дубль. Для помилок доступні класи `CancelSubscriptionOrderException` і `TriggerRecurringPaymentException`, а також `rawPayload` для захищеної діагностики.
