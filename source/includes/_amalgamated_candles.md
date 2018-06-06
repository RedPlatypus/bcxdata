# Amalgamated Candles

Return a volume weighted average accross all exchanges we track for the selected currency or currencies.

Authentication | `None`

<aside class="notice">
<strong>TODO:</strong>
<ol>
    <li>specify what we are storing the date object as &amp; in what format.</li>
</ol>
</aside>

## AC Endpoints

```javascript
// get amalgamated candles 
// sampling defaults of 1 day frequency over a 30 day time period
let data = requester.get("https://api.bcxdata.com/v1/candles/btc");
console.log(data)

```

> The above command returns JSON structured like this:

```json
// user requested default data 
// return 30 days of data at daily intervals
{
    "data":[
        {
            "symbol":"btcusd",
            "name":"Bitcoin United States Dollars",
            "time": "2017-12-13T20:31:24.737Z",
            "open":6500.00,
            "high":7500.00,
            "low":6400.00,
            "close":7000.00,
            "volume":92902.00,
            "last_price":7000
        },
        {
            "symbol":"btcusd",
            "name":"Bitcoin United States Dollars",
            "time": "2017-12-14T20:31:24.737Z",
            "open":7000.00,
            "high":7900.00,
            "low":6000.00,
            "close":7800.00,
            "volume":92902.00,
            "last_price":7000
        },
        {
            "symbol":"btcusd",
            "name":"Bitcoin United States Dollars",
            "time": "2017-12-15T20:31:24.737Z",
            "open":7800.00,
            "high":10291.00,
            "low":6400.00,
            "close":7238.00,
            "volume":92902.00,
            "last_price":7000
        },
        //... 3 days of data provided, add another 27 objects.
    ]
}
```


### v1 endpoints

Key | Value | Return
--- | ----- | ------
Endpoints | `/candles/:bcx_symbol` | Returns amalgamated candles for the coin over `30 days`, with a `1d` frequency
Endpoints | `/candles/:bcx_symbol/:frequency` | Returns the largest time period of possible for a specified frequency size. See [Frequency](#ac-frequency) for more information.
Endpoints | `/candles/:bcx_symbol/:frequency/`<br>`:period?start<timestamp>&end<timestamp>` | Returns the time period of data at the frequency for the `bcx_symbol` specified.


### v1 to be discussed endpoints

Key | Value | Return | Problem
--- | ----- | ------ | -------
Endpoints | `/candles` | Returns all amalgamated candles over the past `30 days`, with a `1d` frequency. | If we return all data, won't this be a costly API request as we will have to return all coin data?


## AC Passed Parameters

Variable | Default | Type | Description
-------- | ------- | ---- | -----------
`bcx_symbol` | `BTC` | `String` | The coin's symbol ID. It will be converted to `BTCUSD` on the server
`frequency` | `1d`   | `String` | The frequency at which the candle data will be amalgamated over `1d`, `1h`, `30m`, `5m`, `1m`
`start` | `Today` | `DateTime` | Defaults to today's date.
`end` | `30 days before today` | `DateTime` | Defaults to 30 days before today.


## AC Currency

Candles returns the data by default in relation to USD. To request a pair, conjoin two symbols. Returned data is amalgamated over all exchanges we currently track by volume weighted averages. For instance an exchange that only trades 10% relative to another exchange, only accounts for 10% of the actual price of the amalgamated candle.

### AC Currency Symbols

> Example Requests

```javascript
// Pair is assumed to be USD
let data_btc = req.get("https://api.bcxdata.com/v1/candles/btc");
let data_xrm = req.get("https://api.bcxdata.com/v1/candles/xrm");

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

## AC Frequency

> Warning

```javascript
  let requestedData = req.get("https://api.bcxdata.com/v1/candles/btc/1h/period?start=2018-05-13:09:00:00:000&end=2017-05-13:09:00:00:000");
```

> The above request returns this error

```json
{
    "errors":[
        {
            "number":   405,
            "message":  "The interval was too small for the requested time period."
        }
    ]
}
```

Candles returns the following time period of data based on frequency specified:

frequency | time_period
---- | -----
`1d` | Inception
`1h` | 30 days 
`30m`| 14 days 
`5m` | 3 days 
`1m` | 24 hours

<aside class="notice">
    Requesting <code>https://api.bcxdata.com/v1/candles/btc/1d</code> returns the candle data since inception.
    Requesting <code>https://api.bcxdata.com/v1/candles/btc/1h</code> returns only the last 30 days of data available.
</aside>

<aside class="warning">
    Requesting a time period longer than the frequencies time_period specified returns a <code>405</code> error.
</aside>

## AC Returned Data

Variable | Type | Description
-------- | ---- | -----------
`symbol` | `string` | The traded bair conjoined. "btcusd"
`name` | `string` | The asset in relation to it's traded pair. "Bitcoin" over "United States Dollars"
`open` | `number` | The opening price at the begining of the period
`high` | `number` | The high of the price for the period
`low` | `number` | The low of the price for the period
`close` | `number` | The close at the end of the period
`volume` | `number` | The volume during the period
`last_price` | `number` | The last price before moving to the next period