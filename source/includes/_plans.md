# Plans

Plans contains the information for creating subscriptions. Plans API allows you to create and retrieve plans.
 
Until the point for retrieval is available, you can view your plans at [https://www.firstofficer.io/plans](https://www.firstofficer.io/plans).
 
## The plan object
 
 > Example Response
 
 ```json
  {
    "id": "test",
    "fo_id": "1",
    "object": "plan",
    "amount": 0,
    "currency": "usd",
    "interval": "month",
    "interval_count": 1,
    "name": "Test Plan"
  }
 ```
 
### Attributes
 
 Attribute | Description
 --------- | -------
 id <small>string</small> | Plan's unique ID. If plan exists in Stripe, Stripe id is returned.
 fo_id <small>integer</small> | Plan's unique ID in FirstOfficer. 
 object <small>string</small> | Value is "plan".
 amount <small>positive integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the total amount before discounts. 
 name <small>string</small> | Display name of the plan.
 interval <small>string</small> | The billing frequency. Either "day", "week", "month" or "year".
 interval_count <small>integer</small> | The number of intervals between each subscription billing. For example, interval=month and interval_count=3 means that subscription length is 3 months.
 currency <small>string</small> | 3-letter ISO code for currency.
 
 
## Create a plan
 
 > Example Request
 
 ```ruby
 
 ```
 
 
 ```shell
 curl -X POST https://api.firstofficer.io/v2/plans \
    -u YourTokenHere: \
    -d amount=2000 \
    -d interval=month \
    -d name="The Plan" \
    -d currency=eur \
    -d id="the-plan"
 
 ```
 
 > Example Response
 
 ```json
 {
   "id": "test",
   "fo_id": "1",
   "object": "plan",
   "amount": 0,
   "currency": "usd",
   "interval": "month",
   "interval_count": 1,
   "name": "Test Plan"
 }
 ```
 
### HTTP Request
 
 `POST https://api.firstofficer.io/v2/plans`
 
 Creates a plan.
 
### Arguments
 
 Argument | Description
 --------- | -------
 id <small>string</small> |  <small class="req-badge">required</small>
 amount <small>positive integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the total amount before discounts.  <small class="req-badge">required</small>
 name <small>string</small> | Display name of the plan. <small class="req-badge">required</small>
 interval <small>string, default is "month"</small> | The billing frequency. Either "day", "week", "month" or "year".
 interval_count <small>integer,default is 1</small> | The number of intervals between each subscription billing. For example, interval=month and interval_count=3 means that subscription length is 3 months.
 currency <small>string, default is "usd"</small> | 3-letter ISO code for currency. 
 
### Returns
 
 Returns the created plan object if call succeeds. If the plan ID does already exists, returns <a href=#errors>an error</a>.
 
## Retrieve a plan

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/plans/1  \
-u YourTokenHere:
```

> Example Response

```json
{
   "id": "test",
   "fo_id": "1",
   "object": "plan",
   "amount": 0,
   "currency": "usd",
   "interval": "month",
   "interval_count": 1,
   "name": "Test Plan"
 }
```
### HTTP Request

`GET https://api.firstofficer.io/v2/plans/<fo_id>`

Retrieves the details of an existing plan.

### Arguments

Argument | Description
--------- | -------
fo_id <small>integer</small> | The FirstOfficer ID of the plan to be retrieved. <small class="req-badge">required</small> 

### Returns

Returns a plan object if the call succeeded. If the plan ID does not exist, returns <a href=#errors>an error</a>.
