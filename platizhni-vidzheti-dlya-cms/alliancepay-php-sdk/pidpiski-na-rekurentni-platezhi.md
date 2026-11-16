# Підписки на рекурентні платежі

У v1.5.0 підписка пов’язує розклад платежів із конкретним замовленням покупця. План можна використати для кількох підписок. Рекурентні платежі підтримують гривню (`980`). Зберігайте `planId`, `versionId`, `hppOrderId` й операції у своєму застосунку.

### Створення й оновлення плану

У прикладі перший платіж безкоштовний, далі щомісяця списується 100,00 грн. Передайте погоджений код категорії у змінній `$categoryIndicator`.

#### Поля `PlanRequestDTO` для створення й оновлення

| Поле                           | Тип                 | Опис                                                                                                     |
| ------------------------------ | ------------------- | -------------------------------------------------------------------------------------------------------- |
| `name`                         | `string`            | Назва плану, за якою ви зможете знайти його у своєму обліку.                                             |
| `description`                  | `string` або `null` | Опис умов підписки. Для створення плану вкажіть непорожній текст.                                        |
| `merchantId`                   | `string`            | Ідентифікатор мерчанта, якому належатиме план.                                                           |
| `categorySubcategoryIndicator` | `string`            | Код категорії та підкатегорії, погоджений із банком для вашого мерчанта.                                 |
| `rules`                        | `array`             | Правила платежів за планом. Додайте окреме правило для кожного діапазону з іншою сумою чи періодичністю. |
| `planId`                       | `string` або `null` | Для оновлення передайте ID наявного плану, отриманий від банку. Під час створення пропустіть поле.       |

#### Поля правила платежів `PlanRuleDTO`

| Поле                | Тип      | Опис                                                                                             |
| ------------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `paymentNumberFrom` | `int`    | Порядковий номер першого платежу, для якого діє правило. Нумерація в прикладі починається з `1`. |
| `paymentNumberTo`   | `int`    | Порядковий номер останнього платежу цього діапазону включно.                                     |
| `intervalValue`     | `int`    | Кількість одиниць часу між платежами. Наприклад, `1` разом із `MONTH` задає щомісячний платіж.   |
| `intervalUnit`      | `string` | Одиниця інтервалу. У прикладі `MONTH` означає місяць.                                            |
| `coinAmount`        | `int`    | Сума одного платежу в копійках. `0` — безкоштовний платіж, `10000` — 100,00 грн.                 |
| `currency`          | `string` | Код валюти правила. Для гривні передайте рядок `'980'`.                                          |

```php
use AlliancePay\Sdk\Payment\Dto\Subscription\Plan\PlanRequestDTO;
use AlliancePay\Sdk\Payment\Subscription\Plan\PlanLifecycleOrchestrator;

$common = ['intervalValue' => 1, 'intervalUnit' => 'MONTH', 'currency' => '980'];
$plan = PlanRequestDTO::fromArray([
    'name' => 'Місячна підписка',
    'description' => 'Щомісячний доступ до сервісу',
    'merchantId' => $authDto->getMerchantId(),
    'categorySubcategoryIndicator' => $categoryIndicator,
    'rules' => [
        $common + ['paymentNumberFrom' => 1, 'paymentNumberTo' => 1, 'coinAmount' => 0],
        $common + ['paymentNumberFrom' => 2, 'paymentNumberTo' => 999, 'coinAmount' => 10000],
    ],
]);
$lifecycle = new PlanLifecycleOrchestrator();
$result = $lifecycle->createPlanWithInfiniteSchedule($plan, $authDto);
$planId = $result->getPlanResponse()->getPlanId();
$versionId = $result->getPlanResponse()->getVersionId();
```

#### Поля відповіді `PlanResponseDTO` у прикладі

| Поле        | Тип      | Опис                                                                                                |
| ----------- | -------- | --------------------------------------------------------------------------------------------------- |
| `planId`    | `string` | ID плану в банку. Збережіть його для оформлення підписок, перевірки деталей і подальших змін плану. |
| `versionId` | `int`    | Номер версії плану в банку. Збережіть разом із `planId`, щоб ідентифікувати версію розкладу.        |

Оркестратор спершу створює план, потім застосовує нескінченний розклад до версії. Якщо `isFullySuccessful()` повернув `false`, збережіть ідентифікатори та помилку `getInfiniteScheduleError()` для звірки. План уже може існувати в банку. Для зміни наявного плану передайте його `planId` у `PlanRequestDTO` та викличте `updatePlanWithInfiniteSchedule()`.

