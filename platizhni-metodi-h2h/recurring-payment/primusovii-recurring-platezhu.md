---
description: POST /ecom/jws/scheduled_payments/payments/recurring_subscription_v1
---

# Примусовий recurring платежу

Окрім автоматики, мерчант може **самостійно запустити** будь-який запланований платіж через API:

* Вказується конкретний `scheduled_payment_id`
* Система перевіряє статус платежу перед проведенням
* Примусове проведення recurring платежу доступне, якщо платіж має статус  `SKIPPED_PAUSED` або `FAIL_WITHOUT_RETRY`

Це корисно, якщо потрібно примусово повторити невдале списання або провести платіж поза розкладом.

#### Вхідні параметри

| **Параметри**      | **Опис**                           | **Формат даних** | **Обовʼязковість** | **Приклад**                           |
| ------------------ | ---------------------------------- | ---------------- | ------------------ | ------------------------------------- |
| merchantRequestId  | Id запиту мерчанта                 | uuid (36)        | Так                | 137d9304-0368-11ed-b939-0242ac120002  |
| merchantId         | Id мерчанта                        | uuid(36)         | Так                | 137d9304-0368-11ed-b939-0242ac120002  |
| date               | Дата                               | string           | Так                | 2024-12-13 15:35:41.170+02:00         |
| scheduledPaymentId | Id платежу який необхідно провести | uuid             | Так                |  15b24d26-1350-418d-81e3-df34138b2d80 |
| merchantComment    | додатковий коментар мерчанта       | string           | Ні                 | null                                  |

#### Вихідні параметри:  <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр** | **Опис** | **Формат даних** | **Приклад** |
| ------------ | -------- | ---------------- | ----------- |

| **Параметр**    | **Опис**                   | **Формат даних** | **Приклад**                          |
| --------------- | -------------------------- | ---------------- | ------------------------------------ |
| operationId     | Id операціі                | string           | 1712844596346b9F-WwrWZpq             |
| ecomOperationId | Id операціі в системі Ecom | string           | 8c3303e9-7396-43b8-af4e-31d9facdde9b |
| status          | статус операціі            | string           |  SENT                                |

#### Приклад запиту: <a href="#priklad-zapitu" id="priklad-zapitu"></a>

```json
{
   "merchantRequestId":"{{requestUUIDT}}",
   "merchantId":"137d9304-0368-11ed-b939-0242ac120002",
   "date":"{{currentdateT}}.00+00:00",
   "scheduledPaymentId":"15b24d26-1350-418d-81e3-df34138b2d80",
   "merchantComment":""
}
```

#### Приклад відповіді: <a href="#priklad-zapitu" id="priklad-zapitu"></a>

```json
{
   "operationId":"1778667433262DvOj-LGz42o",
   "ecomOperationId":"b6715eaa-7cf8-4d21-842f-ceac1f8c6121",
   "status":"SENT"
}
```
