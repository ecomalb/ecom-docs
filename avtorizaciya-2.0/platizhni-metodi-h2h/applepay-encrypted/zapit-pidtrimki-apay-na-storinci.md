---
description: >-
  Необхідно виконати скрипт для перевірки підтримки оплати за допомогою Арау на
  сторінці
---

# Запит підтримки aPay на сторінці

```javascript
if (!window.ApplePaySession || !window.ApplePaySession?.canMakePayments?.()) {
    return <div>Apple Pay is not supported on this device</div>;
}
```
