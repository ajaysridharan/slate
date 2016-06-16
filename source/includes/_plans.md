# Plans

Plans contains the information for creating subscriptions. Plans API allows you to create and retrieve plans.
 
## The plan object
 
 > Example Response
 
 ```json
 {
     "id":1340573,
     
 }
 ```
 
 ### Attributes
 
 Attribute | Description
 --------- | -------
 plan_id <small>string</small> | Plan's unique ID. If plan exists in Stripe, Stripe id is returned
 stripe_id <small>string</small> | Customer's ID in Stripe
 
 ## Create a plan
 
 > Example Request
 
 ```ruby
 
 ```
 
 
 ```shell
 curl https://api.firstofficer.io/v2/plans \
    -u YourTokenHere: \
    -d amount=2000 \
    -d interval=month \
    -d name="Amazing Gold Plan" \
    -d currency=eur \
    -d id=gold
 
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
 
 Creates a plan.
 
 ### Arguments
 
 Argument | Description
 --------- | -------
 id <small>string</small> |   <small class="req-badge">required</small>
 amount <small>integer</small> | A positive integer in the smallest currency unit (e.g., 100 cents to charge $1.00) representing the total amount before discounts.  <small class="req-badge">required</small>
 currency <small>string</small> | Currency of the invoice, e.g. 'usd', 'eur'.  <small class="req-badge">required</small>
 interval <small>string</small> | <small class="req-badge">required</small>
 name <small>string</small> | <small class="req-badge">required</small>
 interval_count <small>integer,default is 1</small> | The number of intervals between each subscription billing. For example, interval=month and interval_count=3 means that subscription length is 3 months.
 
 ### Returns
 
 Returns the invoice object if call succeeds.
 
 Returns an error if:
 
 * the customer or plan ID provided is invalid
 
 * the date paid is invalid