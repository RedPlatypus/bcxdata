# Developer

```javascript
// using the node module
const BCX = require('BCXDATA');

let api = BCX.authorize('xxx.api-key');
let developers = api.developers.get();

// plain javascript
let data = req.get("https://api.bcxdata.com/v1/developers")

```

```python
import developer

api = developer.authorize('xxx.api-key')
api.developers.get()
```

> The above command returns JSON structured like this:

```json
"data":[
  {
    "coinId":"",
    "":""
  }
]
```

This endpoint retrieves all developer information we have on the particular coin. Developer data is important in guaging how much technical support the community is having.

## DEV Endpoints

## DEV Passed Parameters

## DEV CoinId

## DEV Returned Data

