# MRR by Plan

MRR by Plan API allows you to retrieve Monthly Recurring Revenue broken down by plans.

## The MRR by Plan object

> Example Response

```json
{
	"month": "2019-02-01T00:00:00.000Z",
	"total_mrr": 24900,
	"total_customers": 1,
	"end_of_term_customers": 1,
	"lost_customers": 0,
	"end_of_term_mrr": 24900,
	"lost_mrr": 0,
	"new_mrr": 0,
	"beginning_mrr": 0,
	"upgrade_mrr": 0,
	"downgrade_mrr": 0,
	"moved_in_mrr": 0,
	"moved_out_mrr": 0,
	"waiting_mrr": 0,
	"plan_name": null,
	"plan_eid": "business monthly"
}
```

### Attributes

Attribute | Description
--------- | -------
month <small>ISO date string</small> | The first day of the returned month
total_mrr <small>integer</small> | MRR. When retrieved for current month, includes only MRR charged by current date and MRR from 
total_customers <small>integer</small> | Total number of customers for the plan for the given period
end_of_term_customers <small>integer</small> | 
lost_customers <small>integer</small> | Number of customers who stopped paying
end_of_term_mrr <small>integer</small> | 
lost_mrr <small>integer</small> | MRR from customers who stopped paying 
new_mrr <small>integer</small> | MRR from new and returning customers
beginning_mrr <small>integer</small> | 
upgrade_mrr <small>integer</small> | MRR from upgrades to higher priced plans and increased seats. Change from monthly to annual 
downgrade_mrr <small>integer</small> | MRR from downgrades to lower priced plans and decreased seats 
moved_in_mrr <small>integer</small> | 
moved_out_mrr <small>integer</small>| 
waiting_mrr <small>integer</small> | Expected MRR from subscriptions to be charged. Only shown for current month. The MRR already 
plan_name <small>string</small>  | Plan name
plan_eid <small>string</small> | Plan eid (as set in Stripe). (non-null)

## Retrieve Monthly RR by Plans

> Example Request

```ruby

```


```shell
curl https://api.firstofficer.io/v2/mrr_by_plan?start_month=2019-01-01&end_month=2019-02-01  \
-u YourTokenHere:
```

> Example Response

```json
[{
	"month": "2019-02-01T00:00:00.000Z",
	"total_mrr": 24900,
	"total_customers": 1,
	"end_of_term_customers": 1,
	"lost_customers": 0,
	"end_of_term_mrr": 24900,
	"lost_mrr": 0,
	"new_mrr": 0,
	"beginning_mrr": 0,
	"upgrade_mrr": 0,
	"downgrade_mrr": 0,
	"moved_in_mrr": 0,
	"moved_out_mrr": 0,
	"waiting_mrr": 0,
	"plan_name": null,
	"plan_eid": "business monthly"
}, {
	"month": "2019-02-01T00:00:00.000Z",
	"total_mrr": 24950,
	"total_customers": 1,
	"end_of_term_customers": 1,
	"lost_customers": 0,
	"end_of_term_mrr": 24950,
	"lost_mrr": 0,
	"new_mrr": 0,
	"beginning_mrr": 0,
	"upgrade_mrr": 0,
	"downgrade_mrr": 0,
	"moved_in_mrr": 0,
	"moved_out_mrr": 0,
	"waiting_mrr": 0,
	"plan_name": null,
	"plan_eid": "enterprise_2_monthly_1501"
}]
```

### HTTP Request

`GET https://api.firstofficer.io/v2/mrr_by_plan?start_month=2019-01-01&end_month=2019-02-01`

### Arguments

Argument | Description
--------- | -------
start_month <small>string</small> | The starting month from which MRR data needs to be returned grouped by plan.
end_month <small>string</small> | The ending month (inclusive) till which MRR data needs to be returned grouped by plan.

### Returns

Returns a list of MRR objects grouped by plans and aggregated on a monthly basis.