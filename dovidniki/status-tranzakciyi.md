# Статус транзакції

Успішна транзакція повинна в собі мати такі параметри:

* status - "SUCCESS"
* approvalCode&#x20;
* actionCode - "0"
* responseCode - "00"

| Status                         | Опис                                                                |
| ------------------------------ | ------------------------------------------------------------------- |
| SUСCESS                        | Успіх                                                               |
| FAIL                           | Помилка                                                             |
| PENDING                        | На проведенні                                                       |
| REQUIRED\_3DS                  | Проведення 3DS                                                      |
| DESIRED\_THREEDS\_MODE\_ERROR  | Бізнес помилка, карта не підтримує 3DS та desiredThreeDSMode = MUST |

