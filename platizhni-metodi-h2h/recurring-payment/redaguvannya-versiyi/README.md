---
description: POST /ecom/jws/scheduled_payments/plan/version/update_v1
---

# Редагування версії

Редагувати можна **тільки останню версію** плану, і обсяг дозволених змін залежить від її поточного стану

**Що можна змінити залежить від стану версії:**

<table data-header-hidden><thead><tr><th width="164.758056640625"></th><th width="228.0614013671875"></th><th></th></tr></thead><tbody><tr><td><strong>Стан версії</strong></td><td><strong>Дозволено змінити</strong></td><td><strong>Бізнес потреба</strong></td></tr><tr><td>Ще не почалась</td><td><code>appliesDateTimeFrom</code>, <code>appliesDateTimeTo</code></td><td><ol><li>Зміна дати завершення версіі</li><li>Зміна дати початку версіі (з автоскороченням активної)</li></ol></td></tr><tr><td>Вже діє</td><td>Тільки <code>appliesDateTimeTo</code></td><td><ol><li>Продовження терміну дії версіі</li><li>Скорочення терміну дії</li></ol></td></tr></tbody></table>

Параметри `coinAmount`, `intervalUnit`, `intervalValue` — НЕ редагуються. Якщо потрібно змінити суму або частоту — створюється **нова версія** плану ендпоітом [Редагування плану та додавання нової версіі](../redaguvannya-planu-ta-dodavannya-novoyi-versii.md)

Після будь-якого редагування графік ще не виконаних (`WAITING`) платежів автоматично перебудовується — вже виконані списання це не зачіпає.

#### Вхідні параметри:  <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

| **Параметр**        | **Опис**                                                                                                  | **Формат даних** | **Обовʼязковість**                                     | **Приклад**                  |
| ------------------- | --------------------------------------------------------------------------------------------------------- | ---------------- | ------------------------------------------------------ | ---------------------------- |
| planId              | Id плану                                                                                                  | uuid             | так                                                    |                              |
| versionId           | Id версіі                                                                                                 | int              | так                                                    |                              |
| infiniteVersion     | ознака нескінченності версіі                                                                              | boolean          | ні, по дефолту false                                   | true                         |
| appliesDateTimeFrom | зміна версії застосовується з                                                                             | TIMESTAMPZ       | ні, якщо параметр не передано, то нічого не змінюється | 2026-02-26 11:23:45.12+02:00 |
| appliesDateTimeTo   | <p>версія застосовується до..</p><p>після цієї дати видаляться всі заплановані платежі по цьому плану</p> | TIMESTAMPZ       | ні, якщо параметр не передано, то нічого не змінюється | 2026-02-26 11:23:45.12+02:00 |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**            | **Опис**                                                   | **Формат даних** | **Приклад**                  |
| ----------------------- | ---------------------------------------------------------- | ---------------- | ---------------------------- |
| planId                  | Унікальний ідентифікатор створеної підписки                | uuid             |                              |
| versionId               | Id версіі                                                  | int              | 1                            |
| rules.paymentNumberFrom | початковий номер платіжа з якого почина діяти дане правило | integer          | 1                            |
| rules.paymentNumberTo   | останній номер платіжа для якого ще працює правило         | integer          | 1                            |
| rules.intervalValue     | Значення білінг-інтервалу                                  | integer          | 1                            |
| rules.intervalUnit      | Одиниця білінг-інтервалу                                   | string           | MONTH                        |
| rules.coinAmount        | сума                                                       | long             | 10                           |
| rules.currency          | валюта                                                     | string           | 980                          |
| appliesDateTimeFrom     | зміна застосовується з                                     | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |
| appliesDateTimeTo       | зміна застосовується до                                    | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |
| createdAt               | Дата та час створення версіі                               | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |
| updatedAt               | Дата та час останнього оновлення версіі                    | TIMESTAMPZ       | 2026-02-26 11:23:45.12+02:00 |

#### &#x20;Приклад запиту

```json
{
   "planId":"{{planId}}",
   "versionId":"4",
   "infiniteVersion":"false",
   "appliesDateTimeTo": "2026-10-18 13:46:00.52+03:00",
   "appliesDateTimeTo": "2026-12-18 13:46:00.52+03:00"
}
```

#### &#x20;Приклад відповіді

```json
{
    "planId": "a9562240-10ca-42d7-8d90-bbd1ace3dc5a",
    "versionId": 4,
    "rules": [
        {
            "paymentNumberFrom": 1,
            "paymentNumberTo": 3,
            "intervalValue": 1,
            "intervalUnit": "DAY",
            "coinAmount": 205,
            "currency": "980"
        },
        {
            "paymentNumberFrom": 4,
            "paymentNumberTo": 6,
            "intervalValue": 1,
            "intervalUnit": "MONTH",
            "coinAmount": 8000,
            "currency": "980"
        }
    ],
    "appliesDateTimeFrom": "2026-10-18 13:46:00.52+03:00",
    "appliesDateTimeTo": "2026-12-18 12:46:00.52+02:00",
    "createdAt": "2026-07-10 11:59:54.48+03:00",
    "updatedAt": "2026-07-10 12:10:34.14+03:00"
}
```
