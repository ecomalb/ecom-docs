---
description: POST {{url}}/ecom/jws/cardholder/detokenize_card_v1
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

# Отримання даних картки та клієнта за номером токену (DPAN)

#### Вхідні параметри: <a href="#vkhidni-parametri" id="vkhidni-parametri"></a>

<table data-header-hidden><thead><tr><th width="168.68878173828125"></th><th width="259.669921875"></th><th></th><th width="92.4969482421875"></th><th></th></tr></thead><tbody><tr><td><strong>Параметр</strong></td><td><strong>Опис</strong></td><td><strong>Формат даних</strong></td><td><strong>Обовʼязковість</strong></td><td><strong>Приклад</strong></td></tr><tr><td>token</td><td>Номер токену картки</td><td>string</td><td>Так</td><td>5353885499598408</td></tr><tr><td>includeDateOfBirth</td><td>Ознака повернення дати народження клієнта</td><td>boolean</td><td>Ні</td><td>true</td></tr></tbody></table>

#### Вихідні параметри: <a href="#vikhidni-parametri" id="vikhidni-parametri"></a>

| **Параметр**      | **Опис**                                | **Формат даних** | **Приклад**            |
| ----------------- | --------------------------------------- | ---------------- | ---------------------- |
| pan               | Повний номер картки (FPAN).             | string           | 5375931080003599       |
| maskedPan         | Маскований номер картки                 | string           | 53759310••••3599       |
| tokenStatus       | Статус токену                           | string           | ACTIVE/INACTIVE        |
| clientFullUkrName | Повне ПІБ клієнта українською мовою     | string           | Мазепа Іван Степанович |
| dateOfBirth       | Дата народження клієнта (якщо запитано) | string           | 20.03.1639             |

**Приклад запиту**

```json
{
    "token": "5353885499598408",
    "includeDateOfBirth": true
}
```

**Приклад відповіді**&#x20;

```json
{
    "pan": "5375931080003599",
    "maskedPan": "53759310••••3599",
    "tokenStatus": "ACTIVE",
    "clientFullUkrName": "Мазепа Іван Степанович",
    "dateOfBirth": "20.03.1639"
}
```