### Пошук і керування планами

| Дія                                     | Метод SDK                              |
| --------------------------------------- | -------------------------------------- |
| Деталі плану за planId                  | GetPlan::getPlan()                     |
| Вибірка планів за мерчантом і фільтрами | SearchPlans::searchPlans()             |
| Зміна статусу плану                     | UpdatePlanStatus::updatePlanStatus()   |
| Видалення конкретної версії             | DeletePlanVersion::deletePlanVersion() |

Щоб перевірити поточні дані в банку, виконайте запит деталей. Список планів можна відфільтрувати, наприклад, за статусом `ACTIVE`.

#### Поля запиту деталей плану `GetPlanRequestDTO`

| Поле     | Тип      | Опис                                                                       |
| -------- | -------- | -------------------------------------------------------------------------- |
| `planId` | `string` | Ідентифікатор плану в банку. Візьміть його з відповіді на створення плану. |

```php
use AlliancePay\Sdk\Payment\Dto\Subscription\Plan\GetPlanRequestDTO;
use AlliancePay\Sdk\Payment\Subscription\Plan\GetPlan;

$getPlan = new GetPlan();
$details = $getPlan->getPlan(new GetPlanRequestDTO($planId), $authDto);
$statistics = $details->getSubscriptionStatistics();
```

### Оформлення та скасування підписки

Після вибору плану створіть окреме HPP-замовлення для покупця.

#### Поля `SubscriptionOrderRequestDTO` у прикладі

| Поле                | Тип      | Опис                                                                                             |
| ------------------- | -------- | ------------------------------------------------------------------------------------------------ |
| `planId`            | `string` | ID обраного плану, отриманий від банку під час його створення.                                   |
| `merchantId`        | `string` | Ідентифікатор мерчанта, якому належить план.                                                     |
| `merchantRequestId` | `string` | Унікальний ID запиту на оформлення підписки. Згенеруйте його у своєму застосунку.                |
| `statusPageType`    | `string` | Вигляд сторінки результату. У прикладі використано `STATUS_TIMER_PAGE`.                          |
| `successUrl`        | `string` | Адреса, куди повернеться покупець після успішного оформлення.                                    |
| `failUrl`           | `string` | Адреса, куди повернеться покупець у разі невдалого оформлення.                                   |
| `hppPaymentMethods` | `array`  | Способи оплати на платіжній сторінці для підписки. У прикладі передано `['CARD']`.               |
| `customerData`      | `array`  | Дані покупця. У вкладеному полі `senderCustomerId` передайте його ідентифікатор у вашій системі. |

```php
use AlliancePay\Sdk\Payment\Dto\Subscription\SubscriptionOrder\SubscriptionOrderRequestDTO;
use AlliancePay\Sdk\Payment\Subscription\SubscriptionOrder\CreateSubscriptionOrder;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

$request = SubscriptionOrderRequestDTO::fromArray([
    'planId' => $planId,
    'merchantId' => $authDto->getMerchantId(),
    'merchantRequestId' => GenerateRequestIdentification::generateRequestId(),
    'statusPageType' => 'STATUS_TIMER_PAGE',
    'successUrl' => 'https://shop.example/pay/success',
    'failUrl' => 'https://shop.example/pay/fail',
    'hppPaymentMethods' => ['CARD'],
    'customerData' => ['senderCustomerId' => '12345'],
]);
$order = (new CreateSubscriptionOrder())->createSubscriptionOrder($request, $authDto);
$hppOrderId = $order->getHppOrderId();
$redirectUrl = $order->getRedirectUrl();
```

#### Поля відповіді на оформлення підписки

| Поле          | Тип      | Опис                                                                                                                                  |
| ------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `hppOrderId`  | `string` | Збережіть ID банківського замовлення разом із локальною підпискою. Він знадобиться, щоб знайти підписку за callback або скасувати її. |
| `redirectUrl` | `string` | Посилання на оформлення підписки на платіжній сторінці банку. Перенаправте за ним покупця.                                            |

#### Поля `SubscriptionOrderCancelRequestDTO`

| Поле         | Тип      | Опис                                                                                                     |
| ------------ | -------- | -------------------------------------------------------------------------------------------------------- |
| `hppOrderId` | `string` | ID замовлення конкретної підписки. Збережіть його з відповіді на оформлення та передайте при скасуванні. |
| `merchantId` | `string` | Ідентифікатор мерчанта, у якого оформлено підписку.                                                      |

