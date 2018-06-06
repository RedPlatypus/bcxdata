# Coins

Returns status and information about coins.

## Coin Endpoints

```javascript
// get coins 
let data = requester.get("https://api.bcxdata.com/v1/coins");

```

> The above command returns JSON structured like the data below:

```json
{
    "coins":[
        {
            "name":                 "Bitcoin",  
            "id":                   "bitcoin",  // BCX Data id for coin
            "bcx_symbol":           "btc",      // BCX Data symbol. Used when requesting indicies
            "base_currency":        "usd",      // prices not specified are in this base currency
            "circulating_supply":   17069050.0, // coins released * conversion to base currency
            "bcx_score":            78.98,      // max 100
            "bcx_recomend" :        "buy",      // our algo

            "momentum_50" :         18.2939,    // 50 day momentum
            "momentum_25" :         24.8719,    // 25 day momentum

            "tcmi" :                82.302      // TCMI max 100

            "all_time_high" :       25000.39,
            "all_time_high_date" :  "2018-01-03T11:23:59.371Z",

            "market_cap" :          77333111.34, // in base currency
            "market_share" :        33.32,       // percent
            
            "images": {
                "thumb":            "https://bcxdata.com/coins/images/thumb/bitcoin.png",
                "small":            "https://bcxdata.com/coins/images/small/bitcoin.png"
            },
            
            "symbols":[                         // exchanges we track
                {
                "exchange":"bitfinex",
                "id":"bfx",
                "symbol":"btc"
                }, {
                "exchange":"Kraken",
                "id":"krk",
                "symbol":"bit"
                },
                ...
            ],
            
            "market_data": {
                "current_price": {
                    "aud": 9882.61572096458,
                    "usd": 8789.61572096458,
                    "btc": 1,
                    "cad": 10290.03902323298,
                    "eth": 9700.03817228985,
                    "eur": 7391.10689865095,
                    "hkd": 48026.0936377929
                },
                "price_change": {
                    "24h": 42.83,
                    "48h": 39.19,
                    "7d": 140.39,
                    "30d": 193.92,
                    "1yr": 2930.32,
                    "inception": 29103920.39
                },
                "price_percent_change": {
                    "24h": 0.34,
                    "48h":31.395,
                    "7d": 35.395,
                    "30d": 121.395,
                    "1yr": 231.395,
                    "inception": 1039.59
                },
                "market_cap": {
                    "aud": 168686733397.9261,
                    "usd": 8789.61572096458,
                    "btc": 17069037,
                    "cad": 165570310464.2278,
                    "eth": 222770839.3036304,
                    "eur": 109423370141.29701,
                    "hkd": 1001761179709.8
                },
                "total_volume": {
                    "aud": 2166036160.2693434,
                    "usd": 6173502427.778992,
                    "btc": 6173502427.778992,
                    "cad": 219176.4024249574,
                    "eth": 2126019469.9872484,
                    "eur": 1619956219.9845994,
                    "hkd": 10526186426.055582
                },
                "volume_change": {                  // compared to base_currency
                    "24h": 0.34,
                    "48h": 31.395,
                    "7d": 35.395,
                    "30d": 121.395,
                    "1yr": 231.395,
                    "inception": 1039.59
                },
                "high": {                           // 24h high
                    "aud": 10109.68553964355,
                    "btc": 28814.001062341806,
                    "usd": 28814.001062341806,
                    "cad": 1.022976692111712,
                    "eth": 9922.912962846409,
                    "eur": 7560.930086226004,
                    "hkd": 49129.574404636725
                },
                "low": {                           // 24h low
                    "aud": 9567.863567088827,
                    "btc": 27269.733554557155,
                    "usd": 27269.733554557155,
                    "cad": 0.9681509265600554,
                    "eth": 9391.100944170325,
                    "eur": 7155.706992233335,
                    "hkd": 46496.50705448918
                }
            },
            "community_data": {
                "facebook_likes": 37863,
                "twitter_followers": 55785,
                "reddit_average_posts_48h": 3.313,
                "reddit_average_comments_48h": 191.969,
                "reddit_subscribers": 847008,
                "reddit_accounts_active_48h": 8234
            },
            "developer_data": {
                "forks": 19273,
                "stars": 31999,
                "subscribers": 3319,
                "total_issues": 3955,
                "closed_issues": 3418,
                "pull_requests_merged": 5488,
                "pull_request_contributors": 503,
                "commit_count_4_weeks": 30
            },
            "public_interest_stats": {
                "alexa_rank": 11135,
                "bing_matches": 32600000
            }
            
        },
        ...
    ]
}
```

