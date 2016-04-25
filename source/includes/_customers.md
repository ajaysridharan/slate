# Customers

Customers API allows you to retrieve a snapshot of your customer's metrics. 

## The customer object

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
stripe_id | Customers ID in Stripe, string
extra_id | Optional internal ID from Stripe metadata, <a href='https://www.firstofficer.io/activate_ext_id'>instructions here</a>, string
total_contract_value | The realized customer lifetime value by now. Includes all purchases, integer
current_mrr | MRR in the current month, integer
current_subscription_count | Subscription count in the current month, integer. When subscription count is zero, customer is lost. This does not relate to the real-time active/cancelled subscriptions in Stripe, but customer's status in bookkeeping. Reflects the subscriptions that contributed to MRR.
currency | The currency for this customer, e.g. "usd", "eur", string.

## Retrieve a customer

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/customers/cus_1234ABCD  \
-u YourTokenHere:
```

> Example Response

```json
{
    "object": "customer",
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