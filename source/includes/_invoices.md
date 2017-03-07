# Invoices

Invoices API allows you to import non-Stripe payments to FirstOfficer. 

FirstOfficer cannot change the data in Stripe, so any changes done here will not affect customer billing.

Imported invoices will be processed during the next metrics recalculation, usually within one hour. 
This means your metrics will not update right away after you've imported the invoice. 

You will be able to see the imported invoice in customer's page, which you can access by searching the customer:
 
 `https://www.firstofficer.io/customers?stripe_id=cus_ABCD`
 
 or
 
 `https://www.firstofficer.io/customers?email=partialemailhere@gmail.com`

## The invoice object

> Example Response

```json
{
    "id": "1462443986",
    "subscription_id": "sub_man_2313372_1462443986",
    "object": "invoice",
    "amount_paid": 2900,
    "discount": 0,
    "amount": 2900,
    "currency": "usd",
    "customer": "cus_ABCD",
    "plan": "hobby_monthly",
    "date_paid": "2016-05-05T10:26:26+00:00",
    "date": "2016-05-05T10:26:26+00:00",
    "quantity": 1,
    "period_start": "2016-05-05T10:26:26+00:00",
    "period_end": "2016-06-05T10:26:26+00:00",
    "description": ""
}
```
   
### Attributes

Attribute | Description
--------- | -------
id <small>integer</small> | Unique identifier.
subscription_id <small>string</small> | Identifier of the subscription.
object <small>string</small> | Object type, value is "invoice".
amount_paid <small>integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the invoiced amount.
discount <small>integer</small> | A positive integer representing the discount. Invoice total will be amount - discount.
amount <small>integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the total amount before discounts.
currency <small>string</small> | Currency of the invoice, e.g. 'usd', 'eur'.
customer <small>string</small> | The ID of the customer. 
plan <small>string</small> | The ID of the plan. If plan is omitted, payment is booked only into revenue, not to MRR. 
date_paid <small>ISO datetime</small> | ISO datetime representing when the payment was received.
date <small>ISO datetime</small> | ISO datetime representing when invoice was created.
quantity <small>integer</small> | The quantity of the seats used. 
period_start <small>ISO datetime</small> | ISO datetime representing the subscription period start time. 
period_end <small>ISO datetime</small> | ISO datetime representing the subscription period end time.
description <small>string</small> |

## Create an invoice

> Example Request

```ruby

```


```shell
curl -X POST https://api.firstofficer.io/v2/invoices \
   -u YourTokenHere: \
   -d customer=cus_ABCD \
   -d plan=hobby_monthly \
   -d amount=4000 

```

> Example Response

```json
{
    "id": "sub_man_2313372_1462443986",
    "object": "invoice",
    "amount_paid": 2900,
    "discount": 0,
    "amount": 2900,
    "currency": "usd",
    "customer": "cus_ABCD",
    "plan": "hobby_monthly",
    "date_paid": "2016-05-05T10:26:26+00:00",
    "date": "2016-05-05T10:26:26+00:00",
    "quantity": 1,
    "period_start": "2016-05-05T10:26:26+00:00",
    "period_end": "2016-06-05T10:26:26+00:00",
    "description": ""
}   
```


<aside class="notice">
It is important to import invoices to a plan with the same interval. Do not import monthly subscriptions to an annual plan or vice versa.
</aside>

### HTTP Request

`POST https://api.firstofficer.io/v2/invoices`

Creates an invoice for metrics calculation. 

