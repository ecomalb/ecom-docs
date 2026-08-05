---
description: >-
  Для безшовного переходу з поточного формату авторизації на JWS Authorization
  2.0 рекомендуємо виконувати інтеграцію поетапно.
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

# Порядок переходу на JWS Authorization 2.0

{% stepper %}
{% step %}
### Крок 1. Ознайомитися з форматом JWS Authorization 2.0

У новому форматі авторизації запити до Ecom передаються у вигляді JWS:

```
HEADER.PAYLOAD.SIGNATURE
```

де:

* `HEADER` — містить службову інформацію, необхідну для перевірки запиту;
* `PAYLOAD` — містить параметри API-запиту;
* `SIGNATURE` — цифровий підпис запиту, сформований приватним ключем мерчанта.

Перед початком інтеграції рекомендуємо ознайомитися з принципом формування та підписання JWS: [Робота з підписанням](https://docs.merchant.alb.ua/avtorizaciya-2.0/robota-z-pidpisannyam)

### Крок 2. Згенерувати ключі для підписання JWS
{% endstep %}

{% step %}
Для роботи з JWS необхідно згенерувати пару криптографічних ключів:

* `Private Key` — використовується мерчантом для підписання JWS-запитів;
* `Public Key` — використовується Банком для перевірки підпису запитів мерчанта.

`Private Key` повинен зберігатися виключно на стороні мерчанта та не передаватися Банку або третім особам.

Генерацію ключів необхідно виконувати відповідно до параметрів та алгоритмів, зазначених у документації : [Генерація ключів](https://docs.merchant.alb.ua/avtorizaciya-2.0/generaciya-klyuchiv?select=%D0%B7%D0%B0%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-payload,%D1%80%D0%BE%D0%B7%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-payload,%D0%B7%D0%B0%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-header,%D1%80%D0%BE%D0%B7%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-header)
{% endstep %}

{% step %}
### Крок 3. Передати Public Key Банку

Для підключення JWS Authorization 2.0 до існуючого `merchantId` необхідно передати Банку згенерований `Public Key`.

Публічний ключ необхідно направити на:

`aromashkan@alliancedigital.tech`

Після реєстрації ключа на стороні Банку мерчанту буде надано ідентифікатор ключа — `kid`.

Отриманий `kid` необхідно використовувати при формуванні `HEADER` JWS-запитів.

Наприклад:

```
{
  "alg": "ES256",
  "kid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "ts": "1769174930000",
  "targetUrl": "/ecom/jws/payments/create/purchase_v3"
}
```
{% endstep %}

{% step %}
### Крок 4. Реалізувати формування та підписання JWS

Для кожного API-запиту необхідно:

1. Сформувати `HEADER`.
2. Сформувати `PAYLOAD` відповідно до документації конкретного ендпоінта.
3. Закодувати необхідні частини JWS.
4. Сформувати `SIGNATURE` за допомогою `Private Key` мерчанта.
5. Передати сформований JWS на відповідний JWS-ендпоінт Ecom.

При формуванні `HEADER` необхідно враховувати:

* `alg` — алгоритм підписання;
* `kid` — ідентифікатор зареєстрованого публічного ключа мерчанта;
* `ts` — час формування JWS;
* `targetUrl` — URL API-методу, для якого формується JWS.

Детальніше: [https://docs.merchant.alb.ua/avtorizaciya-2.0/robota-z-pidpisannyam](https://docs.merchant.alb.ua/avtorizaciya-2.0/robota-z-pidpisannyam)
{% endstep %}

{% step %}
### Крок 5. Реалізувати шифрування карткових даних

Якщо мерчант використовує API-методи, в яких передаються карткові дані, необхідно додатково реалізувати їх шифрування.

Шифрування карткових даних та підписання JWS є окремими механізмами.

Детальніше:

[https://docs.merchant.alb.ua/avtorizaciya-2.0/shifruvannya-kartkovikh-danikh](https://docs.merchant.alb.ua/avtorizaciya-2.0/shifruvannya-kartkovikh-danikh)
{% endstep %}

{% step %}
### Крок 6. Реалізувати перевірку JWS-відповідей Банку

Відповіді Ecom повертаються мерчанту у форматі JWS та містять цифровий підпис Банку.

{% hint style="info" %}
Перевірка відповіді, не є обов'язковим
{% endhint %}

На стороні мерчанта необхідно реалізувати перевірку цього підпису.

Загальний алгоритм:

1. Отримати JWS-відповідь.
2. Декодувати `HEADER`.
3. Отримати значення `kid`.
4. За `kid` визначити публічний ключ Банку.
5. Перевірити `SIGNATURE`.
6. Після успішної перевірки обробити дані з `PAYLOAD`.

Якщо необхідний публічний ключ Банку ще не був отриманий, його можна отримати через:

```
/ecom/keys/public_key/get_v1
```

Детальніше про перевірку підпису:

[https://docs.merchant.alb.ua/avtorizaciya-2.0/obrobka-sinkhronnikh-asinkhronnikh-vidpovidei#perevirka-pidpisu](https://docs.merchant.alb.ua/avtorizaciya-2.0/obrobka-sinkhronnikh-asinkhronnikh-vidpovidei#perevirka-pidpisu)
{% endstep %}

{% step %}
### Крок 7. Провести тестування інтеграції

Перед переходом на JWS Authorization 2.0 у production необхідно провести тестування інтеграції.

Для цьго рекомендуємо ознайомитись з покроковим описом робот з JWS на прикладі операції [Purchase](https://docs.merchant.alb.ua/avtorizaciya-2.0/opis-roboti-z-jws?select=%D0%B7%D0%B0%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-payload,%D1%80%D0%BE%D0%B7%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-payload,%D0%B7%D0%B0%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-header,%D1%80%D0%BE%D0%B7%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B0-%D1%87%D0%B0%D1%81%D1%82%D0%B8%D0%BD%D0%B0-header)

Після успішного проходження тестування можна погоджувати переключення інтеграції на JWS Authorization 2.0.
{% endstep %}
{% endstepper %}
