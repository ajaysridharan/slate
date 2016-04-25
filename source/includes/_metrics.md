# Metrics

Metrics API allows you to retrieve your metrics. 

## MRR - Monthly Recurring Revenue

### The MRR object

> Example Response

```json
{
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":null,
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd"
}
```

### Attributes

Attribute | Description
--------- | -------
id | Customer's ID in FirstOfficer, integer


## Retrieve current month's metrics

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/metrics  \
-u YourTokenHere:
```

> Example Response

```json
{
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":null,
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd"
}
```
### HTTP Request

`GET https://api.firstofficer.io/v2/customers/<ID>`

Retrieves the details of an existing customer.

### Arguments

Argument | Description
--------- | -------
customer | The identifier of the customer to be retrieved. Use Stripe ID, FirstOfficer ID, <a href='https://www.firstofficer.io/activate_ext_id'>Extra ID</a> or email

### Returns

Returns a customer object if the call succeeded. If the customer ID does not exist, returns <a href=#errors>an error</a>.