<aside class="information">
    <strong>TODO:</strong> 
    <ol>
        <li>Determine if <code>/coins</code> returns too much or too little data for our home page.</li>
    </ol>
</aside>

### v1

Endpoint | Return
----- | ------
`/coins` | Returns a list of coins, their ID & summary data.
`/coins/:bcx_symbol` | All data for a particular coin, dev, community, news, cheatsheet.


### v1 if easy enough

Endpoint | Return
----- | ------
`/coins/:bcx_symbol/developer` | all dev data on github: stars, forks, branches, issues etc...
`/coins/:bcx_symbol/community` | all community data: facebook, youtube, twitter, reddit, reddit hot issues, recent news etc...
`/coins/:bcx_symbol/cheatsheet` | Instead of getting the top 10, return all cheat sheet data for the coin
`/coins/:bcx_symbol/tcmi` | Total Crypto Market Index Ranking. 


### v2

Endpoint | Return
----- | ------
`/coins/:bcx_symbol[:base_currency]` | Specify the base currency for a symbol. *While this endpoint may be easily created will it be difficult to process the data?*


## Coin Passed Parameters

Variable | Default | Type | Description
-------- | ------- | ---- | -----------
`bcx_symbol` | `null` | `String` | BCX Data symbol. Used when requesting indicies


## Coin Returned Data


```javascript
// get coins 
let data = requester.get("https://api.bcxdata.com/v1/coins/btc");

```

> The above command returns JSON structured like this:

