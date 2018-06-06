Copy below this line & replace the templates with the plural, replace template with the singlar.
---

# Templates

```javascript
// get templates 
let data = requester.get("https://api.bcxdata.com/v1/templates");

```

```python
# get templates 
let data = requester.get("https://api.bcxdata.com/v1/templates");

```

> The above command returns JSON structured like this:

```json
{
    "templates":[
        {
           "template_id":"",
           "templateName":"",
        },
        ...
    ]
}
```

Returns status and information about templates.

## ABBREVIATION Endpoints

Endpoint | Return
----- | ------
`/templates` | Returns a list of templates.
`/templates/:template_id` | Returns a particular template.


## ABBREVIATION Passed Parameters

Variable | Default | Type | Description
-------- | ------- | ---- | -----------
`template_id` | `null` | `String` | The template you wish to find


## ABBREVIATION Returned Data

what will we return for JSON format? What does each category mean?

Variable | Type | Description
--------- | --- | ---------
`templateName` | `string` | Name of the template
`template_id` | `string` | BCXData's id for the template
`volume` | `string` | 24h trading volume of the market
`quote` | `string` | BCX Data currency id of the asset used to quote a price
`timeStamp` | `string` | Timestamp of the quoted volume. TODO: decide what timestamp to use.