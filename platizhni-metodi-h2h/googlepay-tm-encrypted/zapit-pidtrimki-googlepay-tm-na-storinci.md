# Запит підтримки GooglePay™ на сторінці

Для того, щоб підключити Google Pay™ на сторінку потрібно:

1. Підключити скрипт на сторінку:

```javascript
 <script async src="https://pay.google.com/gp/p/js/pay.js" onload="onGooglePayLoaded()"></script>
```

2. Вставити наступний скріпт на сторінку (функція onGooglePayLoaded має запуститись після завантаження pay.js):

```javascript
      const baseRequest = {
        apiVersion: 2,
        apiVersionMinor: 0,
      };

      const allowedCardNetworks = ["MASTERCARD", "VISA"];

      const allowedCardAuthMethods = ["PAN_ONLY", "CRYPTOGRAM_3DS"];

      const tokenizationSpecification = {
        type: "PAYMENT_GATEWAY",
        parameters: {
          gateway: "alliance_bank ", // TODO: вказуємо потрібний gateway
          gatewayMerchantId: "123123123123324", // TODO: вказуємо потрібний merchantId
        },
      };

      const baseCardPaymentMethod = {
        type: "CARD",
        parameters: {
          allowedAuthMethods: allowedCardAuthMethods,
          allowedCardNetworks: allowedCardNetworks,
        },
      };
      
      const baseCardPaymentMethod = {
        type: "CARD",
        parameters: {
          allowedAuthMethods: allowedCardAuthMethods,
          allowedCardNetworks: allowedCardNetworks,
          assuranceDetailsRequired: true
        },
      };

      const cardPaymentMethod = Object.assign({}, baseCardPaymentMethod, {
        tokenizationSpecification: tokenizationSpecification,
      });

      let paymentsClient = null;

      function getGoogleIsReadyToPayRequest() {
        return Object.assign({}, baseRequest, {
          allowedPaymentMethods: [baseCardPaymentMethod],
        });
      }

      function getGooglePaymentDataRequest() {
        const paymentDataRequest = Object.assign({}, baseRequest);
        paymentDataRequest.allowedPaymentMethods = [cardPaymentMethod];
        paymentDataRequest.transactionInfo = getGoogleTransactionInfo();
        paymentDataRequest.merchantInfo = {
          merchantId: "12345678901234567890", // TODO: вказуємо потрібний merchantId
          merchantName: "Example Merchant", // TODO: вказуємо потрібний merchantName
        };
        return paymentDataRequest;
      }

      function getGooglePaymentsClient() {
        if (!paymentsClient) {
          paymentsClient = new google.payments.api.PaymentsClient({
            environment: "TEST",
          });
        }
        return paymentsClient;
      }

      function onGooglePayLoaded() {
        const paymentsClient = getGooglePaymentsClient();
        paymentsClient
          .isReadyToPay(getGoogleIsReadyToPayRequest())
          .then(function (response) {
            if (response.result) {
              addGooglePayButton();
            }
          })
          .catch(function (err) {
            console.error(err);
          });
      }

      function addGooglePayButton() {
        const paymentsClient = getGooglePaymentsClient();
        const button = paymentsClient.createButton({
          onClick: onGooglePaymentButtonClicked,
          allowedPaymentMethods: [baseCardPaymentMethod],
        });
        document.getElementById("container").appendChild(button);
      }

      function getGoogleTransactionInfo() {
        return {
          countryCode: "UA",
          currencyCode: "UAH",
          totalPriceStatus: "FINAL",
          totalPrice: "1.00", // TODO: вказуємо потрібну ціну
        };
      }

      function prefetchGooglePaymentData() {
        const paymentDataRequest = getGooglePaymentDataRequest();
        paymentDataRequest.transactionInfo = {
          totalPriceStatus: "NOT_CURRENTLY_KNOWN",
          currencyCode: "UAH",
        };
        const paymentsClient = getGooglePaymentsClient();
        paymentsClient.prefetchPaymentData(paymentDataRequest);
      }

      function onGooglePaymentButtonClicked() {
        const paymentDataRequest = getGooglePaymentDataRequest();
        paymentDataRequest.transactionInfo = getGoogleTransactionInfo();

        const paymentsClient = getGooglePaymentsClient();
        paymentsClient
          .loadPaymentData(paymentDataRequest)
          .then(function (paymentData) {
            processPayment(paymentData);
          })
          .catch(function (err) {
            console.error(err);
          });
      }
      function processPayment(paymentData) {
        // Далі записано приклад запиту до серверу, у запит потрібно підставити свої значення
        // Відправляємо запит на сервер, попередньо зашифрувавши його, у прикладі цього не вказано та виконувати запит під авторизацією
        // Обробка запиту не описана, через те, що на кожному проекті своя обвʼязка для виклику запитів
        // Звертати увагу прохання лише на структуру
        
        fetch('/ecom/execute_request/payments/v1/google_pay/token/purchase', {
          method: 'POST',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            "googlePayPaymentData": {
              ...paymentData,
              merchantInfo: {
                merchantId: '123123123123324', // TODO: вказуємо потрібний gatewayMerchantId
                gateway: 'alliance_bank' // TODO: вказуємо потрібний gateway
              },
            },
            environment: 'TEST', // або PRODUCTION
            coinAmount: 100, // ціна у копійках
            desiredThreeDSMode: 'MUST_NOT',
            notificationUrl: 'https://www.google.com.ua/?hl=ru',
            resultRedirectUrl: 'https://www.google.com.ua/?hl=ru',
            purpose: 'purpose',
            comment: 'comment',
            merchantId: '137d6304-0668-11ed-b939-0242ac120002', //  // TODO: вказуємо потрібний merchantId
            merchantRequestId: uuid(), // унікальний uuid
            date: getCurrentDate(), // поточна дата у форматі 
            customerData: {
              senderCustomerId: '34234234',
              senderCountry: '804',
            },
            browserInfo: {
              browserAcceptHeader:
                'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7',
              browserUserAgent:
                'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36',
              browserLanguage: 'ru-RU',
              browserColorDepth: '24',
              browserScreenHeight: '864',
              browserScreenWidth: '1536',
              browserTZ: '-180',
            },
          })
        })
      }
```

3. Вказати у allowedCardNetworks типи карток які підтримуються для платежу
4. У змінну tokenizationSpecification вставити відповідні gateway та gatewayMerchantId.
5. Для getGooglePaymentsClient використовувати **PRODUCTION** замість **TEST** для роботи з реальними даними
6. У функції getGooglePaymentDataRequest вказати merchantId та merchantName для paymentDataRequest.merchantInfo
7. У функції processPayment відправити токенізовані дані для обробки на сервер
