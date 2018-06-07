# Exchange Candles

Returns candle data for the specified coin on a particular exchange.

## EC Endpoints

```javascript
// get exchange 
let data = requester.get("https://api.bcxdata.com/v1/exchange_candles/bfx/btceth");

```

> The above command returns JSON structured like this:

```json
{
    // Return 30 candles with 1d frequency
    "data":[
        {
            "symbol":"btceth",
            "name":"Bitcoin Ethereum",
            "time": "2017-12-13T20:31:24.737Z",
            "open":12.00,
            "high":14.00,
            "low":10.00,
            "close":11.00,
            "volume":3783.00,
            "last_price":7000
        },
        {
            "symbol":"btceth",
            "name":"Bitcoin Ethereum",
            "time": "2017-12-14T20:31:24.737Z",
            "open":11.00,
            "high":25.00,
            "low":11.00,
            "close":20.00,
            "volume":3783.00,
            "last_price":7000
        },
        {
            "symbol":"btceth",
            "name":"Bitcoin Ethereum",
            "time": "2017-12-15T20:31:24.737Z",
            "open":20.00,
            "high":24.00,
            "low":19.00,
            "close":20.00,
            "volume":3783.00,
            "last_price":7000
        },
        //... 3 days of data provided, add another 27 objects.
    ]
}
```


### v1 endpoints

Endpoint | Return
----- | ------
`/exchanges` | Returns a list of supported exchanges & it's data. See [exchanges](#exchanges) for more information
`/exchange_candles/:exchange_id/:bcx_symbol` | Returns a symbol in relation to the exchange base currency. Typically over `USD` 
`/exchange_candles/:exchange_id/:bcx_symbol/:frequency` | returns the max interval of data possible for a specified frequency size. See heading "Interval" for frequency to data size relationship.
`/exchange_candles/:exchange_id/:bcx_symbol/:frequency/`<br>`:interval?start<timestamp>&end<timestamp>` | Returns the interval of data at the frequency for the currency you specify.


> Example error if `end` is past now:
> Up for **debate**. Do we return error only, or do we return data in addition to the error for the start to end dates we have. 

```json
{
    "errors":[
        {
            "number":   404,
            "message":  "The data requested was more than what is available. Check your start and end dates."
        }
    ],
    "data":[
        {
            "symbol":"btceth",
            "name":"Bitcoin Ethereum",
            "time": "2 days ago, requested date",
            "open":12.00,
            "high":14.00,
            "low":10.00,
            "close":11.00,
            "volume":3783.00,
            "last_price":7000
        },
        {
            "symbol":"btceth",
            "name":"Bitcoin Ethereum",
            "time": "yesterday",
            "open":11.00,
            "high":25.00,
            "low":11.00,
            "close":20.00,
            "volume":3783.00,
            "last_price":7000
        },
        {
            "symbol":"btceth",
            "name":"Bitcoin Ethereum",
            "time": "today",
            "open":20.00,
            "high":24.00,
            "low":19.00,
            "close":20.00,
            "volume":3783.00,
            "last_price":7000
        }
        // 3 days of data provided. User might have requested data from 2 days ago, 
        // until 30 days into the future. In which case we should only return 3 days 
        // of data and an errors array letting them know we don't have that data.
    ]
}
```

## EC Passed Parameters

Variable | Default | Type | Description
-------- | ------- | ---- | -----------
`exchange_id` | `null` | `String` | The exchange you wish to find. Return error if `null`
`bcx_symbol` | `null` | `String` | The BCX Data symbol used to identify a coin. [See Coins](#Coins) for endpoints to get `bcx_symbol`s
`frequency` | `1d`   | `String` | The frequency at which the candle data will be amalgamated over `1d`, `1h`, `30m`, `5m`, `1m`
`start` | `30 days before today` | `DateTime` | The day at which you want the data to begin. If not passed in, we will get data from 1 month ago.
`end` | `today` | `DateTime` | The day at which the data ends. It needs to be greater than the start date. If it is a time past now, we return an error along with the requested data.




## EC Currency

Candles returns the data by default in relation to a `base_currency` typically **USD**. To request a pair, conjoin two symbols. Returned data is amalgamated over all exchanges we currently track. If the pair is not available on that exchange, an error will be returned.

### EC Symbols

> Example Requests

```javascript
// These should default to BTCUSD & XRMUSD respectively
let data = req.get("https://api.bcxdata.com/v1/exchange_candles/bfx/btc");
let data = req.get("https://api.bcxdata.com/v1/exchange_candles/bfx/xrm");

// Since Exchange Candles don't need to be amalgamated. We can request a specific pair from the exchange.
// These should request the pair ETHBTC & XRMBCC respectively from the bitfinex market
let data = req.get("https://api.bcxdata.com/v1/exchange_candles/bfx/ethbtc");
let data = req.get("https://api.bcxdata.com/v1/exchange_candles/bfx/xrmbcc");

```

Symbol | Ticker
------ | ------
Bitcoin | btc
Bitcoin Cash | bch
BitConnect | bcc
Dash | dash
Ethereum | eth
Ethereum Classic | etc
Litecoin | ltc
Monero | xmr
NEO | neo
Nxt | nxt
Ripple | xrp
Stellar | xlm
Zcash | zec

## EC Frequency

> Warning

```javascript
  let requestedData = req.get("https://api.bcxdata.com/v1/exchange_candles/bfx/btc/1h/interval?start=2018-05-13:09:00:00:000&end=2017-05-13:09:00:00:000");
```

> The above request returns this error

```json
{
    "errors":[
        {
            "number":405,
            "message":"The interval was too small for the requested time period."
        }
    ]
}
```

Candles returns the following date intervals based on size requests. These are also the maximum frequency a user can request for a given time period. You can always request a smaller frequency example: 30 min for anything less than 14 days, but you can not request 30 min frequency for a 14 day or greater interval.

frequency | max_return_data
---- | -----
`1d` | Inception
`1h` | 30 days 
`30m`| 14 days 
`5m` | 3 days 
`1m` | 24 hours


<aside class="notice">
    Requesting <code>https://api.bcxdata.com/v1/exchange_candles/krak/eth/1d</code> returns the candle data since inception.<br>
    Requesting <code>https://api.bcxdata.com/v1/exchange_candles/krak/eth/1h</code> returns only the last 30 days of data available.
</aside>

<aside class="warning">
    Requesting a time period longer than the frequencies time_period specified returns a <code>405</code> error.
</aside>




## EC Returned Data

Variable | Type | Description
-------- | ---- | -----------
`symbol` | `string` | The traded bair conjoined. "btcusd"
`open` | `number` | The opening price at the begining of the period
`high` | `number` | The high of the price for the period
`low` | `number` | The low of the price for the period
`close` | `number` | The close at the end of the period
`volume` | `number` | The volume during the period
`last_price` | `number` | The last price before moving to the next period