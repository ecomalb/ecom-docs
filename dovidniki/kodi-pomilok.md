# Коди помилок

**Перераховані нижче коди помилок не свідчать про успішність або неуспішність транзакцій**

Для перевірки статусу транзакції необхідно:&#x20;

* очікувати callback
* перевірити статус транзакції по OPERATION\_ID
* перевірити статус транзакції по merchantRequestId

<table data-full-width="true">
    <thead>
        <tr>
            <th width="135.24999999999997">http code</th>
            <th>msgType</th>
            <th>msgCode</th>
            <th>msgText</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_terminal_not_found</td>
            <td>@Payment terminal not found</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_merchant_not_found</td>
            <td>@Merchant not found</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_reverse_transaction_failed</td>
            <td>@Failed to reverse transaction</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_payment_invalid_refund_amount</td>
            <td>@Payment invalid refund amount</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_phys_transaction_not_found</td>
            <td>@Phys transaction not found</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_cannot_process_logic_transaction</td>
            <td>@Cannot process logic transaction</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_authorize_transaction_failed</td>
            <td>@Failed to authorize transaction</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_initiate_transaction_failed</td>
            <td>@Failed to initiate transaction</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_payment_logic_transaction_not_found</td>
            <td>@Payment logic transaction not found</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_explicit_payment_execution_not_supported</td>
            <td>@Payment type doesn't support explicit execution</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_payment_not_found</td>
            <td>@Payment not found</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_operation_not_found</td>
            <td>@Operation not found</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_payment_refund_not_supported</td>
            <td>@Payment type doesn't support refund</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_invalid_request</td>
            <td>Невірний запит</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_unsupported_payment_system</td>
            <td>Платіжна система не підтримується</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_validation_card_expiration_date_and_security_code</td>
            <td>Значення повинно складатися з 7 цифр.</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_invalid_pan_format</td>
            <td>Неправильний формат повного номера картки</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_payment_invalid_refund_status</td>
            <td>@Payment invalid refund status</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_validation_card_expiration_date</td>
            <td>Значення повинно складатися з 4 цифр</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_encryptor_failed_decrypt_message</td>
            <td>Не вдалося розшифрувати повідомлення</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_virtual_device_not_found</td>
            <td>Віртуальний пристрій не знайдено</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_refresh_token_absent</td>
            <td>Токен оновлення відсутній</td>
        </tr>
        <tr>
            <td>200</td>
            <td>ERROR</td>
            <td>b_overload_error</td>
            <td>@Overload error</td>
        </tr>
        <tr>
            <td>400</td>
            <td>ERROR</td>
            <td>b_duplicate_field_value</td>
            <td>Value {data} must be unique</td>
        </tr>
        <tr>
            <td>400</td>
            <td>ERROR</td>
            <td>b_request_is_not_correct</td>
            <td>Запит не в правильному форматі</td>
        </tr>
        <tr>
            <td>400</td>
            <td>ERROR</td>
            <td>b_error_parse_json</td>
            <td>JSON parse error: {info}</td>
        </tr>
        <tr>
            <td>400</td>
            <td>ERROR</td>
            <td>b_txn_not_allowed</td>
            <td>@transaction type is not allowed for this Merchant</td>
        </tr>
        <tr>
            <td>400</td>
            <td>ERROR</td>
            <td>b_failed_to_get_apple_pay_session</td>
            <td>@Failed to get apple pay session</td>
        </tr>
        <tr>
            <td>400</td>
            <td>ERROR</td>
            <td>b_user_merchant_request_mismatch</td>
            <td>@User&#39;s merchant ID doesn&#39;t match the merchant ID from request</td>
        </tr>
        <tr>
            <td>401</td>
            <td>ERROR</td>
            <td>b_expired_token</td>
            <td>@Token Expired</td>
        </tr>
        <tr>
            <td><br /></td>
            <td>ERROR</td>
            <td>b_unknown_device</td>
            <td>@Unknown Device</td>
        </tr>
        <tr>
            <td>401</td>
            <td>ERROR</td>
            <td>b_used_token</td>
            <td>Використаний токен</td>
        </tr>
        <tr>
            <td>401</td>
            <td>ERROR</td>
            <td>b_auth_token_expired</td>
            <td>Термін дії токена аутентифікації закінчився</td>
        </tr>
        <tr>
            <td>401</td>
            <td>ERROR</td>
            <td>b_previous_auth_token_expired</td>
            <td>@Previous Auth Token Expired</td>
        </tr>
        <tr>
            <td>404</td>
            <td>ERROR</td>
            <td>b_service_unavailable</td>
            <td>@Service '{service}' unavailable</td>
        </tr>
        <tr>
            <td>404</td>
            <td>ERROR</td>
            <td>payment_operation_not_found</td>
            <td>@Payment operation is not found.</td>
        </tr>
        <tr>
            <td>404</td>
            <td>ERROR</td>
            <td>b_hpp_order_not_found</td>
            <td>@The HPP order not found</td>
        </tr>
        <tr>
            <td>404</td>
            <td>ERROR</td>
            <td>b_merchant_balances_not_found</td>
            <td>@Balance not found.</td>
        </tr>
        <tr>
            <td>500</td>
            <td>ERROR</td>
            <td>b_hpp_order_expired</td>
            <td>@The HPP order is expired</td>
        </tr>
        <tr>
            <td>500</td>
            <td>ERROR</td>
            <td>b_unknown_error</td>
            <td>Невідома помилка</td>
        </tr>
        <tr>
            <td>503</td>
            <td>ERROR</td>
            <td>b_server_is_overloaded</td>
            <td>
                <p>@Server is overloaded</p>
                <p>(необхідно повторити спробу запиту пізніше)</p>
            </td>
        </tr>
    </tbody>
</table>



#### Приклад відповіді з помилкою

```json
{
    "requestId": "29a36a0a-5926-11ed-9b6a-0242ac120002",
    "serviceId": "api-gateway",
    "msgCode": "b_used_token",
    "msgType": "ERROR",
    "msgText": "@Used Token Alert!",
    "isLocalized": false,
    "msgAttrs": {},
    "errorCauses": []
}

```
