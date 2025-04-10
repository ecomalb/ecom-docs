# Коди помилок

**Перераховані нижче коди помилок не свідчать про успішність або неуспішність транзакцій**

Для перевірки статусу транзакції необхідно:&#x20;

* очікувати callback
* перевірити статус транзакції по OPERATION\_ID
* перевірити статус транзакції по merchantRequestId

<table data-full-width="true"><thead><tr><th width="135.24999999999997"> http  code</th><th> msgType</th><th>msgCode</th><th>msgText</th></tr></thead><tbody><tr><td>200</td><td>ERROR</td><td>b_terminal_not_found</td><td>@Payment terminal not found</td></tr><tr><td><br></td><td>ERROR</td><td>b_merchant_not_found</td><td>@Merchant not found</td></tr><tr><td><br></td><td>ERROR</td><td>b_reverse_transaction_failed</td><td>@Failed to reverse transaction</td></tr><tr><td><br></td><td>ERROR</td><td>b_payment_invalid_refund_amount</td><td>@Payment invalid refund amount</td></tr><tr><td><br></td><td>ERROR</td><td>b_phys_transaction_not_found</td><td>@Phys transaction not found</td></tr><tr><td><br></td><td>ERROR</td><td>b_cannot_process_logic_transaction</td><td>@Cannot process logic transaction</td></tr><tr><td><br></td><td>ERROR</td><td>b_authorize_transaction_failed</td><td>@Failed to authorize transaction</td></tr><tr><td><br></td><td>ERROR</td><td>b_initiate_transaction_failed</td><td>@Failed to initiate transaction</td></tr><tr><td><br></td><td>ERROR</td><td>b_payment_logic_transaction_not_found</td><td>@Payment logic transaction not found</td></tr><tr><td><br></td><td>ERROR</td><td>b_explicit_payment_execution_not_supported</td><td>@Payment type doesn't support explicit execution</td></tr><tr><td><br></td><td>ERROR</td><td>b_payment_not_found</td><td>@Payment not found</td></tr><tr><td><br></td><td>ERROR</td><td>b_operation_not_found</td><td>@Operation not found</td></tr><tr><td><br></td><td>ERROR</td><td>b_payment_refund_not_supported</td><td>@Payment type doesn't support refund</td></tr><tr><td>401</td><td>ERROR</td><td>b_expired_token</td><td>@Token Expired</td></tr><tr><td><br></td><td>ERROR</td><td>b_unknown_device</td><td>@Unknown Device</td></tr><tr><td>404</td><td>ERROR</td><td>b_service_unavailable</td><td>@Service '{service}' unavailable </td></tr><tr><td>503</td><td>ERROR</td><td>b_server_is_overloaded</td><td><p>@Server is overloaded</p><p>(необхідно повторити спробу запиту пізніше)</p></td></tr></tbody></table>

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
