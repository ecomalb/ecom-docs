---
description: POST /ecom/jws/scheduled_payments/plan/status_update_v1
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Зміна статусу плана

**Зміна статусу плану**

<table data-header-hidden><thead><tr><th width="186.77117919921875"></th><th></th></tr></thead><tbody><tr><td><strong>Дія</strong></td><td><strong>Що відбувається</strong></td></tr><tr><td>ACTIVE → PAUSED</td><td>Нові списання пропускаються зі статусом <code>SKIPPED_PAUSED</code></td></tr><tr><td>PAUSED → ACTIVE</td><td>Списання відновлюються. Пропущені під час паузи НЕ компенсуються</td></tr><tr><td>→ CANCELED</td><td>Всі <code>WAITING</code> платежі → <code>INVALIDATED</code>, ордери закриваються. <strong>Необоротно!</strong></td></tr></tbody></table>

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр** | **Опис**           | **Формат даних** | **Обовʼязковість** | **Приклад**                          |
| ------------ | ------------------ | ---------------- | ------------------ | ------------------------------------ |
| planId       | Id плана           | uuid             | Так                | f21fe53d-b315-4c5c-8ed6-7ed4529f655f |
| status       | Новий статус плана | string           | Так                | CANCELED                             |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр** | **Опис**             | **Формат даних** | **Приклад**                          |
| ------------ | -------------------- | ---------------- | ------------------------------------ |
| planId       | Id плану             | uuid             | f21fe53d-b315-4c5c-8ed6-7ed4529f655f |
| merchantId   | Id мерчанта          | uuid             | 137d9304-0368-11ed-b939-0242ac120002 |
| status       | поточний стату плана | string           | CANCELED                             |

#### Приклад запиту&#x20;

```json
{
   "planId":"{{planId}}",
   "status":"CANCELED"
}
```

Приклад відповіді&#x20;

```json
{
   "planId":"f21fe53d-b315-4c5c-8ed6-7ed4529f655f",
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "status":"CANCELED"
}
```
