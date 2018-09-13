# Customers

Customers API allows you to retrieve a snapshot of your customer's metrics. You can also update their data. 
  
FirstOfficer cannot change the data in Stripe, so changes done here will not affect customer billing or their data in Stripe. 

## The customer object

> Example Response

```json
{
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":null,
    "email":"tester@example.com",
    "name":"John Doe",
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd",
    "country": "US", 
    "state": "OH"
}
```

<aside class="notice">
Extra ID is shown and returned only if the feature is activated for your product. Account owners have access rights to enable and disable optional features.
</aside>

### Attributes

Attribute | Description
--------- | -------
id <small>integer</small> | Customer's ID in FirstOfficer 
stripe_id <small>string</small> | Customer's ID in Stripe
extra_id <small>string</small> | Optional internal ID from Stripe metadata, <a href='https://www.firstofficer.io/activate_ext_id'>instructions here</a>
email <small>string</small> | Customer's email. 
total_contract_value <small>integer</small> | The realized customer lifetime value by now. Includes all purchases
current_mrr <small>integer</small> | MRR in the current month
current_subscription_count <small>integer</small> | Subscription count in the current month. When subscription count is zero, customer is lost. This does not relate to the real-time active/cancelled subscriptions in Stripe, but customer's status in bookkeeping. Reflects the subscriptions that contributed to MRR.
currency <small>string</small> | The currency for this customer, e.g. "usd", "eur"
country <small>string</small> | The country for this customer, e.g. “US”, “FI”
state <small>string</small> | The US state for this customer, e.g. “OH”, “CA”. If customer does not reside in the US, the state will be empty.

## Create a customer

> Example Request

```ruby

```


```shell
curl -X POST https://api.firstofficer.io/v2/customers  \
-u YourTokenHere: \
-d email="customer@company.com"
```

> Example Response

```json
{
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":null,
    "email":"tester@example.com",
    "name":"John Doe",
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd",
    "country": "US", 
    "state": "OH"
}
```
### HTTP Request

`POST https://api.firstofficer.io/v2/customers`

Creates a customer.

### Arguments

Argument | Description
--------- | -------
email <small>string</small> | The email of the customer, unique. <small class="req-badge">required</small>
name <small>string</small> | The name of the customer.
extra_id <small>string</small> | Additional ID that will help to identify this customer. 

### Returns

Returns a customer object if the call succeeded. If arguments are invalid, returns <a href=#errors>an error</a>.

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
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":null,
    "email":"tester@example.com",
    "name":"John Doe",
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd",
    "country": "US", 
    "state": "OH"
}
```
### HTTP Request

`GET https://api.firstofficer.io/v2/customers/<id>`

Retrieves the details of an existing customer.

### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The FirstOfficer ID of the customer to be retrieved. Stripe ID, <a href='https://www.firstofficer.io/activate_ext_id'>Extra ID</a> will also work, but are deprecated and will be removed in V3. <small class="req-badge">required</small> 

### Returns

Returns a customer object if the call succeeded. The extra_id arguments may match to several customers, but only one customer is returned. 

If the customer ID does not exist, returns <a href=#errors>an error</a>.

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
    "id":1340573,
    "stripe_id":"cus_1234ABCD",
    "extra_id":"Team X",
    "email":"tester@example.com",
    "name":"John Doe",
    "total_contract_value":629100,
    "current_mrr":69900,
    "current_subscription_count":1,
    "currency":"usd",
    "country": "US", 
    "state": "OH"
}
```
### HTTP Request

`PUT https://api.firstofficer.io/v2/customers/<id>`

Updates the details of an existing customer. Any parameters not provided will be left unchanged. 
If there is conflicting data in Stripe, the data in Stripe will override any data set here.

### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The FirstOfficer ID of the customer to be retrieved. Stripe ID or <a href='https://www.firstofficer.io/activate_ext_id'>Extra ID</a> will also work, but are deprecated and will be removed in V3. <small class="req-badge">required</small>
extra_id <small>string</small> | Additional ID that will help to identify this customer. If this argument is omitted, extra_id is not changed.
email <small>string</small> | The email of the customer, unique. 
name <small>string</small> | The name of the customer.

### Returns

Returns a customer object if the call succeeded. If the customer ID does not exist, returns <a href=#errors>an error</a>.  

## List all customers

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/customers?limit=2  \
-u YourTokenHere:
```

> Example Response

```json
{
    "object": "list",
    "has_more": false,
    "data": 
    [
        {
            "id":1340573,
            "stripe_id":"cus_1234ABCD",
            "extra_id":"Team X",
            "email":"tester@example.com",
            "name":"John Doe",
            "total_contract_value":629100,
            "current_mrr":69900,
            "current_subscription_count":1,
            "currency":"usd",
            "country": "US", 
            "state": "OH"
        },
        {
            "id":1340574,
            "stripe_id":"cus_1234ABCE",
            "extra_id":"Team Y",
            "email":"tester2@example.com",
            "name":"Jane Doe",
            "total_contract_value":629100,
            "current_mrr":69900,
            "current_subscription_count":1,
            "currency":"usd",
            "country": "US", 
            "state": "OH"    
        }
    ]
 }
```
### HTTP Request

`GET https://api.firstofficer.io/v2/customers`

Returns a list of your customers

### Arguments

Argument | Description
--------- | -------
limit <small>optional integer<br>default is 10</small> | A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
starting_after <small>optional, <br>customer's id </small> | A cursor to use in pagination. If there are more plans than can be returned in a single call, you can use <br><code>starting_after=id</code> <br>to retrieve the next page of customers. Id would be the id of the last customer returned in your previous request.

### Returns

An array of customers in the data property. Limit the number of customers returned in a single call by using limit argument. 
Paginate through the customers by using starting_after argument. 

This request should never return an error. If no more customers are available, an empty array is returned in data property.