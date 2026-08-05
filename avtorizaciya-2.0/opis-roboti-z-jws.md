# Опис роботи з JWS

## Приклад роботи з JWS для Purchase платежу

```mermaid

sequenceDiagram
    autonumber

    participant M as Merchant
    participant E as Ecom

    Note over M: Підготовка Purchase

    M->>M: Шифрування карткових даних
    M->>M: Формування Header для Create Purchase
    M->>M: Формування Payload
    M->>M: Підписання JWS приватним ключем

    M->>E: JWS<br/>POST /ecom/jws/payments/create/purchase_v3

    E->>E: Пошук public key мерчанта за kid
    E->>E: Перевірка JWS Signature
    E->>E: Обробка Create Purchase
    E->>E: Формування та підписання JWS Response

    E-->>M: JWS Response

    M->>M: Декодування Header
    M->>M: Отримання kid Банку

    opt Публічний ключ ще не отримано
        M->>E: Запит public key за kid
        E-->>M: Public Key Банку
    end

    M->>M: Перевірка Signature відповіді

    alt Signature валідний
        M->>M: Обробка Payload
    else Signature невалідний
        M->>M: Відхилення відповіді
    end

    Note over M: Execute Purchase

    M->>M: Формування Header для Execute Purchase
    M->>M: Формування Payload
    M->>M: Підписання нового JWS

    M->>E: JWS<br/>POST /ecom/jws/payments/execute/purchase_v1

    E->>E: Перевірка JWS Signature
    E->>E: Виконання Purchase
    E->>E: Формування JWS Response

    E-->>M: JWS Response

    M->>M: Отримання kid з Header
    M->>M: Перевірка Signature

    alt Signature валідний
        M->>M: Декодування та обробка Payload
        M->>M: Обробка результату Purchase
    else Signature невалідний
        M->>M: Відхилення відповіді
    end
```

#### Опис :&#x20;

1. Мерчант шифрує карткові дані.
2. Формує `payload` для Create Purchase.
3. Формує `header` з `alg`, `kid`, `ts` та `targetUrl`.
4. Підписує JWS своїм приватним ключем.
5. Відправляє JWS на `/ecom/jws/payments/create/purchase_v3`.
6. Отримує JWS-відповідь Банку.
7. Отримує `kid` з `header` відповіді.
8. За необхідності отримує відповідний public key Банку та верифікує підпис відповіді.
9. Отримує дані для наступного кроку з `payload`.
10. Формує новий JWS для Execute Purchase.
11. Відправляє його на `/ecom/jws/payments/execute/purchase_v1`.
12. Отримує фінальну JWS-відповідь.
13. Перевіряє її цифровий підпис.
14. Обробляє результат виконання Purchase.
