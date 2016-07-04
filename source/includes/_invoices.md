# Invoices

Invoices API allows you to import non-Stripe payments to FirstOfficer. 

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
   
### Attributes

Attribute | Description
--------- | -------
id <small>integer</small> | Unique identifier.
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

## Import an invoice

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/invoices \
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
At the moment you can only create invoices to existing plans and customers. That'll change when the customer and plan api points are ready.
</aside>

### HTTP Request

`POST https://api.firstofficer.io/v2/invoices`

Creates an invoice. 

You can view the imported invoices at [https://www.firstofficer.io/import_payments](https://www.firstofficer.io/import_payments) and see when they get processed.
That's also where you can delete individual invoices if needed.

### Arguments

Argument | Description
--------- | -------
customer <small>string</small> | The FirstOfficer ID of the customer. Stripe ID or email will also work, but are deprecated and will be removed in V3. <small class="req-badge">required</small> 
plan <small>string</small> | The ID of the plan. If plan is omitted, payment is booked only into revenue, not to MRR. 
amount <small>integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the total amount before discounts. Optional when plan given.
date_paid <small>ISO datetime</small> | ISO datetime representing when the payment was received. If date_paid is omitted, current time is used.
discount <small>integer</small> | A positive integer representing the discount. Invoiced amount will be amount - discount.
id <small>integer</small> | Unique identifier to prevent the same invoice from being imported twice. If id is omitted, it will be generated from date and customer id.
quantity <small>integer</small> | The quantity of the seats used. If your plan is €10/user/month, you could pass 5 as the quantity to create an invoice of €50 (5 x €10).
period_start <small>ISO datetime</small> | ISO datetime representing the subscription period start time. If period_start is omitted, date_paid is used.
currency <small>string</small> | Currency of the invoice, e.g. 'usd', 'eur'.
description <small>string</small> | Free text describing what got invoiced.

### Returns

Returns the invoice object if call succeeds.

Returns an error if:

* the customer or plan ID provided is invalid

* the date paid is invalid


