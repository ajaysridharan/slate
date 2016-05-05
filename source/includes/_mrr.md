# MRR

MRR API allows you to retrieve Monthly Recurring Revenue. 

## The MRR object

> Example Response

```json
{
    "object": "mrr",
    "month":"2016-04-01",
    "mrr":15317,
    "subscriptions":20,
    "change_in_mrr":0,
    "upgrade_mrr":0,
    "downgrade_mrr":0,
    "new_mrr":0,
    "new_customers":0,
    "lost_mrr":0,
    "lost_customers":0,
    "currency":"usd",
    "waiting_mrr":1617110,
    "waiting_subscriptions":204}
}
```

### Attributes

Attribute | Description
--------- | -------
month | The first day of the returned month, ISO format string
mrr | MRR, integer. When retrieved for current month, includes only MRR charged by current date and MRR from pre-paid annual subscriptions. The rest will be found in 'waiting_mrr'.
subscriptions | Subscription count, integer. When retrieved for current month, includes only subscriptions charged by current date and old annual subscriptions. The rest will be found in 'waiting_subscriptions'.
change_in_mrr | Overall change in MRR due to upgrades and downgrades, integer
upgrade_mrr | MRR from upgrades to higher priced plans and increased seats, integer. Change from monthly to annual plan is counted as an upgrade.
downgrade_mrr | MRR from downgrades to lower priced plans and decreased seats, integer 
new_mrr | MRR from new and returning customers, integer
new_customers | Number of new and returning customers, integer
lost_mrr | MRR from customers who stopped paying, integer 
lost_customers | Number of customers who stopped paying, integer
currency | Currency of this object, e.g. "usd", "eur", string.
waiting_mrr | Expected MRR from subscriptions to be charged, integer. Only shown for current month. The MRR already charged can be found in mrr attribute.
waiting_subscriptions | Expected subscriptions to be charged, integer. Only shown for current month.

## Retrieve all MRRs

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/mrr  \
-u YourTokenHere:
```

> Example Response

```json
{
    "data": [
        {
            "object": "mrr",
            "month":"2014-05-01",
            "mrr":33700,
            "subscriptions":3,
            "expansion_mrr":0,
            "contraction_mrr":0,
            "upgrade_mrr":0,
            "downgrade_mrr":0,
            "new_mrr":33700,
            "new_customers":3,
            "lost_mrr":0,
            "lost_customers":0,
            "currency":"usd"
        },
        {
            "object": "mrr",
            "month":"2014-06-01",
            "mrr":61400,
            "subscriptions":7,
            "expansion_mrr":0,
            "contraction_mrr":0,
            "upgrade_mrr":0,
            "downgrade_mrr":0,
            "new_mrr":25700,
            "new_customers":4,
            "lost_mrr":0,
            "lost_customers":0,
            "currency":"usd"
        }
    ]
}
```
### HTTP Request

`GET https://api.firstofficer.io/v2/mrr`

Retrieves the MRR from all time.

### Returns

Returns a JSON array of MRR objects if the call succeeded. 

## Retrieve Month's Recurring Revenue

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/mrr/2016-02-01  \
-u YourTokenHere:
```

> Example Response

```json
{
    "object": "mrr",
    "month":"2016-04-01",
    "mrr":15317,
    "subscriptions":20,
    "change_in_mrr":0,
    "upgrade_mrr":0,
    "downgrade_mrr":0,
    "new_mrr":0,
    "new_customers":0,
    "lost_mrr":0,
    "lost_customers":0,
    "currency":"usd",
    "waiting_mrr":1617110,
    "waiting_subscriptions":204}
}
```
### HTTP Request

`GET https://api.firstofficer.io/v2/mrr/<month in ISO format>`

Retrieves the MRR from a single month

### Arguments

Argument | Description
--------- | -------
month <small>ISO date</small> | ISO format date, e.g. 2016-04-01. Giving any date from the wanted month is OK and will return the MRR, but we recommend using the first day of the month. <small class="req-badge">required</small>

### Returns

Returns a MRR object if the call succeeded. If the month does not have any data, returns and empty JSON.