```json
{       
    "name":                 "Bitcoin",  
    "id":                   "bitcoin",  // BCX Data id for coin
    "bcx_symbol":           "btc",      // BCX Data symbol. Used when requesting indicies
    "base_currency":        "usd",      // prices not specified are in this base currency
    "circulating_supply":   17069050.0, // coins released * conversion to base currency
    "bcx_score":            78.98,      // max 100
    "bcx_recomend" :        "buy",      // our algo

    "momentum_50" :         18.2939,    // 50 day momentum
    "momentum_25" :         24.8719,    // 25 day momentum

    "tcmi" :                82.302      // TCMI max 100

    "all_time_high" :       25000.39,
    "all_time_high_date" :  "2018-01-03T11:23:59.371Z",

    "market_cap" :          77333111.34, // in base currency
    "market_share" :        33.32,       // percent
    
    "images": {
        "thumb":            "https://bcxdata.com/coins/images/thumb/bitcoin.png",
        "small":            "https://bcxdata.com/coins/images/small/bitcoin.png"
    },
    "white_paper_url":      "https://bcxdata.com/coins/paper/bitcoin_whitepaper.pdf",
    "inception_date":       "2008-08-18T00:00:00.000Z",
    "website":              "https://bitcoin.org/en/",
    "opensource_url":       "https://github.com/bitcoin/bitcoin",

    "cheat_sheet": [
    {
        "type" :        "fundamental",     // determines what template we use to display
        "date" :        "2018-06-01T11:23:59.371Z",
        "price" :       243019.2409,       // price in relation to base_currency   
        "volume" :      49283091.392,
        "momentum" :    18.3920,
        "description":  "A new all time high was set less than 3 days ago."
    }, {
        "type" :        "general",
        "date" :        "2017-01-3T11:23:59.371Z",
        "price" :       243019.2409,   
        "volume" :      49283091.392,
        "momentum" :    18.3920,
        "description":  "More business are accepting bitcoin over other cryptocurrencies, with reduced fees, and quicker resolution times. It is a preffered and trusted coin for trading with small businesses.",
        "url":          "https://www.cbc.ca/bitcoin-accepted"
    },{
        "type" :        "news",
        "date" :        "2018-06-19T11:23:59.371Z",
        "price" :       243019.2409,   
        "volume" :      49283091.392,
        "momentum" :    18.3920,
        "description":  "SEC is clamping down on other crpyto currencies but not Bitcoin due to the annonominity of it's founders.",
        "url":          "https://www.sec.ca/bitcoin-anon"
    },{
        "type" :        "fork",
        "date" :        "2017-08-23T11:23:59.371Z",
        "price" :       243019.2409,   
        "volume" :      49283091.392,
        "momentum" :    18.3920,
        "description":  "SegWit (short for Segregated Witness) is a protocol upgrade that changes the way data is stored. This cointroversial upgrage is still heavily debated in the community. As of today, over 80% of transactions are now processed using this new procedure.",
        "url":          "https://www.coindesk.com/information/what-is-segwit/"
    },
    ... // 6 more "cheat sheet" items
    ],

    "asset_strong_coorleation" : [       // top 10 strongly coorelated assets
        {
            "asset":"eth",               // bcx_symbol
            "coorleation":85.32234       // percent coorleated
        }, {
            "asset":"iota",
            "coorleation":81.30324
        }, {
            "asset":"eos",
            "coorleation":78.32344
        },
        ...
    ],

    "asset_weak_coorelation" : [       // top 10 weakly coorelated assets
        {
            "asset":"mkd",             // bcx_symbol
            "coorleation":12.2942      // percent coorleated
        }, {
            "asset":"lyt",
            "coorleation":14.3902
        }, {
            "asset":"thm",
            "coorleation":24.3029
        },
        ...
    ],

    "symbols":[                         // exchanges we track
        {
        "exchange":"bitfinex",
        "id":"bfx",
        "symbol":"btc"
        }, {
        "exchange":"Kraken",
        "id":"krk",
        "symbol":"bit"
        },
        ...
    ],
    "market_data": {
        "current_price": {
            "aud": 9882.61572096458,
            "usd": 8789.61572096458,
            "btc": 1,
            "cad": 10290.03902323298,
            "eth": 9700.03817228985,
            "eur": 7391.10689865095,
            "hkd": 48026.0936377929
        },
        "price_change": {
            "24h": 42.83,
            "48h": 39.19,
            "7d": 140.39,
            "30d": 193.92,
            "1yr": 2930.32,
            "inception": 29103920.39
        },
        "price_percent_change": {
            "24h": 0.34,
            "48h":31.395,
            "7d": 35.395,
            "30d": 121.395,
            "1yr": 231.395,
            "inception": 1039.59
        },
        "market_cap": {
            "aud": 168686733397.9261,
            "usd": 8789.61572096458,
            "btc": 17069037,
            "cad": 165570310464.2278,
            "eth": 222770839.3036304,
            "eur": 109423370141.29701,
            "hkd": 1001761179709.8
        },
        "total_volume": {
            "aud": 2166036160.2693434,
            "usd": 6173502427.778992,
            "btc": 6173502427.778992,
            "cad": 219176.4024249574,
            "eth": 2126019469.9872484,
            "eur": 1619956219.9845994,
            "hkd": 10526186426.055582
        },
        "volume_change": {                  // compared to base_currency
            "24h": 0.34,
            "48h": 31.395,
            "7d": 35.395,
            "30d": 121.395,
            "1yr": 231.395,
            "inception": 1039.59
        },
        "high": {                           // 24h high
            "aud": 10109.68553964355,
            "btc": 28814.001062341806,
            "usd": 28814.001062341806,
            "cad": 1.022976692111712,
            "eth": 9922.912962846409,
            "eur": 7560.930086226004,
            "hkd": 49129.574404636725
        },
        "low": {                           // 24h low
            "aud": 9567.863567088827,
            "btc": 27269.733554557155,
            "usd": 27269.733554557155,
            "cad": 0.9681509265600554,
            "eth": 9391.100944170325,
            "eur": 7155.706992233335,
            "hkd": 46496.50705448918
        }
    },
     "community_data": {
        "facebook_likes": 37863,
        "twitter_followers": 55785,
        "reddit_average_posts_48h": 3.313,
        "reddit_average_comments_48h": 191.969,
        "reddit_subscribers": 847008,
        "reddit_accounts_active_48h": 8234
    },
    "developer_data": {
        "forks": 19273,
        "stars": 31999,
        "subscribers": 3319,
        "total_issues": 3955,
        "closed_issues": 3418,
        "pull_requests_merged": 5488,
        "pull_request_contributors": 503,
        "commit_count_4_weeks": 30
    },
    "public_interest_stats": {
        "alexa_rank": 11135,
        "bing_matches": 32600000
    },
    // Here we have data from Amazon Turk fill in the blanks
    // Amazon Turk Data: description, supply_generated, used_for, proof, references, website
    "description": {
        "en": "Bitcoin is the first successful internet money based on peer-to-peer technology; whereby no central bank or authority is involved in the transaction and production of the Bitcoin currency. It was created by an anonymous individual/group under the name, Satoshi Nakamoto. The source code is available publicly as an open source project, anybody can look at it and be part of the developmental process.\r\n\r\nBitcoin is changing the way we see money as we speak. It is a decentralized peer-to-peer internet currency making mobile payment easy, very low transaction fees, protects your identity, and it works anywhere all the time with no banking hours.\r\n\r\nAs of the current design, there will only be 21 million Bitcoin ever created, thus making it a deflationary currency unlike fiat currencies. Bitcoin uses the SHA-256 hashing algorithm with an average transaction confirmation time of 10 minutes. Miners today are mining Bitcoin using ASIC chip dedicated to only mining Bitcoin, and the hash rate has shot up to peta hashes.\r\n\r\nBeing the first successful online cryptography currency, Bitcoin has inspired other alternative currencies such as Litecoin, Peercoin, Primecoin, and so on.",
        "fr": "French localization of translated description"
    },
    "used_for":{
        "en":""
    },
    "supply_generated": {
        "en": "Through mining. In addition to rewards from people funding their transactions. Miners generate new bitcoin for every block that is added to the transaction based on difficulty of hash.",
        "fr": "french localization of generationg"
    },
    "proof":"POW or Proof of Work",
    "references":[{
        "nice":"Wikipedia",
        "url":"https://en.wikipedia.org/wiki/Bitcoin"
    },{
        "nice":"Bitcoin Wikipedia",
        "url":"https://en.bitcoin.it/wiki/Main_Page"
    }
    ...
    ]
}
```


