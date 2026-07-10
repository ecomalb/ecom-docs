---
description: POST /ecom/jws/scheduled_payments/plan/version/update_v1
---

# Редагування версії

**Що можна змінити залежить від стану версії:**

| **Стан версії** | **Дозволено змінити**                      | **Заборонено** |
| --------------- | ------------------------------------------ | -------------- |
| Ще не почалась  | `appliesDateTimeFrom`, `appliesDateTimeTo` | Суму, інтервал |
| Вже діє         | Тільки `appliesDateTimeTo`                 | Все інше       |

Параметри `coinAmount`, `intervalUnit`, `intervalValue` — НЕ редагуються. Якщо потрібно змінити суму або частоту — створюється **нова версія** плану ендпоітом [https://app.gitbook.com/o/zBSkiJ3Oy2kvtv30JbMh/s/djW26z83WQoOq0ZjunWw/\~/edit/\~/changes/368/platizhni-metodi-h2h/recurring-payment/redaguvannya-planu-ta-dodavannya-novoyi-versii](redaguvannya-planu-ta-dodavannya-novoyi-versii.md)

&#x20;
