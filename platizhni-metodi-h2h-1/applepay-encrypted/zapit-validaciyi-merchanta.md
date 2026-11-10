---
description: >-
  Запит через сервер проксі до сервера apple pay для отримання валідації
  мерчанта
---

# Запит валідації мерчанта

`fetchAppleSessionAPI` та `purchaseApplePayAPI` - функції які викликають API, використовуйте свої функції для роботи з апі, або `fetch`

Нижче описано приклад обробника події кліку на кнопку оплати через ApplePay:

```javascript

const onApplePayButtonClicked = async () => {
    // Додаткова перевірка на те чи підтримує браузер епл пей
    if (!window.ApplePaySession) {
      return;
    }
    
    // Обʼєкт для створення сесії
    const request = {
      countryCode: 'UA', 
      currencyCode: 'UAH',
      merchantCapabilities: ['supports3DS'],
      supportedNetworks: ['visa', 'masterCard'],
      total: {
        label: 'PoC Merchant Apple Pay', // назва мерчанта
        type: 'final',
        amount: amount.toString(), // сума транзакції
      },
    };

    // Створення сесії
    const session = new window.ApplePaySession(3, request);

    session.onvalidatemerchant = async (event: any) => {
      try {
        // Виклик запиту для створення сесії https://docs.merchant.alb.ua/platizhni-metodi-h2h/applepay-encrypted/zapit-vstanovlennya-sesiyi-v-apau
        const response = await fetchAppleSessionAPI(event.validationURL, applePayMercantId, { deviceId, refreshToken });

        session.completeMerchantValidation(response.applePaySessionData);
      } catch (error) {
        // обробка помилки запиту для створення сесії
      }
    };

    session.onshippingmethodselected = () => {
      const newTotal = {
        label: 'PoC Merchant Apple Pay', // назва мерчанта
        type: 'final',
        amount: amount.toString(), // сума транзакції
      };
      session.completeShippingMethodSelection(window.ApplePaySession.STATUS_SUCCESS, {}, newTotal);
    };

    // подія коли користувач успішно вибрав картку для оплати
    session.onpaymentauthorized = async (event: any) => {

      const result = {
        status: window.ApplePaySession.STATUS_SUCCESS,
      };
      
      session.completePayment(result);
      
      try {
        // виклик запиту проведення платежу https://docs.merchant.alb.ua/platizhni-metodi-h2h/applepay-encrypted/zapit-provedennya-platezhu
        const response = await purchaseApplePayAPI(
          {
            paymentToken: event.payment.token,
            // інші дані які потрібні для виклику 
            
          }
          { deviceId, refreshToken, serverPublicKey }
        );
        
      } catch (error) {
         // обробка помилки запиту для проведення платежу
      }
    };

    session.begin();
  };

```