Variable | Type | Description
--------- | --- | ---------
`name` | `string` | Name of the coin used in nice display
`id` | `string` | BCX Data id
`bcx_symbol` | `string` | BCX Data symbol for the coin. Made from the most common symbols found on exchanges. Used when requesting indicies.
`base_currency` | `string` | Default to USD. What price each coin is stated in for ATH, curculating_supply, cheat_sheet.price, 
`circulating_supply` | `number` | How many coins are out there
`bcx_score` | `number` | A figure that sums up our score of the coin. TODO: determine formula that makes up this number
`bcx_recomend` | `enum` | [`buy`,`hold`,`sell`] A reccomendation to buy/hold/sell without being legally responsible for advice given. TODO: determine formula that makes this up.
`momentum_50` | `number` | 50 day moving momentum. In relation to all the other coins, does this one have momentum.
`momentum_25` | `number` | 25 day moving momentum. In relation to all the other coins, does this one have momentum.
`tcmi` | `number` | Total Crypto Momentum Index. How is this coin doing in relation to the rest of the coins we are trading? In addition to momentum on price the **Total** in **TCMI** means we pull in other factors as well such as **developer interest momentum** and **community interest momentum**.
`all_time_high` | `number` | A price in relation to the base_currency that was the highest ever offered for this coin.
`all_time_high_date` | `date` | A date specifying was the all time high purchased
`market_cap` | `number` | Shown in the base currency
`market_share` | `number` | Percent. of the market that this coin occupies. TODO: Determine if this will be for all coins or only the ones we track, and if it is for all coins, how do we figure out market share?
`images` | `array` | An array containing the links to each coin's image.
`white_paper_url` | `string` | the url to the white paper
`inception_date` | `date` | the date the coin was first launched
`website` | `string` | The url to the community website, or companies website running the coin.
`opensource_url` | `string` | the url to the main repository where the source code for the coin is kept
`cheat_sheet` | `array` | the array containing objects for our cheatsheet. We return up to 10 objects here with a ratio of 25:25:25:25 for the four types of cheat sheet's. `fundamental`, `general`, `fork`, `news`. See Cheat Sheet for more information.
`cheat_sheet.type` | `enum` | `fundamental`, `general`, `fork`, `news`
`cheat_sheet.date` | `date` | The date the event occured
`cheat_sheet.price` | `number` | The price on the date in the base_currency
`cheat_sheet.volume` | `number` | The volume traded on that day
`cheat_sheet.momentum` | `number` | The momentum on that day.
`cheat_sheet.description` | `string` | The description of the event
`cheat_sheet.url` | `string` | The url pointing to an outside reference. Not present on `fundamental`
`asset_strong_coorleation` | `array` | An array containing the top 10 most strongly coorelated data points with this coin. Check `asset_strong_coorleation.asset` & `asset_strong_coorleation.coorleation` for details. This is refreshed daily on the server.
`asset_weak_coorelation` | `array` | An array containing the top 10 most weakly coorelated data points with this coin. Check `asset_weak_coorelation.asset` & `asset_weak_coorelation.coorleation` for details. This is refreshed daily on the server.
`symbols` | `array` | An array of exchanges, and what this coin's ticker/symbol is on that exchange
`symbols.exchange` | `string` | The nice name of the exchange
`symbols.id` | `string` | An id that the exchange has given itself. Use this in `/exchanges/:exchangeId`
`symbols.symbol` | `string` | the symbol that this coin is trading under on this exchange
`market_data` | `array` | An array containing `current_price`, `price_change`, `price_percent_change`, `market_cap`, `total_volume`, `volume_change`, `high`, `low`
`market_data.current_price` | `array` | An array containing the current price in different base currencies. This comes from a volume weighted amalgamation accross the different exchanges.
`market_data.price_change` | `array` | An array containing the absolute price change in `base_currency`. This comes from: a volume weighted amalgamation of different exchanges. Looks up price on a particular day and compares it to today.
`market_data.price_percent_change` | `array` | An array containing the price change as a percent, calculated using `base_currency`. This comes from: a volume weighted amalgamation of different exchanges. Looks up price on a particular day and compares it to today.
`market_data.market_cap` | `array` | number of coins * current price in a variety of currencies.
`market_data.total_volume` | `array` | number of coins traded in the past `24 hours`
`market_data.volume_change` | `array` | number of coins traded in the past `24 hours` compared to `7d`, `14d`, `30d`, &  `1yr`
`market_data.high` | `array` | the `24h` high in a variety of currencies
`market_data.low` | `array` | the `24h` low in a variety of currencies
`community_data` | `array` | TODO: this needs to be scoped out further, but for now should be relativly self explanitory.
`developer_data` | `array` | Key metricis on the `opensource_url`, such as `forks`, `stars`, `subscribers`, `issues`. TODO: it would be great to see the change over time. The `momentum` as it were on these stats to see interest ramping up or cooling off.
`public_interest_stats` | `array` | TODO: this needs to be scoped out further, but for now should be relativly self explanitory.
`description` | `array` | An array of localizations that contain descriptions. Currently only `en` supported. But this should make it easier when we want to add translations later on down the road. User will be able to toggle between these. **TODO: Should the get have a specified parameter for localization, or is that a cookie, or how should we display localization by default?**
`used_for` | `array` | What kind of coin is this. **TODO: Should the get have a specified parameter for localization, or is that a cookie, or how should we display localization by default?**
`supply_generated` | `array` | Description of how this coin generates supply.
`references` | `array` | Array of objects contining `references.nice` & `references.url`. These are what were used in Amazon Turk.

### Cheat Sheet

Top 10 (ten) cheat items we have on this particular coin. 

**These are things you NEED to know before investing in this coin.**

A cheatsheet can have **4** types of information: `fundamental`, `general`, `fork`, `news`

This is server generated, and while we may more than 10 items, we try to give out a balanced understanding of 25% of each type of information.

`fundamental`: an alert about a factor making up the price. I.e. price, tcmi, volume, momentum etc...

`general`: something outside about the coin. example:
The original Bitcoin software by Satoshi Nakamoto was released under the MIT license. Satoshi Nakamoto is a pseudonym for an anonomyous person or group still unknown to today.

`news`: An important alert about news in the media either recently or not.

`fork`: Information about the latest fork, hard or soft. Was it controversial. Are the core developers happy about this, or not. What makes it controversial. Link to more information.