You can view the imported invoices at [https://www.firstofficer.io/import_payments](https://www.firstofficer.io/import_payments) and see when they get processed.
That's also where you can delete individual invoices if needed.

Argument "plan" defines whether the invoice will be handled as a subscription or as a single purchase. If plan is present, it's a subscription. If plan is omitted, it's a one-time payment.

### Arguments

Argument | Description
--------- | -------
customer <small>string</small> | The FirstOfficer ID of the customer. Stripe ID or email will also work, but are deprecated and will be removed in V3. <small class="req-badge">required</small> 
plan <small>string</small> | The ID of the plan. If plan is omitted, payment is booked only into revenue, not to MRR. 
amount <small>integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the total amount before discounts. Optional when plan given.
date_paid <small>ISO datetime</small> | ISO datetime representing when the payment was received. If date_paid is omitted, current time is used.
date <small>ISO datetime</small> | ISO datetime representing when the invoice was created. If date is omitted, date_paid is used.
discount <small>integer</small> | A positive integer representing the discount. Invoiced amount will be amount - discount.
id <small>integer</small> | Unique identifier to prevent the same invoice from being imported twice. If id is omitted, it will be generated.
subscription_id <small>string</small> | Use this to continue or upgrade existing subscription or to add quantities to it. 
quantity <small>integer</small> | The quantity of the seats used. If your plan is €10/user/month, you could pass 5 as the quantity to create an invoice of €50 (5 x €10).
period_start <small>ISO datetime</small> | ISO datetime representing the subscription period start time. If period_start is omitted, date is used.
period_end <small>ISO datetime</small> | ISO datetime representing the subscription period end time. If period_end is omitted and plan is given, period_end is calculated using the Plan's interval.
currency <small>string</small> | Currency of the invoice, e.g. 'usd', 'eur'.
description <small>string</small> | Free text describing what got invoiced.

### Returns

Returns the invoice object if call succeeds.

Returns an error if:

* the customer or plan ID provided is invalid

* the date paid is invalid

## Retrieve an invoice

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/invoices/in_123456 \
   -u YourTokenHere: 

```

> Example Response

```json
{
    "id": "in_123456",
    "object": "invoice",
    "amount_paid": 2900,
    "discount": 0,
    "amount": 2900,
    "currency": "usd",
    "customer": "cus_ABCD",
    "plan": "hobby_monthly",
    "date_paid": "2016-05-05T10:26:26+00:00",
    "date": "2016-05-05T10:26:26+00:00",
    "quantity": 1,
    "period_start": "2016-05-05T10:26:26+00:00",
    "period_end": "2016-06-05T10:26:26+00:00",
    "description": ""
}   
```

### HTTP Request

`GET https://api.firstofficer.io/v2/invoices/<id>`

Retrieves the details of an existing invoice. Only returns invoices created through this API. Retrieve Stripe invoices through [the invoices endpoint in Stripe API](https://stripe.com/docs/api#invoices).

### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The ID of the invoice to be retrieved. <small class="req-badge">required</small> 

### Returns

Returns an invoice object if the call succeeded. Only one invoice is returned. 

If the invoice ID does not exist, returns <a href=#errors>an error</a>.

## Delete an invoice

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/invoices/in_123456 \
   -u YourTokenHere: \
    -X DELETE

```

> Example Response

```json
{
  "deleted": true,
  "id": "in_123456"
}
```

### HTTP Request

`DELETE https://api.firstofficer.io/v2/invoices/<id>`

Permanently deletes an invoice. It cannot be undone.

<aside class="notice">
Changes in invoices are processed during the next metrics recalculation, usually within one hour. 
This means your metrics will not update right away after you've deleted the invoice.
</aside>


### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The ID of the invoice to be deleted. <small class="req-badge">required</small> 

### Returns

Returns an object with a deleted parameter on success. If the invoice ID does not exist, this call returns an error.

## List all invoices

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/invoices?limit=2  \
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
            "id": "in_1",
            "object": "invoice",
            "amount_paid": 2900,
            "discount": 0,
            "amount": 2900,
            "currency": "usd",
            "customer": "cus_A",
            "plan": "hobby_monthly",
            "date_paid": "2016-05-05T10:26:26+00:00",
            "date": "2016-05-05T10:26:26+00:00",
            "quantity": 1,
            "period_start": "2016-05-05T10:26:26+00:00",
            "period_end": "2016-06-05T10:26:26+00:00",
            "description": ""
        },
        {
            "id": "in_2",
            "object": "invoice",
            "amount_paid": 2900,
            "discount": 0,
            "amount": 2900,
            "currency": "usd",
            "customer": "cus_B",
            "plan": "hobby_monthly",
            "date_paid": "2016-05-05T10:26:26+00:00",
            "date": "2016-05-05T10:26:26+00:00",
            "quantity": 1,
            "period_start": "2016-05-05T10:26:26+00:00",
            "period_end": "2016-06-05T10:26:26+00:00",
            "description": ""
        }
    ]
 }
```
### HTTP Request

`GET https://api.firstofficer.io/v2/invoices`

Returns a list of your invoices. Only returns invoices created through this API. List Stripe invoices through [the invoices endpoint in Stripe API](https://stripe.com/docs/api#invoices).

### Arguments

Argument | Description
--------- | -------
limit <small>optional integer<br>default is 10</small> | A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
starting_after <small>optional, <br>plan's id </small> | A cursor to use in pagination. If there are more items than can be returned in a single call, you can use <br><code>starting_after=id</code> <br>to retrieve the next page of items. Id would be the id of the last item returned in your previous request.

### Returns

An array of invoices in the data property. Limit the number of invoices returned in a single call by using limit argument. 
Paginate through the invoices by using starting_after argument. 

This request should never return an error. If no more invoices are available, an empty array is returned in data property.