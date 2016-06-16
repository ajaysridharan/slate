# Customers

Customers API allows you to retrieve a snapshot of your customer's metrics. You can also update their extra IDs.   

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

<aside class="notice">
Extra ID is shown and returned only if the feature is activated for your product. Account owners have access rights to do that.
</aside>

### Attributes

Attribute | Description
--------- | -------
id <small>integer</small> | Customer's ID in FirstOfficer 
stripe_id <small>string</small> | Customer's ID in Stripe
extra_id <small>string</small> | Optional internal ID from Stripe metadata, <a href='https://www.firstofficer.io/activate_ext_id'>instructions here</a>
total_contract_value <small>integer</small> | The realized customer lifetime value by now. Includes all purchases
current_mrr <small>integer</small> | MRR in the current month
current_subscription_count <small>integer</small> | Subscription count in the current month. When subscription count is zero, customer is lost. This does not relate to the real-time active/cancelled subscriptions in Stripe, but customer's status in bookkeeping. Reflects the subscriptions that contributed to MRR.
currency <small>string</small> | The currency for this customer, e.g. "usd", "eur"

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

`GET https://api.firstofficer.io/v2/customers/<id>`

Retrieves the details of an existing customer.

### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The identifier of the customer to be retrieved. Use Stripe ID, FirstOfficer ID, <a href='https://www.firstofficer.io/activate_ext_id'>Extra ID</a> or email. <small class="req-badge">required</small> 

### Returns

Returns a customer object if the call succeeded. If the customer ID does not exist, returns <a href=#errors>an error</a>.

## Update a customer

> Example Request

```ruby

```


```shell
curl -X PUT https://api.firstofficer.io/v2/customers/7598372  \
-u YourTokenHere: \
-d extra_id="Team X"
```

> Example Response

```json
{
    "object": "customer",
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":"Team X",
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd"
}
```
### HTTP Request

`PUT https://api.firstofficer.io/v2/customers/<id>`

Updates the details of an existing customer. Any parameters not provided will be left unchanged. 
If there is conflicting data in Stripe, the data in Stripe will override any data set here.

### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The identifier of the customer to be retrieved. Use Stripe ID, FirstOfficer ID, <a href='https://www.firstofficer.io/activate_ext_id'>Extra ID</a> or email. <small class="req-badge">required</small>
extra_id <small>string</small> | Additional ID that will help to identify this customer. If this argument is omitted, extra_id is not changed. 

### Returns

Returns a customer object if the call succeeded. If the customer ID does not exist, returns <a href=#errors>an error</a>.