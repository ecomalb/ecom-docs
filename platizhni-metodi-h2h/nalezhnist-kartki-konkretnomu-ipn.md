---
description: POST  /ecom/jws/cardholder/verify_card_inn_v1
---

# Належність картки конкретному ІПН

Ендпоінт використовується для перевірки належності картки до конкретного ІПН

#### Вхідні параметри:

| **Параметр**        | **Опис**                                                                | **Формат даних** | **Обовʼязковість** | **Приклад**                          |
| ------------------- | ----------------------------------------------------------------------- | ---------------- | ------------------ | ------------------------------------ |
| merchantId          | Id мерчанту згенерований в Єкомі                                        | uuid(36)         | Так                | 137d9304-0368-11ed-b939-0242ac120002 |
| encryptedCardNumber | номер карти зашифрований в JWE за допомогою публічного платіжного ключа | string           | Так                | \{{encryptedPanT\}}                  |
| inn                 | іпн відправника                                                         | string (10)      | Так                | 123456789                            |
| requestId           | Id запиту мерчанта                                                      | uuid             | Так                | 337d9304-0368-11ed-b939-0242ac120003 |
| requestType         | тип запиту                                                              | string           | Так                | CREDIT, PAYMENT, BETTING.            |
| userApproval        | згода клієнта на передачу даних третій стороні                          | boolean          | Так                | true                                 |

#### Вихідні параметри: <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**  | **Опис**                            | **Формат даних** | **Приклад** |
| ------------- | ----------------------------------- | ---------------- | ----------- |
| result        | Статус перевірки                    | boolean          | true\|false |
| msgText       | Опис результату або причини помилки | string           |             |

#### Приклад запиту&#x20;

```json
{
  "merchantId": "467c8a10-c705-11ed-afa1-0242ac120002",
  "encryptedCardNumber": "{{encryptedPanT}}",
  "inn": "3126509874",
  "requestId": "337d9304-0368-11ed-b939-0242ac120003",
  "requestType": "BETTING",
  "userApproval": true
}
```

#### Приклад відповіді&#x20;

```json
{
  "result": true,
  "msgText": ""
}
```

<table data-header-hidden><thead><tr><th width="61.32659912109375"></th><th width="307.84759521484375"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>#</td><td><strong>Ситуація</strong></td><td><strong><code>result</code></strong></td><td><strong><code>msgText</code></strong></td><td><strong><code>httpStatus</code></strong></td></tr><tr><td>1</td><td>BIN та ІПН збігся</td><td>true</td><td>Success</td><td>200</td></tr><tr><td>2</td><td>BIN та ІПН не збігся</td><td>false</td><td>INN mismatch</td><td>200</td></tr><tr><td>3</td><td>BIN Альянсу, картку не знайдено</td><td>false</td><td>Card not found</td><td>200</td></tr><tr><td>4</td><td>BIN Альянсу, клієнта не знайдено </td><td>false</td><td>Client not found</td><td>200</td></tr><tr><td>5</td><td>BIN Альянсу, помилка читання картки</td><td>false</td><td>Card read error</td><td>200</td></tr><tr><td>6</td><td>AFHUB вимкнено(для локального запуску)</td><td>false</td><td>Verification is disabled</td><td>503</td></tr><tr><td>7</td><td>немає в <code>d_afhub_bin</code> / неоднозначний BIN</td><td>false</td><td>Card not found</td><td>404</td></tr><tr><td>11</td><td>AFHUB відповів 405 (потрібен encrypted mode)</td><td>false</td><td>Encrypted mode required</td><td>405</td></tr><tr><td>12</td><td>AFHUB відповів 401 (помилка підпису/автентифікації)</td><td>false</td><td>AFHUB authentication failed</td><td>401</td></tr><tr><td>13</td><td>AFHUB application-помилка <code>{code,message}</code> (напр. <code>code=9</code>)</td><td>false</td><td><em>текст</em> <code>message</code> <em>від AFHUB</em></td><td><em>статус від AFHUB</em></td></tr><tr><td>14</td><td>AFHUB недоступний після 3 спроб (500/503/timeout)</td><td>false</td><td>AFHUB verification unavailable</td><td>503</td></tr><tr><td>15</td><td>Неочікувана внутрішня помилка AFHUB-флоу</td><td>false</td><td>AFHUB verification unavailable</td><td>500</td></tr></tbody></table>
