# AlliancePay PHP SDK

AlliancePay PHP SDK підключає серверний PHP-застосунок до [платіжної сторінки банку (HPP)](https://docs.merchant.alb.ua/platizhni-metodi-hpp). Цей розділ описує реліз `v1.5.0` та охоплює разову оплату, резервування коштів, повернення й рекурентні платежі.

### Перший платіж

Почніть із [встановлення](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/vstanovlennya), налаштуйте [авторизацію JWS](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/avtorizaciya) і [створіть замовлення](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/stvorennya-zamovlennya). Збережіть виданий банком `hppOrderId` та перенаправте покупця на платіжну сторінку.

Результат оплати отримуйте через [серверний callback](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/robota-z-asinkhronnimi-vidpovidyami-callback). Для звірки відкрийте [перевірку стану замовлення](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/perevirka-stanu-zamovlennya).

### Інші платіжні сценарії

Для двоетапної оплати використовуйте [PREAUTH і COMPLETION](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/preauth-and-completion-php-sdk). Щоб повернути кошти після успішного списання, виконайте [повернення](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/vikonannya-povernen). Для регулярних списань налаштуйте [план і підписку покупця](https://docs.merchant.alb.ua/platizhni-vidzheti-dlya-cms/alliancepay-php-sdk/pidpiski-na-rekurentni-platezhi).

[Вихідний код SDK v1.5.0](https://github.com/alliancedigital-tech/alliancepay-php-sdk/tree/v1.5.0)