Перевірте результат скасування перед оновленням локального стану.

```php
use AlliancePay\Sdk\Payment\Dto\Subscription\SubscriptionOrder\SubscriptionOrderCancelRequestDTO;
use AlliancePay\Sdk\Payment\Subscription\SubscriptionOrder\CancelSubscriptionOrder;

$cancelSubscriptionOrder = new CancelSubscriptionOrder();
$response = $cancelSubscriptionOrder->cancelSubscriptionOrder(
    new SubscriptionOrderCancelRequestDTO($hppOrderId, $authDto->getMerchantId()),
    $authDto
);
```

### Плановий платіж і ручний запуск

#### Поля `RecurringPaymentTriggerRequestDTO`

| Поле                 | Тип                 | Опис                                                                                                                     |
| -------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `merchantRequestId`  | `string`            | Унікальний ID цього запиту на запуск платежу. Згенеруйте й збережіть його перед викликом.                                |
| `merchantId`         | `string`            | Ідентифікатор мерчанта. Використайте значення з `$authDto->getMerchantId()`.                                             |
| `date`               | `string`            | Дата й час запланованого платежу з мілісекундами та зміщенням часового поясу. Приклад — `2026-11-16 15:35:41.170+02:00`. |
| `scheduledPaymentId` | `string`            | ID конкретного запланованого платежу в банку. Збережіть його разом із датою у своєму журналі платежів.                   |
| `merchantComment`    | `string` або `null` | Необов’язковий коментар мерчанта до запиту.                                                                              |

Перед повторною спробою ручного запуску звірте попередні операції запланованого платежу.

```php
use AlliancePay\Sdk\Payment\Dto\Subscription\Payment\RecurringPaymentTriggerRequestDTO;
use AlliancePay\Sdk\Payment\Subscription\Payment\TriggerRecurringPayment;
use AlliancePay\Sdk\Services\RequestIdentification\GenerateRequestIdentification;

$trigger = new TriggerRecurringPayment();
$response = $trigger->triggerRecurringPayment(
    new RecurringPaymentTriggerRequestDTO(
        GenerateRequestIdentification::generateRequestId(),
        $authDto->getMerchantId(),
        $scheduledPaymentDate, // "2024-12-13 15:35:41.170+02:00"
        $scheduledPaymentId,   // з власного журналу запланованих платежів застосунку
    ),
    $authDto
);
```

### Callback та облік повторних доставок

Виконайте перевірку підпису з інструкції «Робота з асинхронними відповідями Callback». Передайте отриманий масив `$verified` обробнику підписок.

```php
use AlliancePay\Sdk\Payment\Subscription\Callback\SubscriptionCallbackHandler;

$callback = (new SubscriptionCallbackHandler())->handle($authDto, $verified);
$hppOrderId = $callback->getHppOrderId();
$isInitial = $callback->isInitialPayment();
$operation = $callback->getOperation();
if ($operation !== null) {
    $operationId = $operation->getOperationId();
    // Оновіть відповідну операцію за її ID у транзакції вашого застосунку.
}
```

#### Поля `SubscriptionCallbackDTO` для звірки платежу

| Поле                       | Тип                                                        | Опис                                                                                                                                |
| -------------------------- | ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `hppOrderId`               | `string`                                                   | ID замовлення підписки в банку. За ним знайдіть підписку у своєму застосунку.                                                       |
| `orderStatus`              | `string`                                                   | Стан замовлення на момент повідомлення.                                                                                             |
| `recurringTransactionType` | `string` або `null`                                        | Ознака типу рекурентної операції. Метод `isInitialPayment()` повертає `true`, якщо поле порожнє або має значення `null`.            |
| `scheduledPaymentId`       | `string` або `null`                                        | Якщо значення є, за ним знайдіть відповідний платіж у розкладі.                                                                     |
| `operation`                | `OperationPurchaseDTO` або `OperationRefundDTO` або `null` | Деталі операції. Якщо об’єкт є, зіставте його `operationId` із записом у своєму обліку. Повідомлення може надійти лише зі статусом. |

Якщо наступне повідомлення містить більше деталей, доповніть локальний запис і збережіть відомі значення. Розбіжність суми, виявлену через `reconcileAmount()`, передайте на звірку.

Захист від дублювання планів і замовлень забезпечує застосунок. Перед створенням зафіксуйте локальну спробу. Якщо відповідь банку втрачено, звірте стан перед повторним запитом.
