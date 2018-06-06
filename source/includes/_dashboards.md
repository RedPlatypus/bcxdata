# Dashboards

```javascript
// get dashboards 
let data = requester.get("https://api.bcxdata.com/v1/dashboards");

```

> The above command returns JSON structured like this:

```json
{
    "dashboards":[
        {
           "dashboard_id":"",
           "dashboardName":"",
        },
        ...
    ]
}
```

Returns status and information about dashboards.

## DB Endpoints

Endpoint | Return
----- | ------
`/dashboards` | Returns the home page information.
`/dashboards/:bcx_symbol` | Returns the dashboard for a specific coin.


## DB Passed Parameters

Variable | Default | Type | Description
-------- | ------- | ---- | -----------
`dashboard_id` | `null` | `String` | The dashboard you wish to find


## DB Returned Data

what will we return for JSON format? What does each category mean?

Variable | Type | Description
--------- | --- | ---------
`dashboardName` | `string` | Name of the dashboard
`dashboard_id` | `string` | BCXData's id for the dashboard
`volume` | `string` | 24h trading volume of the market
`quote` | `string` | BCX Data currency ID of the asset used to quote a price
`timeStamp` | `string` | Timestamp of the quoted volume. TODO: decide what timestamp to use.