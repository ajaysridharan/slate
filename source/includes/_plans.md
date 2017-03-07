# Plans

Plans contains the information for creating subscriptions. Plans API allows you to create and retrieve plans.

FirstOfficer cannot change the data in Stripe, so any changes done here will not affect customer billing.
 
## The plan object
 
 > Example Response
 
 ```json
  {
    "id": "test",
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
curl https://api.firstofficer.io/v2/plans/test  \
-u YourTokenHere:
```

> Example Response

```json
{
   "id": "test",
   "object": "plan",
   "amount": 0,
   "currency": "usd",
   "interval": "month",
   "interval_count": 1,
   "name": "Test Plan"
 }
```
### HTTP Request

`GET https://api.firstofficer.io/v2/plans/<id>`

Retrieves the details of an existing plan.

### Arguments

Argument | Description
--------- | -------
id <small>string</small> | The ID of the plan to be retrieved. If the plan is in Stripe, this is the Stripe ID. <small class="req-badge">required</small> 

### Returns

Returns a plan object if the call succeeded. If the plan ID does not exist, returns <a href=#errors>an error</a>.

## List all plans

You can also view a list of your plans at [https://www.firstofficer.io/plans](https://www.firstofficer.io/plans).

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/plans?limit=2  \
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
            "id": "test",
            "object": "plan",
            "amount": 0,
            "currency": "usd",
            "interval": "month",
            "interval_count": 1,
            "name": "Test Plan"
        },
        {
            "id": "test_2",
            "object": "plan",
            "amount": 0,
            "currency": "usd",
            "interval": "month",
            "interval_count": 1,
            "name": "Test Plan 2"    
        }
    ]
 }
```
### HTTP Request

`GET https://api.firstofficer.io/v2/plans`

Returns a list of your plans.

### Arguments

Argument | Description
--------- | -------
limit <small>optional integer<br>default is 10</small> | A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
starting_after <small>optional, <br>plan's id </small> | A cursor to use in pagination. If there are more plans than can be returned in a single call, you can use <br><code>starting_after=id</code> <br>to retrieve the next page of plans. Id would be the id of the last plan returned in your previous request.

### Returns

An array of plans in the data property. Limit the number of plans returned in a single call by using limit argument. 
Paginate through the plans by using starting_after argument. 

This request should never return an error. If no more plans are available, an empty array is returned in data property.