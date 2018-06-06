# Exchanges

Returns status and information about exchanges we track. Note in early development, this data will be pulled directly from barcharts

## EXCH Endpoints

Endpoint | Return
----- | ------
`/exchanges` | Returns a list of exchanges supported by BCX Data & their current status
`/exchanges/:exchange_id` | Returns information on a single exchange

## EXCH Passed Parameters

Variable | Default | Type | Description
-------- | ------- | ---- | -----------
`exchange_id` | NA | `String` | The exchange_id, that can be received from endpoint `/exchanges`

## EXCH Returned Data

```javascript
// get exchange 
let data = requester.get("https://api.bcxdata.com/v1/exchanges");

```

> The above command returns JSON structured like this:

```json
{
    "exchanges":[ // I figure an array because if the user is calling this, they don't know which exchange they want more information on yet and probably want an easy way to loop through all exchanges.
        {
           "name":"Kraken",
           "id":"krak",
           "volume":"243921.38",
           "base_currency":"usd",
           "timeStamp":"2018-05-03T20:31:24.737Z",
           "pairs":[ // all pairs that can be traded on that exchange.
           // https://api.kraken.com/0/public/AssetPairs
           // the objects under `result`
               "bcheur",
               "bchusd",
               "bchxtbt",
               "dasheur",
               "dashusd",
               "dashxbt",
               "eoseth",
               ...
           ]
        },
        ...
    ]
}
```

what will we return for JSON format? What does each category mean?

Variable | Type | Description
--------- | --- | ---------
`name` | `string` | Name of the exchange
`id` | `string` | BCXData's id for the exchange
`volume` | `string` | 24h trading volume of the market
`base_currency` | `string` | The default currency every pair is over in this market. When requesting `https://api.bcxdata.com/v1/exchanges/bfx/candles/btc` we know that we are getting candles for `BTCUSD`. This is also the currency of `volume`.
`timeStamp` | `string` | TimeStamp of the quoted volume.
`pairs` | `array` | An array of tradeable pairs on that exchange