---
title: Suredbits API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json
  - javascript
 

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---
 
# Lightning API v0 Beta Documentation

## Connect With Us

Follow us on twitter <a href="https://twitter.com/Suredbits">@Suredbits</a>

We invite you to join our Slack channel <a href="https://join.slack.com/t/suredbits/shared_invite/zt-eavycu0x-WQL7XOakzQo8tAy7jHHZUw">Suredbits Slack</a>

## Websocket Playground

Explore and experiment with our APIs on our <a href="https://suredbits.com/ws-playground/"> Websocket Playground. </a>

## Blog

To learn more about all things Lightning Network, check out our <a href="https://suredbits.com/blog/">Suredbits Blog</a>. 

## Background Resources
Thank you and welcome to Suredbits' Lightning App API documentation. This API allows you to query our NFL, NBA and Crypto Exchange data. Our NFL and NBA APIs offer multiple channels including teams, players, games, scores, and statistics.  Our Crypto Exchange API allows you to stream data on Trades, Tickers and Order Books. 

We are currently focused primarily on developers already familiar with Bitcoin and know Lightning or are interested in building apps using the Lightning protocol. However, if you are just starting out in cryptocurrency development, we have included some helpful links below.

<aside class="success">IMPORTANT: Suredbits is a Lightning application built on the Bitcoin protocol.  As of February 6, 2019, we have moved our API services to mainnet. We have kept some data available for free - on testnet - for testing and experiment.  See <a href="#Testnet"> Testnet Node </a> section below. </aside>

Here are some useful resources to help you learn and get started with Bicoin and Lightning Network.  Read and watch and come back when you're ready. 

1. <a href="https://bitcoin.org/en/download">Download Bitcoin Core</a>
2. <a href="http://lightning.network/">Lightning Network Background</a>
3. <a href="https://lightning.network/lightning-network-paper.pdf">Lightning Whitepaper</a>
4. <a href="https://www.youtube.com/watch?v=l1si5ZWLgy0">Introduction to Bitcoin</a>

## Recommended Client Library

We recommend using our custom <a href="https://github.com/suredbits/sb-api"> Javascript Client Library</a> for interacting with our API services. It supports all major implementations of the Lightning protocol: LND, C-lightning and Eclair.   

## Mainnet Node (paid) 
In order to access our paid API service, you will need to connect to our lightning node via your preferred lightning client.  

Our paid service offers complete coverage for all channels, endpoints and fields .  

The Lightning Node URL for our paid service is: 
<span style="color: blue"><code style="word-wrap: break-word;"> 038bdb5538a4e415c42f8fb09750729752c1a1800d321f4bb056a9f582569fbf8e@ln.suredbits.com </code></span>


<h2 id="Testnet"> Testnet Node (free) </h2>

In order to access our free API service, you will need to connect to our lightning node via your preferred lightning client.   

The Lightning Node URL for our testnet service is:

<span style="color:blue"><code style="word-wrap: break-word;" > 0338f57e4e20abf4d5c86b71b59e995ce4378e373b021a7b6f41dabb42d3aad069@ln.test.suredbits.com </code></span>


We provide a number of free data endpoints so users can experiment and learn the structure of our Lightning API service. To allow for complete testing, we make the following data avaialble for free on testnet:  

## Crypto Spot Exchange Testnet API

Currently, we offer the trading pair `BTCUSD` data for free across all available exchanges. 

For Binance, the symbol is `BTCUSDT`.

## Crypto Futures Testnet API

Currently, we offer the trading pair `BTCUSD` data for free across all available exchanges. 

## Historical Prices Data API

All data is currently available on both mainnet and testnet.  

## NFL Testnet API 

> Example request for "Tom Brady" in "Players" endpoint

```json
{
  "channel":"players", 
  "lastName" : "Brady", 
  "firstName" : "Tom", 
  "uuid": "6dc1320d-de0e-40a5-8162-83d9eb4634de"
}

```

```javascript
import {  Lnd, NflRestAPI } from "sb-api"
const ln = await Lnd()

const players = await NflRestAPI(ln).players({
   network: 'testnet',
   firstName: 'Tom',
   lastName: 'Brady',
})
```

> Example request for "NE" (New England) roster in "Team" endpoint

```json
{
  "channel": "team", 
  "teamId": "NE", 
  "retrieve": "roster", 
  "uuid": "689c2c7d-cd08-4b2c-b87d-f1de10b4e94d"
}

```

```javascript
import {  Lnd, NflRestAPI } from "sb-api"
const ln = await Lnd()

const players = await NflRestAPI(ln).roster({
   teamId: 'NE',
})
```

> Example request for Tom Brady in "Stats" endpoint by lastName and firstName

```json
{
    "channel":"stats", 
    "lastName" : "Brady", 
    "firstName" : "Tom", 
    "year": 2018, 
    "week" : 2, 
    "seasonPhase" : "Postseason", 
    "statType" : "passing",
    "uuid": "b97247c2-8bd6-450e-b81c-3c5a725e2057"
}

```

```javascript
import {  Lnd, NflRestAPI } from "sb-api"
const ln = await Lnd()

const players = await NflRestAPI(ln).statsByName({
  year: 2018,
  week: 2,
  seasonPhase: 'postseason',
  statType: 'passing',
})
```

> Example request for Tom Brady in "Stats" endpoint by playerId and gameId

```json
{
  "channel":"stats", 
  "statType" : "passing", 
  "gameId" : "2019011300", 
  "playerId" : "00-0019596",
  "uuid": "aa334616-71e0-45ee-be6d-6dbce545bad3"
}

```

```javascript
import {  Lnd, NflRestAPI } from "sb-api"
const ln = await Lnd()

const stats = await NflRestAPI(ln).statsById({
  statType: 'passing',
  gameId: '2019011300',
  playerId: '00-0019596',
})
```

Currently, we offer `Info` and `Games` data endpoints for free on testnet. 

In addition, to help developers build and test end-to-end applications, we offer a series of data across all endpoints: `Games`, `Players`, `Team` and `Stats` for a specific player.  

For testing, we provide data for **Tom Brady** for free on testnet.   

## NBA Testnet API 

> Example request for "Lebron James" in Players endpoint  

```json

{
  "channel": "players", 
  "lastName": "James", 
  "firstName": "Lebron", 
  "uuid": "2602b409-1737-49e5-a32d-62608d1e2c29"
}
```

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nbaTestnet(ln)
const players = await nba.players() // name is inferred automatically on testnet
```

> Example request for "LAL" (Los Angeles Lakers) in "Team" endpoint

```json
{
  "channel": "games", 
  "year": 2019, 
  "month": 1, 
  "day": 14, 
  "teamId":"LAL",
  "uuid": "2c48e899-01ef-443e-b455-144486b1c291"
}
```

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nbaTestnet(ln)
const games = await nba.games({ day: 14, month: 1, year: 2019, teamId: 'LAL' })
```

> Example request of Lebron James in "Stats" endpoint by playerId and gameId

```json
{
  "channel": "stats", 
  "gameId": "21800500", 
  "playerId": "2544", 
  "uuid": "ddc2632e-f9bb-4ea9-bdf6-992e1590f676"
}
```

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nbaTestnet(ln)
const stats = await nba.statsById({ gameId: '21800500', playerId: '2544' })
```

> Example request for Lebron James in "Stats" endpoint by lastName and firstName 

```json

{
  "channel": "stats", 
  "lastName": "James", 
  "firstName": "Lebron", 
  "year": 2019, 
  "month": 1, 
  "day": 13, 
  "uuid": "689c2c7d-cd08-4b2c-b87d-f1de10b4e94d"
}

```

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nbaTestnet(ln)
const stats = await nba.statsByName({ year: 2019, month: 1, day: 13 }) 
// name is inferred automatically because we're on testnet
```

Currently, we offer `Info` and `Games` data endpoints for free. 

In addition, to help developers build and test end-to-end applications, we offer a series of data across all endpoints: `Games`, `Players`, `Team` and `Stats` for a specific player.  

For testing, we provide data for **Lebron James** for free on testnet.   


## Payment & Pricing

### How to Pay

This is our recommended lnd lightning client library: <a href="https://github.com/Suredbits/sb-api-lnd">https://github.com/Suredbits/sb-api-lnd</a>

This is an alternative c-lightning client library: <a href="https://github.com/suredbits/lightning-charge">https://github.com/suredbits/lightning-charge</a>


### Pricing

<aside class="success"> All payments are transacted in cryptocurrency.  For convenience, we have quoted prices in USD equiavalents. </aside>

<aside class="success"> We reserve the right to change pricing as necessary.  We also reserve the right to change what is available in our free API offerings. Any changes in pricing or services will be announced via our Twitter <a href="https://twitter.com/Suredbits">@Suredbits</a> </aside>

For NFL Data and NBA Data APIs, the cost is $.01 (1 cent) per call.  

For our streaming Crypto Spot and Futures Exchange APIs, the cost is $.0001 per minute.    

Anything less than 60 seconds will be prorated accordingly.  

A minimum of 10 satoshis will be charged for all streaming data calls. 

For Historical Prices Data API the cost is $.0001.



## UUID

> Example data returned with valid UUID

```json
{
  "uuid":"123e4567-e89b-12d3-a456-426655440000",
  "data":
    {
      "version":"8",
      "lastRosterDownload":"2018-07-20T141610.664Z",
      "seasonType":"Regular",
      "seasonYear":2017,
      "week":"NflWeek17" 
    }
 }
```

```javascript
// our JS client library automatically generates and inserts UUIDs for you
```
<aside class="warning"> All request require a field called <b> uuid </b> </aside>  

A valid <span style="color:red"> `uuid` </span> is required for all requests and will appear on all invoices, data responses, and errors related to that request.  If no <span style="color:red"> `uuid` </span> is specified in a request, then there will be an error message returned.

## Format 

> Basic example request

```json
{  
   "channel":"players",
   "lastName":"Moss",
   "firstName":"Randy",
   "uuid":"bfbef9da-eb9e-418c-8f6b-963743355ef7"
}
```


> Example data returned

```javascript
  [
    { 
      playerId: "00-0011754",
      gsisName: "R.Moss",
      fullName: "Randy Moss",
      firstName: "Randy",
      lastName: "Moss",
      team: "UNK",
      position: "UNK",
      profileId: 2502220,
      profileUrl: "http://www.nfl.com/player/randymoss/2502220/profile",
      birthDate: "2/13/1977",
      college: "Marshall",
      yearsPro: 14,
      height: 76,
      weight: 210,
      status: "Unknown"
    }
  ]
```

```json 
{  
  "uuid":"bfbef9da-eb9e-418c-8f6b-963743355ef7",
  "data":
  [
    { 
      "playerId": "00-0011754",
      "gsisName": "R.Moss",
      "fullName": "Randy Moss",
      "firstName": "Randy",
      "lastName": "Moss",
      "team": "UNK",
      "position": "UNK",
      "profileId": 2502220,
      "profileUrl": "http://www.nfl.com/player/randymoss/2502220/profile",
      "birthDate": "2/13/1977",
      "college": "Marshall",
      "yearsPro": 14,
      "height": 76,
      "weight": 210,
      "status": "Unknown"
    }
  ]
}
```

Suredbits APIs are available via websockets with the following format:


<aside class="note">NOTE: All API requests must include the  "channel" field.  However, "channel" does not have to be the first field in the request. </aside>

<aside class="note">NOTE: All times are in Universal Time Coordinated or "UTC".  So be sure to do time zone conversions. </aside>

1. Send a request over the websocket 

2. Upon confirmation of a valid request, you will receive a Lightning Network invoice that should appear similar to the one below.

3. Pay that LN invoice in your lightning client 

4. Receive data :)

### Ping/Pong

To confirm your connection, send a <span style="color:red">`ping`</span> request. Ping has an optional `uuid` field for correlating multiple pongs to multiple pings. 

<aside class="success"><code>{"event": "ping"}</code> should return <code>{"event":"pong"}</code></aside>


### Sample Lightning Invoice

A successful request will generate a lightning invoice that will look similar to the example below:

<span style="color:blue"><code style="word-wrap:break-word;">lnbcrt10n1pd5v2mwpp5ulxpj8ht4gvtqnyl8zuykfk4wcv6sz455ce5dy0e0lqt...</code></span>

# Crypto Spot Exchange API 

## Crypto Spot Exchange Websocket Endpoints 

This is the paid service url **wss://api.suredbits.com/exchange/v0** on mainnet.

This is the free version url **wss://test.api.suredbits.com/exchange/v0** on testnet. 

## Overview

### Trading Pairs Supported

Symbol    | Binance  | Bitfinex  | Coinbase | Bitstamp | Gemini |  Kraken |
-------   | :-----:  | :-------: | :------: | :------: | :-----: | :-----:
`BTCUSDT` | &#10003; |           |         |         |         |
`ETHBTC`  | &#10003; |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`ETHUSDT` | &#10003; |           |         |         |         |
`BTCUSD`  |          |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`ETHUSD`  |          |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`LTCUSD`  |          |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;    
`LTCBTC`  | &#10003; |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`LTCETH`  | &#10003; |           |         |         | &#10003;|
`LTCUSDT` | &#10003; |           |         |         |         |
`LTCBCH`  |          |           |         |         | &#10003;| 
`BCHUSDT` | &#10003; |           |         |         |         | 
`BCHUSD`  |          | &#10003;  | &#10003;| &#10003;| &#10003;| &#10003;
`BCHBTC`  | &#10003; | &#10003;  | &#10003;| &#10003;| &#10003;| &#10003;
`BCHETH`  |          |           |         |         | &#10003;|
`XRPUSDT` | &#10003; |           |         |         |         |         
`XRPBTC`  | &#10003; | &#10003;  | &#10003;| &#10003;|         | &#10003; 
`XRPETH`  | &#10003; |           |         |         |         |
`XRPUSD`  |          | &#10003;  | &#10003;| &#10003;|         | &#10003;       
`EOSUSDT` | &#10003; |           |         |         |         | 
`EOSUSD`  |          | &#10003;  | &#10003;|         |         | &#10003;
`EOSBTC`  | &#10003; | &#10003;  | &#10003;|         |         | &#10003;
`EOSETH`  | &#10003; | &#10003;  |         |         |         | &#10003;

### Euro Trading Pairs Supported


Symbol | Bitfinex | Coinbase | Bitstamp | Kraken |
------ | :------: | :------: | :------: | :-----:
`BTCEUR` | &#10003;| &#10003; | &#10003; | &#10003;|
`ETHEUR` | &#10003; | &#10003; | &#10003; | &#10003; |
`EOSEUR` | &#10003; | &#10003; |          | &#10003; |
`LTCEUR` |        | &#10003; | &#10003; |  &#10003; |
`BCHEUR` |       | &#10003; | &#10003; |  &#10003; |
`XRPEUR` |       | &#10003; | &#10003; |  &#10003; |
`EURUSD` |       |          | &#10003; |        |

### Subscribe

> Example request format: 

```javascript
// Our library handles request construction for you
// Refer to the sections on tickers, trades and books
// for specfics on how to send requests
```

```json
{  
   "event":"subscribe",
   "channel":"trades",
   "symbol":"BTCUSDT",  
   "exchange":"binance",
   "duration":120000,
   "refundInvoice":"lnbcrt1pdace6qpp5my6nc58d50r5gk38ynyz...",
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8"
}
```

> Example subscription confirmation 

```javascript
// Our library handles request construction for you
// Refer to the sections on tickers, trades and books
// for specfics on how to send requests
```

```json
{  
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8",
   "exchange":"binance",
   "symbol":"BTCUSDT",
   "duration":100000,
   "event":"payment received"
}
```


To subscribe to a data stream, use the following command format:

Field | Type | Example
------ | ------ | -------
 `uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"
 `event` | String | "subscribe"
 `channel` | String | "tickers" 
 `symbol`  | String | "ETHBTC"
 `exchange`  | String | "bitfinex" 
 `duration` | Integer (milliseconds) | "15000" 
 `refundInvoice`  | String | lnbcrt10n1pd5v2mwpp5ulxpj8ht...


### Snapshots
> Example of snapshot from trades channel

```javascript 
[
  {
    eventTime: 1543347647113,
    symbol: 'BTCUSDT',
    tradeId: 82634229,
    price: 3809.1,
    quantity: 0.293652,
    buyerId: 195007870,
    sellerId: 195007859,
    tradeTime: 1543347647109,
    marketMaker: false,
  }
]

```

```json
{  
   "uuid":"f8363f36-65dd-4a07-a3e0-75f38b816df7",
   "snapshot":[  
      {  
         "eventTime":1543347647113,
         "symbol":"BTCUSDT",
         "tradeId":82634229,
         "price":3809.1,
         "quantity":0.293552,
         "buyerId":195007870,
         "sellerId":195007859,
         "tradeTime":1543347647109,
         "marketMaker":false
      },
      ...
    ]
}
```

Upon subscribing to a channel an initial snapshot is sent.  The snapshot provides a view of the current state of the market.


### Sequence Identifier

In order to better monitor potential gaps in streaming data, we provide a sequence number for each returned data value. 

Example: `"seq": 21` , `"seq":437`, `"seq":2873` etc. 


### Refill

> Subscription refill 

```javascript
import { Lnd, Sockets } from "sb-api"

const ln = await Lnd()
const refundInvoice = await ln.receive()
const exchangeSocket = await Sockets.exchange(ln)
const sub = await exchangeSocket.books({
  duration: 10000,
  exchange: "bitfinex",
  refundInvoice,
  symbol: "ETHBTC",
  onData: data => console.log("received data", data),
  onSnapshot: snapshot => console.log("received snapshot: ", snapshot),
})
await sub.refill(60000) // adds one minute to our subscription
```
 


```json
{
    "event": "refill",
    "addedDuration": 60000, // adds one minute to our subscription
    "uuid": "8f2e4f08-2ef4-11e9-9f18-5f29bb1268a9"
}
```

You may refill your subscription at any time. 


### Unsubscribe
 
> Subscription cancellation

```javascript
import { Lnd, Sockets } from "sb-api"

const ln = await Lnd()
const refundInvoice = await ln.receive()
const exchangeSocket = await Sockets.exchange(ln)
const sub = await exchangeSocket.books({
  duration: 10000,
  exchange: "bitfinex",
  refundInvoice,
  symbol: "ETHBTC",
  onData: data => console.log("received data", data),
  onSnapshot: snapshot => console.log("received snapshot: ", snapshot),
})
await sub.unsubscribe()
```
```json
{
    "event": "unsubscribe",
    "uuid": "8f2e4f08-2ef4-11e9-9f18-5f29bb1268a9"
}
```
You may unsubscribe from a channel at any time. Any time remainaing will be refunded. 


### Maintenance

In the event of maintenance or service interruption, we will refund any remaining portion of your subscription. 


## Tickers

> Example request Tickers

```json
{  "event":"subscribe",
   "channel":"tickers",
   "symbol":"BTCUSDT",
   "exchange":"binance",
   "duration":120000,
   "refundInvoice":"lnbcrt1pdace6qpp5my6nc58d50r5gk...",
    "uuid":"dc48f38e-7f71-4ea2-8c4c-52c683db93fa"
}
```

```javascript
import { Lnd, Sockets } from "sb-api"

const ln = await Lnd()
const refundInvoice = await ln.receive()
const exchangeSocket = await Sockets.exchange(ln)
const tickersSub = await exchangeSocket.tickers({
  duration: 10000,
  exchange: "binance",
  symbol: "BTCUSDT",
  refundInvoice,
  onData: data => console.log("received data", data),
  onSnapshot: snapshot => console.log("received snapshot: ", snapshot),
  onSubscriptionEnded: dataset => console.log(`got dataset with ${dataset.length} elements`) 
  //                    ^^^ dataset is the list of all your 
  //                        previously received data points
})
```

> Example Tickers data

```javascript
// snapshot
[
  {
    eventTime: 1543849532563,
    symbol: 'BTCUSDT',
    priceChange: -253.84,
    priceChangePerc: -6.08,
    weightedAvePrice: 4079.82822535,
    prevClose: 4174.49,
    close: 3921.26,
    closeQuantity: 1.144132,
    bid: 3920.31,
    bidSize: 0.052611,
    ask: 3922.57,
    askSize: 1.207388,
    open: 4175.1,
    high: 4268,
    low: 3896.03,
    volume: 42258.714174,
    quoteVolume: 172408294.85387801,
    statOpenTime: 1543763132561,
    statCloseTime: 1543849532561,
    firstTradeId: 83998182,
    lastTradeId: 84182065,
    totalTrades: 183884,
  }
]


// data
{
  eventTime: 1541716718571,
  symbol: 'BTCUSDT',
  priceChange: -68.06,
  priceChangePerc: -1.036,
  weightedAvePrice: 6524.40647569,
  prevClose: 6575.83,
  close: 6503.16,
  closeQuantity: 0.040421,
  bid: 6501.05,
  bidSize: 0.123017,
  ask: 6503.16,
  askSize: 0.463804,
  open: 6571.22,
  high: 6594,
  low: 6471.22,
  volume: 12760.988421,
  quoteVolume: 83257875.49020969,
  statOpenTime: 1541630318568,
  statCloseTime: 1541716718568,
  firstTradeId: 77686104,
  lastTradeId: 77828352,
  totalTrades: 142249
}
```

```json

{  
   "uuid":"dc48f38e-7f71-4ea2-8c4c-52c683db93fa",
   "exchange":"binance",
   "symbol":"BTCUSDT",
   "duration":120000,
   "event":"payment received"
}

{  
   "uuid":"dc48f38e-7f71-4ea2-8c4c-52c683db93fa",
   "snapshot":[  
      {  
         "eventTime":1543849532563,
         "symbol":"BTCUSDT",
         "priceChange":-253.84,
         "priceChangePerc":-6.08,
         "weightedAvePrice":4079.82822535,
         "prevClose":4174.49,
         "close":3921.26,
         "closeQuantity":1.144132,
         "bid":3920.31,
         "bidSize":0.052611,
         "ask":3922.57,
         "askSize":1.207388,
         "open":4175.1,
         "high":4268,
         "low":3896.03,
         "volume":42258.714174,
         "quoteVolume":172408294.85387801,
         "statOpenTime":1543763132561,
         "statCloseTime":1543849532561,
         "firstTradeId":83998182,
         "lastTradeId":84182065,
         "totalTrades":183884
      }
   ]
}


{  
   "uuid":"dc48f38e-7f71-4ea2-8c4c-52c683db93fa",
   "data":{  
      "eventTime":1541716718571,
      "symbol":"BTCUSDT",
      "priceChange":-68.06,
      "priceChangePerc":-1.036,
      "weightedAvePrice":6524.40647569,
      "prevClose":6575.83,
      "close":6503.16,
      "closeQuantity":0.040421,
      "bid":6501.05,
      "bidSize":0.123017,
      "ask":6503.16,
      "askSize":0.463804,
      "open":6571.22,
      "high":6594,
      "low":6471.22,
      "volume":12760.988421,
      "quoteVolume":83257875.49020969,
      "statOpenTime":1541630318568,
      "statCloseTime":1541716718568,
      "firstTradeId":77686104,
      "lastTradeId":77828352,
      "totalTrades":142249,
   },
   "seq":123
}
```

The **Tickers** channel streams high level updates for given trading pairs.  See the table below for which exchanges return which fields.


Field | Type | Exchanges Supporting
------ | ------ | --------
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"
`eventTime` | Integer | bitfinex, binance, coinbase, bitstamp, kraken
`symbol` | String | binance, coinbase, bitstamp, gemini, kraken
`priceChange` | Double | binance, bitfinex 
`priceChangePerc`  |  Double | binance, bitfinex 
`weightedAvePrice` |  Double | binance, bitstamp, kraken
`prevClose` | Double | binance 
`close` | Double | binance, bitfinex, kraken
`closeQuantity` |  Double | binance, kraken
`bid` | Double | bitfinex, binance, coinbase, bitstamp, gemini, kraken    
`bidSize` | Double |  bitfinex, binance, kraken 
`ask` | Double | bitfinex, binance, coinbase, bitstamp, gemini, kraken      
`askSize` | Double | bitfinex, binance, kraken        
`open`  | Double | binance, coinbase, bitstamp, kraken
`high`  | Double | binance, bitfinex, coinbase, bitstamp, kraken
`low`  | Double | binance, bitfinex, coinbase, bitstamp, kraken
`volume`  | Double | binance, bitfinex, coinbase, bitstamp, gemini, kraken
`quoteVolume` | Double| binance 
`statOpenTime` | Integer | binance, kraken
`statCloseTime`  | Integer | binance, gemini, kraken
`firstTradeId`  | Integer | binance 
`lastTradId`  | Integer | binance, coinbase
`totalTrades` | Integer | binance, kraken


## Trades

> Example request Trades

```json

{  "event":"subscribe",
   "channel":"trades",
   "symbol":"BTCUSDT",
   "exchange":"binance",
   "duration":12000,
   "refundInvoice":"lnbcrt1pdace6qpp5my6nc58d50r5gk38ynyz...",
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8"
}
```

```javascript
import { Lnd, Sockets } from "sb-api"

const ln = await Lnd()
const refundInvoice = await ln.receive()
const exchangeSocket = await Sockets.exchange(ln)
const tickersSub = await exchangeSocket.trades({
  duration: 10000,
  exchange: "gemini",
  symbol: "BTCUSD",
  refundInvoice,
  onData: data => console.log("received data", data),
  onSnapshot: snapshot => console.log("received snapshot: ", snapshot),
  onSubscriptionEnded: dataset => console.log(`got dataset with ${dataset.length} elements`) 
  //                    ^^^ dataset is the list of all your 
  //                        previously received data points
})
```

> Example Trades data

```javascript
// snapshot
[
  {
    eventTime: 1543839862868,
    symbol: 'BTCUSDT',
    tradeId: 84153760,
    price: 4038.81,
    quantity: 0.115984,
    buyerId: '199276007',
    sellerId: '199274414',
    tradeTime: 1543839862861,
    marketMaker: false,
  },
  // rest of elements omitted
  // for brevity
]


//data
{
  eventTime: 1541715784094,
  symbol: 'BTCUSDT',
  tradeId: 77827378,
  price: 6502.99,
  quantity: 0.030665,
  buyerId: '183136564',
  sellerId: '183136526',
  tradeTime: 1541715784094,
  marketMaker: false,
}

```

```json

{  
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8",
   "exchange":"binance",
   "symbol":"BTCUSDT",
   "duration":10000,
   "event":"payment received"
}

{  
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8",
   "snapshot":[  
      {  
         "eventTime":1543839862868,
         "symbol":"BTCUSDT",
         "tradeId":84153760,
         "price":4038.81,
         "quantity":0.115984,
         "buyerId":"199276007",
         "sellerId":"199274414",
         "tradeTime":1543839862861,
         "marketMaker":false
      },
      ...
    ]
}

{  
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8",
   "data":{  
      "eventTime":1541715784094,
      "symbol":"BTCUSDT",
      "tradeId":77827378,
      "price":6502.99,
      "quantity":0.030665,
      "buyerId":"183136564",
      "sellerId":"183136526",
      "tradeTime":1541715784094,
      "marketMaker":false,
   }
   "seq":893
}{  
   "uuid":"8dda8625-2946-4500-8dd5-13c78d2f42b8",
   "data":{  
      "eventTime":1541715784161,
      "symbol":"BTCUSDT",
      "tradeId":77827379,
      "price":6501.35,
      "quantity":0.088033,
      "buyerId":"183136558",
      "sellerId":"183136565",
      "tradeTime":1541715784156,
      "marketMaker":true,
   }
   "seq":894
}
```

The **Trades** channel streams executed trades for a given trading pair.  See the table below for which exchanges returns which fields. 

Field |  Type | Exchanges Supporting 
------ | ------- | -----------
`uuid` | String | "123e4567-e89b-12d3-a456-426655440000"
`eventTime` | Integer | bitfinex, binance, kraken
`symbol` | String | binance, coinbase, kraken
`tradeId` | Integer | bitfinex, binance, coinbase, bitstamp, gemini 
`price` | Double | binance, bitfinex, coinbase, bitstamp, gemini, kraken
`quantity` | Double | bitfinex, binance, coinbase, bitstamp, gemini, kraken
`buyerId` | String | binance, coinbase, bitstamp
`sellerId` | String | binance, coinbase, bitstamp 
`tradeTime` | Integer | binance, coinbase, gemini, kraken
`marketMaker` |  Boolean | binance, coinbase, bitstamp, gemini, kraken


## Order Books

> Example request Order Books

```json
{ "event":"subscribe", 
  "channel":"books", 
  "symbol":"BTCUSD", 
  "exchange":"bitfinex", 
  "duration":15000,
  "refundInvoice":"lnbcrt1pdace6qpp5my6nc58d50r5...",
  "uuid":"d7975109-e6d0-47ae-9c26-531d553c420b"
}
```


```javascript
import { Lnd, Sockets } from "sb-api"

const ln = await Lnd()
const refundInvoice = await ln.receive()
const exchangeSocket = await Sockets.exchange(ln)
const tickersSub = await exchangeSocket.trades({
  duration: 10000,
  exchange: "bitfinex",
  symbol: "ETHBTC",
  refundInvoice,
  onData: data => console.log("received data", data),
  onSnapshot: snapshot => console.log("received snapshot: ", snapshot),
  onSubscriptionEnded: dataset => console.log(`got dataset with ${dataset.length} elements`) 
  //                    ^^^ dataset is the list of all your 
  //                        previously received data points
})
```

> Example Order Books data

```javascript
// snapshot
[
  {
    eventTime: 1543850299172,
    orderId: 19811509228,
    price: 3894.7,
    quantityTotal: 0.25,
  },
  // rest of elements omitted
  // for brevity
]


// data
{
  eventTime: 1541715102336,
  orderId: 18836717013,
  price: 6502.9,
  quantityTotal: 0.1691553,
}

```

```json

{  
      "uuid":"d7975109-e6d0-47ae-9c26-531d553c420b",
      "exchange":"bitfinex",
      "symbol":"BTCUSD",
      "duration":15000,
      "event":"payment received"
}

{  
   "uuid":"d7975109-e6d0-47ae-9c26-531d553c420b",
   "snapshot":[  
      {  
         "eventTime":1543850299172,
         "orderId":19811509228,
         "price":3894.7,
         "quantityTotal":0.25
      },
      ...
   ]
}

{  
      "uuid":"d7975109-e6d0-47ae-9c26-531d553c420b",
      "data":{  
         "eventTime":1541715102336,
         "orderId":18836717052,
         "price":6504.4,
         "quantityTotal":0.16911629,
      }
      "seq":622
   }{  
      "uuid":"d7975109-e6d0-47ae-9c26-531d553c420b",
      "data":{  
         "eventTime":1541715102336,
         "orderId":18836717013,
         "price":6502.9,
         "quantityTotal":0.1691553,
      }
      "seq":309
   }
...

   ```

The **Books** channel streams bids and asks for a given trading pair on given exchange. 

Field | Type | Exchanges Supporting
------| -------| --------
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"
`eventTime` | Integer | binance, bitfinex, bitstamp, gemini, coinbase 
`orderId` |  Integer |  bitfinex, bitstamp 
`price`  | Double | binance, bitfinex, coinbase, bitstamp, gemini 
`quantityTotal` | Double | binance, bitfinex, coinbase, gemini 
`quantityChange` | Double | bitstamp, gemini 
`symbol` | String |  binance, coinbase 

<aside class="warning"> We currently do not support <code>Books</code> for Kraken Spot trading.</a> </aside>


# Crypto Futures Exchange API

## Crypto Futures Exchange Endpoints

This is the paid service url **wss://api.suredbits.com/futures/v0** on mainnet.

This is the free version url **wss://test.api.suredbits.com/futures/v0** on testnet. 

## Overview

**Futures** request follow the same query structure as the **Crypto Exchange API** with one addition: you must include an `interval` request of: `monthly`, `quarterly`, `biquarterly` or `perpetual`.  

If no `interval` is requested, it will default to `perpetual` for all trading pairs except `ETHBTC` on the Bitmex exchange. That will default to `quarterly`. 


### Trading Pairs Supported 

Symbol  | Kraken   | Bitmex |
------  | :------: | :-----: |
`BTCUSD` |  Quarterly, Perpetual  | Quarterly, Perpetual, Biquarterly  |  
`ETHUSD` |  Quarterly, Perpetual  |  Perpetual     |
`ETHBTC` |         |  Quarterly     |
`LTCBTC` |         |  Quarterly     |
`LTCUSD` | Quarterly, Perpetual   |        |
`BCHUSD` | Quarterly, Perpetual   |        |
`BCHBTC` |         |   Quarterly    |
`XRPUSD` | Quarterly, Perpetual | 
`XRPBTC` | Quarterly, Perpetual  |  Quarterly
`EOSBTC` |          | Quarterly 

### Contract Rollover 

When a Futures contract ends, we will rollover the data from the now expired contract to the new one.   

You will see an updated **Snapshot** in your data feed indicating the rollover has occurred.  The rollover will be seamless and users should not see any disruption in their data stream. 

Users should also be able to see the updated contract dates in the `maturationTime` field. 

<aside class="note"> Contracts may share the same interval such as "Quarterly" on Kraken and Bitmex. However, the settlement dates of these contracts may differ due to a shorter interval contracts rolling over - such as "Monthly" on Kraken.  Thus, causing the "Quarterly" rollover date to be different on the different exchanges.</aside>


## Tickers

> Example request Tickers

```json

{  "event":"subscribe",
   "interval": "perpetual",
   "channel":"tickers",
   "symbol":"BTCUSD",
   "exchange":"kraken",
   "duration":15000,
"refundInvoice":"lnbc1pw9ff23pp55qvmh9xan5vfkf49tlmp3q80twqmk...",
   "uuid":"8c948cbb-dcc9-40c2-9bab-6384b1379f9f"
}

```

> Example Tickers data

```json

{  
   "uuid":"8c948cbb-dcc9-40c2-9bab-6384b1379f9f",
   "snapshot":[  
      {  
         "eventTime":1552661137915,
         "symbol":"BTCUSD",
         "maturationInterval":"perpetual",
         "bid":3885,
         "bidSize":72838,
         "ask":3886,
         "askSize":122,
         "markPrice":3886,
         "priceChange":1.1,
         "last":3885,
         "volume":4049778,
         "leverage":"50x",
         "premium":0,
         "index":3885.43,
         "openInterest":6053161,
         "fundingRate":2.1017787561E-8,
         "nextFundingRateTime":1552665600000,
         "fundingRatePrediction":9.695378633E-9
      }
   ]
}

{  
   "uuid":"8c948cbb-dcc9-40c2-9bab-6384b1379f9f",
   "exchange":"kraken",
   "symbol":"BTCUSD",
   "duration":15000,
   "event":"payment received"
}

{  
   "uuid":"8c948cbb-dcc9-40c2-9bab-6384b1379f9f",
   "data":{  
      "eventTime":1552661140917,
      "symbol":"BTCUSD",
      "maturationInterval":"perpetual",
      "bid":3885,
      "bidSize":72838,
      "ask":3886,
      "askSize":122,
      "markPrice":3886,
      "priceChange":1.1,
      "last":3885,
      "volume":4049778,
      "leverage":"50x",
      "premium":0,
      "index":3885.56,
      "openInterest":6053161,
      "fundingRate":2.1017787561E-8,
      "nextFundingRateTime":1552665600000,
      "fundingRatePrediction":9.695378633E-9
   },
   "seq":63599
}
...


```

The **Tickers** channel streams high level updates for given trading pairs.  See the table below for which exchanges return which fields.

Field | Type | Exchanges Supporting
------| -------| --------
`eventTime` | Integer | bitmex, kraken
`symbol` | String | bitmex, krakken
`maturationInterval`| String | bitmex, kraken 
`maturationTime`| Integer | bitmex, kraken *
`bid` | Float | bitmex, kraken
`bidSize` | Float | kraken
`ask` | Float | bitmex, kraken
`askSize`| Float | kraken
`markprice` | Float | bitmex, kraken
`priceChange`| Float | bitmex, kraken
`last`| Float | bitmex,  kraken
`low` | Float | bitmex, kraken
`high`| Float | bitmex, kraken
`volume` | Float | bitmex, kraken
`volWeightedAvePrice`| Float | bitmex, kraken
`leverage`| String | bitmex, kraken
`premium`| Float | kraken
`index`| Float | bitmex, kraken
`openInterest`| Float | bitmex, kraken
`fundingRate`| Float | bitmex, kraken **
`nextFundingRateTime`| Integer | bitmex, kraken **
`fundingRatePrediction` | Float | bitmex, kraken **

* No `maturationTime` for Perpetual contracts * 
* Only for Perpetual contracts **

## Trades

> Example Trades request 

```json
{  
   "event":"subscribe",
   "interval":"perpetual",
   "channel":"trades",
   "symbol":"BTCUSD",
   "exchange":"bitmex",
   "duration":20000,
   "refundInvoice":"lnbc1pw9ff23pp55qvmh9xan5vfkf49tlmp3q80twqmkvskatz4n9rlat4egpz3uaxsdp2v3skugrdv95kumn9wss8yetxw4hxggrfdemx76trv5xqrrss33rls5h8j2546gp26hl6n3r9u6kqq9a7jeffjsa3x9p5a9tqkwzp785haylzj45kcnnrm7sq2ynz7axrm7uzvpnwkcrtumpx92tckqgpd6trqp",
   "uuid":"1920827c-a301-45d2-8794-8868cdac55e0"
}

```

> Example Trades data

```json
{  
   "uuid":"1920827c-a301-45d2-8794-8868cdac55e0",
   "exchange":"bitmex",
   "symbol":"BTCUSD",
   "duration":20000,
   "event":"payment received"
}
{  
   "uuid":"1920827c-a301-45d2-8794-8868cdac55e0",
   "snapshot":[  
      {  
         "symbol":"BTCUSD",
         "tradeId":"451f2cda-ada6-a4c4-a66c-5662a7853324",
         "price":3971,
         "quantity":264,
         "grossValue":6648312,
         "homeNotional":0.06648312,
         "foreignNotional":264,
         "tradeTime":1552833758095,
         "marketMaker":true
      },
      {  
         "symbol":"BTCUSD",
         "tradeId":"078c64c0-e5d0-6f3d-050c-0e0ff058662f",
         "price":3971,
         "quantity":176,
         "grossValue":4432208,
         "homeNotional":0.04432208,
         "foreignNotional":176,
         "tradeTime":1552833758095,
         "marketMaker":true
      },
}
...

{  
   "uuid":"1920827c-a301-45d2-8794-8868cdac55e0",
   "data":{  
      "symbol":"BTCUSD",
      "tradeId":"39a1f9b2-4d10-b8b9-5852-6d11facf79de",
      "price":3971,
      "quantity":845,
      "grossValue":21279635,
      "homeNotional":0.21279635,
      "foreignNotional":845,
      "tradeTime":1552833768748,
      "marketMaker":true
   },
   "seq":4145
}
...

```


The **Trades** channel streams executed trades for a given trading pair.  See the table below for which exchanges returns which fields. 

Field | Type | Exchanges Supporting
------| -------| --------
`eventTime` | Integer | kraken
`symbol` | String | bitmex, kraken
`tradeId` | String | bitmex, kraken
`price` | Float | bitmex, kraken
`quantity` | Float | bitmex, kraken
`buyerId` | String | kraken
`sellerId` | String | kraken
`tradeTime` | Integer | bitmex, kraken
`marketMaker` | Boolean | bitmex, kraken
`reason` | String | kraken
`maturationTime` | String | bitmex, kraken
`grossvalue` | Integer | bitmex
`homeNotional` | Float | bitmex
`foreignNotional` | Float | bitmex


## Order Books 

> Example Books request

```json
{  "event":"subscribe",
   "interval": "quarterly",
   "channel":"books",
   "symbol":"ETHBTC",
   "exchange":"bitmex",
   "duration":15000,
"refundInvoice":"lnbc1pw9ff23pp55qvmh9xan5vfkf49tlmp3q80twqmkvskatz4n9rlat4egpz3uaxsdp2v3skugrdv95kumn9wss8yetxw4hxggrfdemx76trv5xqrrss33rls5h8j2546gp26hl6n3r9u6kqq9a7jeffjsa3x9p5a9tqkwzp785haylzj45kcnnrm7sq2ynz7axrm7uzvpnwkcrtumpx92tckqgpd6trqp",
   "uuid":"ae24b4d3-3d83-4433-8f3c-ef4322a66d62"
}

```

> Example Books data

```json

{  
   "uuid":"ae24b4d3-3d83-4433-8f3c-ef4322a66d62",
   "snapshot":[  
      {  
         "symbol":"ETHBTC",
         "maturation":1553860800000,
         "orderId":31899996636,
         "price":0.03364,
         "quantityChange":129
      },
      {  
         "symbol":"ETHBTC",
         "maturation":1553860800000,
         "orderId":31899996060,
         "price":0.0394,
         "quantityChange":22
      },
      {  
         "symbol":"ETHBTC",
         "maturation":1553860800000,
         "orderId":31899996437,
         "price":0.03563,
         "quantityChange":89
      },
...

{  
   "uuid":"ae24b4d3-3d83-4433-8f3c-ef4322a66d62",
   "data":{  
      "symbol":"ETHBTC",
      "maturation":1553860800000,
      "orderId":31899996488,
      "price":0.03512,
      "quantityChange":1009
   },
   "seq":5177
}
...
      

```

The **Books** channel streams bids and asks for a given trading pair on given exchange. 

Field | Type | Exchanges Supporting
------| -------| --------
`eventTime` | Integer | bitmex, kraken
`symbol` | String | bitmex, kraken
`maturation` | Integer | bitmex, kraken 
`orderId`| Integer | bitmex, kraken
`price` | Float | bitmex, kraken
`quantityChange`| Float | bitmex, kraken
`quantityTotal` | Float | kraken

# Historical Prices Data API

Our Historical Crypto Data REST API service allows you to query any of our supported exchanges and trading pairs for historical pricing data. 

We currently support the years 2018 and 2019.  

We currently support three time periods: `daily`, `weekly`, and `monthly`.  

For this beta release, all data is available on both mainnet and testnet. 

Mainnet address: [https://api.suredbits.com/historical/v0](https://api.suredbits.com/historical/v0)

Testnet address: [https://test.api.suredbits.com/historical/v0](https://test.api.suredbits.com/historical/v0)

## Encrypted payloads

All data server over our REST endpoints are sent to you immediately, but they are encrypted.
The decryption key is the preimage that was used to generate the invoice we sent you. Your
Lightning Client provides you with this preimage upon paying the invoice. 

### Technical details

The payloads are encrypted with AES in CFB mode, with no padding to the plaintext. The 
initialization vector (IV) is prepended to the payload, and the resulting byte sequence
is base64-encoded. When decrypting you decode the base64 string, take the first 16 bytes
as your IV and the rest as the encrypted payload. 


### Reference implementations

Reference implementations for this is available in [JavaScript](https://gist.github.com/torkelrogstad/4611d73567cdcbc40d1da144169c9b03),
[Python](https://gist.github.com/torkelrogstad/9f57c9ec2f14322a9c1ce0a863f4ad50) and 
[Scala](https://github.com/torkelrogstad/bitcoin-s/blob/21f69158de361349a3ef1abe6f94f042af144ea9/core/src/main/scala/org/bitcoins/core/crypto/AesCrypt.scala).

```javascript
import { Lnd, HistoricalRestAPI } from "sb-api"

// it's possible to pass in configuration options here, 
// if you're deviating from the default configuration.
// you can also use Eclair and c-lightning, just 
// import Eclair or CLightning instead of Lnd
const lnd = await Lnd() 

const rest = HistoricalRestAPI(lnd)

const response = await rest.call({ exchange: 'bitstamp', pair: 'BTCUSD', period: 'daily', year: 2018 })

// response: [{timestamp: Date, price: number, pair: string}, ...] 
```

### Client library

You can also use our JavaScript client library (published as 
[`sb-api`](https://www.npmjs.com/package/sb-api) on npm) which handles both
constructing the request, paying the Lightning invoice, decrypting the payload
with the preimage to the invoice and then finally returning the decrypted
data you requested. 


Parameters | Example |
---------- | -------
`exchange` |  `binance`, `coinbase`, `kraken` etc...
`pair` | `BTCUSD`, `ETHBTC`, `LTCBCH`, `XRPUSD`, etc...
`year`| `2018`, `2019` 
`period`| `daily`, `weekly`, `monthly` 


### Spot Trading Pairs Supported 

Symbol    | Binance  | Bitfinex  | Coinbase | Bitstamp | Gemini |  Kraken |
-------   | :-----:  | :-------: | :------: | :------: | :-----: | :-----:
`BTCUSDT` | &#10003; |           |         |         |         |
`ETHBTC`  | &#10003; |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`ETHUSDT` | &#10003; |           |         |         |         |
`BTCUSD`  |          |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`ETHUSD`  |          |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`LTCUSD`  |          |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;    
`LTCBTC`  | &#10003; |  &#10003; | &#10003;| &#10003;| &#10003;| &#10003;
`LTCETH`  | &#10003; |           |         |         | &#10003;|
`LTCUSDT` | &#10003; |           |         |         |         |
`LTCBCH`  |          |           |         |         | &#10003;| 
`BCHUSDT` | &#10003; |           |         |         |         | 
`BCHUSD`  |          | &#10003;  | &#10003;| &#10003;| &#10003;| &#10003;
`BCHBTC`  | &#10003; | &#10003;  | &#10003;| &#10003;| &#10003;| &#10003;
`BCHETH`  |          |           |         |         | &#10003;|
`XRPUSDT` | &#10003; |           |         |         |         |         
`XRPBTC`  | &#10003; | &#10003;  | &#10003;| &#10003;|         | &#10003; 
`XRPETH`  | &#10003; |           |         |         |         |
`XRPUSD`  |          | &#10003;  | &#10003;| &#10003;|         | &#10003;       
`EOSUSDT` | &#10003; |           |         |         |         | 
`EOSUSD`  |          | &#10003;  | &#10003;|         |         | &#10003;
`EOSBTC`  | &#10003; | &#10003;  | &#10003;|         |         | &#10003;
`EOSETH`  | &#10003; | &#10003;  |         |         |         | &#10003;

### Euro Trading Pairs Supported

Symbol | Bitfinex | Coinbase | Bitstamp | Kraken |
------ | :------: | :------: | :------: | :-----:
`BTCEUR` | &#10003;| &#10003; | &#10003; | &#10003;|
`ETHEUR` | &#10003; | &#10003; | &#10003; | &#10003; |
`EOSEUR` | &#10003; | &#10003; |          | &#10003; |
`LTCEUR` |        | &#10003; | &#10003; |  &#10003; |
`BCHEUR` |       | &#10003; | &#10003; |  &#10003; |
`XRPEUR` |       | &#10003; | &#10003; |  &#10003; |
`EURUSD` |       |          | &#10003; |        |

### Futures Trading Pairs Supported

<aside class="success">At this time, we only provide pricing data for Perpetual contracts. Historical Quartelry and Bi-Quarterly data are not available at this time. </aside>

Symbol  | Kraken   | Bitmex |
------  | :------: | :-----: |
`BTCUSD` |  Perpetual  | Perpetual|  
`ETHUSD` |  Perpetual  | Perpetual     |
`LTCUSD` | Perpetual   |        |
`BCHUSD` | Perpetual   |        |
`XRPUSD` | Perpetual | 
`XRPBTC` | Perpetual  | 



## Prices

> Example Price data

```json

[  
   {  
      "timestamp":"2019-01-14T00:00:09.000Z",
      "price":3516.07,
      "pair":"BTCUSD"
   },
   {  
      "timestamp":"2019-01-21T00:00:06.000Z",
      "price":3538.74,
      "pair":"BTCUSD"
   },
   {  
      "timestamp":"2019-01-28T00:00:05.000Z",
      "price":3533.23,
      "pair":"BTCUSD"
   },
   {  
      "timestamp":"2019-02-04T00:00:08.000Z",
      "price":3414.82,
      "pair":"BTCUSD"
   },
   {  
      "timestamp":"2019-02-11T00:00:02.000Z",
      "price":3650.37,
      "pair":"BTCUSD"
   },
   {  
      "timestamp":"2019-02-18T00:00:01.000Z",
      "price":3625.6,
      "pair":"BTCUSD"
   },
  
...
```

<aside class="success">URIs relative to https://www.suredbits.com/api/historical/v0</aside>

Method | HTTPS Request | Description
:-------: | :----------:  | :-----------:
get    |  GET /exchange/pair/year/period | Returns the pricing data for the specific `period` requested.


# NFL Data API

Our NFL API allows you to query data across `Games`, `Players`, `Team`, and `Stats`. 

Mainnet address: [https://api.suredbits.com/nfl/v0](https://api.suredbits.com/nfl/v0)

Testnet address: [https://test.api.suredbits.com/nfl/v0](https://test.api.suredbits.com/nfl/v0)

## Encrypted payloads

All data server over our REST endpoints are sent to you immediately, but they are encrypted.
The decryption key is the preimage that was used to generate the invoice we sent you. Your
Lightning Client provides you with this preimage upon paying the invoice. 

### Technical details

The payloads are encrypted with AES in CFB mode, with no padding to the plaintext. The 
initialization vector (IV) is prepended to the payload, and the resulting byte sequence
is base64-encoded. When decrypting you decode the base64 string, take the first 16 bytes
as your IV and the rest as the encrypted payload. 


### Reference implementations

Reference implementations for this is available in [JavaScript](https://gist.github.com/torkelrogstad/4611d73567cdcbc40d1da144169c9b03),
[Python](https://gist.github.com/torkelrogstad/9f57c9ec2f14322a9c1ce0a863f4ad50) and 
[Scala](https://github.com/torkelrogstad/bitcoin-s/blob/21f69158de361349a3ef1abe6f94f042af144ea9/core/src/main/scala/org/bitcoins/core/crypto/AesCrypt.scala).


### Client library

You can also use our JavaScript client library (published as 
[`sb-api`](https://www.npmjs.com/package/sb-api) on npm) which handles both
constructing the request, paying the Lightning invoice, decrypting the payload
with the preimage to the invoice and then finally returning the decrypted
data you requested. 


## Data Types 

Type | Example
----- | -------
`seasonPhase` | `Preseason`, `Regular`, `Postseason`
`teamId` | `CHI`, `NE`, `BAL`, etc.  <a href="#TeamID">See Team ID Table</a>
`firstName` | `Khalil`, `Tom`, `Saquon`, etc. 
`lastName` | `Mack` `Brady`, `Barkley`, etc. 
`retrieve` | `roster`, `schedule` 
`year` | `2018`, `2015`, `2011`, etc.
`statType` | `passing`, `rushing`, `receiving`, `defense`
`gameId` |  `2016101604`
`playerId` | `00-0027973`


## Info

Mainnnet address: [https://api.suredbits.com/nfl/v0/info] (https://api.suredbits.com/nfl/v0/info)

Testnet address: [https://test.api.suredbits.com/nfl/v0/info] (https://test.api.suredbits.com/nfl/v0/info)

Method | HTTPS Request | Description
 ------- | --------- | ------------
 get     | GET /info | Confirms connection and gives server status

## Games

> Example Games Request

> https://api.suredbits.com/nfl/v0/games/1/regular/2017


```javascript
import { Lnd, NflRestAPI } from 'sb-api'
const ln = await Lnd()

const games = await NflRestAPI(ln).games({
  week: 1,
  seasonPhase: 'regular',
  year: 2017,
})
```

> Example Games Data

```json

[
      {
      "gsisId":"2017091006",
      "gameKey":"57241",
      "startTime":"2017-09-10T17:00:00.000Z",
      "week":"NflWeek1",
      "dayOfWeek":"Sunday",
      "seasonYear":2017,
      "seasonType":"Regular",
      "finished":true,
      "homeTeam":{
        "team":"MIA",
        "score":0,
        "scoreQ1":0,
        "scoreQ2":0,
        "scoreQ3":0,
        "scoreQ4":0,
        "turnovers":0
        },
      "awayTeam":{
        "team":"TB",
        "score":0,
        "scoreQ1":0,
        "scoreQ2":0,
        "scoreQ3":0,
        "scoreQ4":0,
        "turnovers":0
      },
      "timeInserted":"2017-08-04T18:29:15.669Z",
      "timeUpdate":"2018-06-08T19:34:44.063Z",
     },
     ...
]

```

```javascript
[
  {
    gsisId: '2017091006',
    gameKey: '57241',
    startTime: '2017-09-10T17:00:00.000Z',
    week: 'NflWeek1',
    dayOfWeek: 'Sunday',
    seasonYear: 2017,
    seasonType: 'Regular',
    finished: true,
    homeTeam: {
      team: 'MIA',
      score: 0,
      scoreQ1: 0,
      scoreQ2: 0,
      scoreQ3: 0,
      scoreQ4: 0,
      turnovers: 0,
    },
    awayTeam: {
      team: 'TB',
      score: 0,
      scoreQ1: 0,
      scoreQ2: 0,
      scoreQ3: 0,
      scoreQ4: 0,
      turnovers: 0,
    },
    timeInserted: '2017-08-04T18:29:15.669Z',
    timeUpdate: '2018-06-08T19:34:44.063Z',
  },
  // more elements omitted for brevity
]
```

Mainnnet address: [https://api.suredbits.com/nfl/v0/games] (https://api.suredbits.com/nfl/v0/games)

Testnet address: [https://test.api.suredbits.com/nfl/v0games] (https://test.api.suredbits.com/nfl/v0games)

Method | HTTPS Request | Description
 ------- | --------- | ------------
get       | GET /games/week/seasonPhase | Returns data by week and season (`Preseason`, `Regualar`, or `Postseason`)
get       | GET /games/week/seasonPhase/year | Returns data by week, season and year
get       | GET /games/week/seasonPhase/year/teamId | Returns data by weak, season, year and team
get       | GET /games/week/seasonPhase/teamId | Returns data by week, season and just teamid
get       | GET /games/realtime     | Returns data for games in progress
get       | GET /games/realtime/teamId | Returns data for games in progress by team
 
## Players


> Example Players Request

> https://api.suredbits.com/nfl/v0/players/Brady/Tom

```javascript
import { Lnd, NflRestAPI } from 'sb-api'
const ln = await Lnd()

const players = await NflRestAPI(ln).players({
  firstName: 'Randy',
  lastName: 'Moss',
})
```

> Example Players Data

```json

[  
      {  
         "playerId":"00-0019596",
         "gsisName":"T.Brady",
         "fullName":"Tom Brady",
         "firstName":"Tom",
         "lastName":"Brady",
         "team":"NE",
         "position":"QB",
         "profileId":2504211,
         "profileUrl":"http://www.nfl.com/player/tombrady/2504211/profile",
         "uniformNumber":12,
         "birthDate":"8/3/1977",
         "college":"Michigan",
         "yearsPro":20,
         "height":76,
         "weight":225,
         "status":"Active"
      }
   ]

```


```javascript
[
  {
    playerId: '00-0011754',
    gsisName: 'R.Moss',
    fullName: 'Randy Moss',
    firstName: 'Randy',
    lastName: 'Moss',
    team: 'UNK',
    position: 'UNK',
    profileId: 2502220,
    profileUrl: 'http://www.nfl.com/player/randymoss/2502220/profile',
    birthDate: '2/13/1977',
    college: 'Marshall',
    yearsPro: 14,
    height: 76,
    weight: 210,
    status: 'Unknown',
  }
]
```


Mainnnet address: [https://api.suredbits.com/nfl/v0/players] (https://api.suredbits.com/nfl/v0/players)

Testnet address: [https://test.api.suredbits.com/nfl/v0/players] (https://test.api.suredbits.com/nfl/v0/players)

Method | HTTPS Request | Description
 ------- | --------- | -----------
get      | GET /players/lastName/firstName | Returns data for individual players 

## Team

> Example Team Request

> https://api.suredbits.com/nfl/v0/team/chi/schedule

```javascript
import { Lnd, NflRestAPI } from 'sb-api'
const ln = await Lnd()

const roster = await NflRestAPI(ln).roster({
  teamId: 'MIN',
})
```

> Example Team Data

```json

[
      {
        "gsisId":"2017091001",
        "gameKey":"57236",
        "startTime":"2017-09-10T170000.000Z",
        "week":"NflWeek1",
        "dayOfWeek":"Sunday",
        "seasonYear":2017,
        "seasonType":"Regular",
        "finished":true,
        "homeTeam":
      {
        "team":"CHI",
        "score":17,
        "scoreQ1":0,
        "scoreQ2":10,
        "scoreQ3":0,
        "scoreQ4":7,
        "turnovers":0
      },
    "awayTeam":
      {
        "team":"ATL",
        "score":23,
        "scoreQ1":3,
        "scoreQ2":7,
        "scoreQ3":3,
        "scoreQ4":10,
        "turnovers":1
      },
    "timeInserted":"2017-08-04T182915.669Z",
    "timeUpdate":"2018-06-08T192330.452Z",
    },
    ...
   ]

```

```javascript
[
  {
    playerId: '00-0027981',
    gsisName: 'K.Rudolph',
    fullName: 'Kyle Rudolph',
    firstName: 'Kyle',
    lastName: 'Rudolph',
    team: 'MIN',
    position: 'TE',
    profileId: 2495438,
    profileUrl: 'http://www.nfl.com/player/kylerudolph/2495438/profile',
    uniformNumber: 82,
    birthDate: '11/9/1989',
    college: 'Notre Dame',
    yearsPro: 8,
    height: 78,
    weight: 265,
    status: 'Active',
  },
  // more elements omitted for brevity
]
```

Mainnnet address: [https://api.suredbits.com/nfl/v0/team] (https://api.suredbits.com/nfl/v0/team)

Testnet address: [https://test.api.suredbits.com/nfl/v0/team] (https://test.api.suredbits.com/nfl/v0/team)

Method | HTTPS Request | Description
 ------- | --------- | ----------
 get     | GET /team/teamId/roster | Returns data by teamid for their roster
 get     | GET /team/teamId/schedule | Returns data by team id for their schedule
 get     | GET /team/teamId/roster/year | Returns data by team id for their roster by year
 get     | GET /team/teamId/schedule/year | Returns data by team id for their schedule by year

<aside class="notice">See the table below for individual team IDs. </aside>

### Team ID Table

Team Id	| City & Name | TeamID | City & Name
-------- | ----------- | ------ | ---------
ARI	| Arizona Cardinals	| LA   | Los Angeles Rams
ATL	| Atlanta Falcons	| MIA  | Miami Dolphins
BAL	| Baltimore Ravens	| MIN | Minnesota Vikings
BUF	| Buffalo Bills	NE	| NE  | New England Patriots
CAR	| Carolina Panthers	| NO | New Orleans Saints
CHI	| Chicago Bears	NYG	| NYG | New York Giants
CIN	| Cincinnati Bengals	| NYJ	| New York Jets
CLE	| Cleveland Browns	| OAK	| Oakland Raiders
DAL	| Dallas Cowboys	| PHI	| Philadelphia Eagles
DEN	| Denver Broncos	| PIT	| Pittsburgh Steelers
DET	| Detroit Lions	SD	| SD   | San Diego Chargers
GB	| Green Bay Packers	| SEA	| Seattle Seahawks
HOU	| Houston Texans	| SF	| San Francisco 49ers
IND	| Indianpolis Colts	| TB	| Tampa Bay Buccaneers
JAC	| Jacksonville Jaguars	| TEN	| Tennessee Titans
KC	| Kansas City Chiefs	| WAS	| Washington Redskins

## Stats 

> Example Stats Request

> https://api.suredbits.com/nfl/v0/stats/Brees/Drew/2017/1/regular/passing

```javascript
import { Lnd, NflRestAPI } from 'sb-api'
const ln = await Lnd()

const roster = await NflRestAPI(ln).statsById({
  gameId: '2016101604',
  playerId: '00=0027973',
  statType: 'passing',
})
```

> Example Stats Data

```json

 [
      {
        "att":37,
        "cmp":27,
        "cmpAirYds":167,
        "inCmp":10,
        "inCmpAirYds": 75,
        "passingInt":0,
        "sack":1,
        "sackYds":-7,
        "passingTds":1,
        "passingTwoPointAttempt":0,
        "passingTwoPointAttemptMade":0,
        "passingTwoPointAttemptMissed":0,
        "passingYds":291,
       },
       ...
    ]

```

```javascript
[
  {
    att: 37,
    cmp: 27,
    cmpAirYds: 167,
    inCmp: 10,
    inCmpAirYds: 75,
    passingInt: 0,
    sack: 1,
    sackYds: -7,
    passingTds: 1,
    passingTwoPointAttempt: 0,
    passingTwoPointAttemptMade: 0,
    passingTwoPointAttemptMissed: 0,
    passingYds: 291,
  }
]
```

Mainnnet address: [https://api.suredbits.com/nfl/v0/stats] (https://api.suredbits.com/nfl/v0/stats)

Testnet address: [https://test.api.suredbits.com/nfl/v0/stats] (https://test.api.suredbits.com/nfl/v0/stats)

Required field for Stats by Id

Method | HTTPS Request | Description
 ------- | --------- | ------------
get      | GET /stats/statType/gameId/playerId | Returns data for a player statistics by statistic type and individual game and player

Required fields for Stats by Name and Week

Method   | HTTPS Request | Description
 ------- | --------- | -----------
 get     | GET /stats/statType/year/week/seasonPhase/lastName/firstName | Returns statistics for a player by satistic type for specific year, week, and season by player name

Our NFL API allows you to query data across `Games`, `Players`, `Team`, and `Stats`. 

# NBA Data API

Our NBA API allows you to query data across `Games`, `Players`, `Team`, and `Stats`. 

Mainnet address: [https://api.suredbits.com/nba/v0](https://api.suredbits.com/nba/v0)

Testnet address: [https://test.api.suredbits.com/nba/v0](https://test.api.suredbits.com/nba/v0)

## Encrypted payloads

All data server over our REST endpoints are sent to you immediately, but they are encrypted.
The decryption key is the preimage that was used to generate the invoice we sent you. Your
Lightning Client provides you with this preimage upon paying the invoice. 

### Technical details

The payloads are encrypted with AES in CFB mode, with no padding to the plaintext. The 
initialization vector (IV) is prepended to the payload, and the resulting byte sequence
is base64-encoded. When decrypting you decode the base64 string, take the first 16 bytes
as your IV and the rest as the encrypted payload. 

### Client library

Coming soon.  Email us at <a href="mailto:support@suredbits.com">support@suredbits.com</a> for updates. 

## Data Types 

Type | Example
----- | -------
`teamId` | `CHI`, `LAL`, `ATL`, etc...
`firstName` | `Kevin`, `Lebron`, `Zion`, etc. 
`lastName` | `Durant`, `James`, `Williamson`, etc. 
`retrieve` | `roster`, `schedule` 
`year` | `2018`, `2017` `2016`, etc.
`month` | `2`, `6`, `10`, etc. 
`day` | `3`, `14`, `25`, etc. 
`gameId` |  `21800280`
`playerId` | `201142`

## Info

Mainnet address: [https://api.suredbits.com/nba/v0/info](https://api.suredbits.com/nba/v0/info)

Testnet address: [https://test.api.suredbits.com/nba/v0/info](https://test.api.suredbits.com/nba/v0/info)

Method | HTTPS Request | Description
 ------- | --------- | ------------
 get     | GET /info | Confirms connection and gives server status

## Games

> Example Games Request 

> https://api.suredbits.com/nba/v0/games/2018/11/24

> Example Games Request by Team Id

> https://api.suredbits.com/nba/v0/games/2016/12/20/CHI

> Example Games Data

 ```json
[
   {  
      "gameId":21800280,
      "startTime":"2018-11-25T01:00:00.000Z",
      "homeTeam":{  
      "teamID":"WAS",
      "finalScore":0
    },
      "awayTeam":{  
      "teamID":"NOP",
      "finalScore":0
    },
      "finished":false,
      "seasonPhase":"Regular",
      "year":"2018-2019"
    },
    {  
      "gameId":21800282,
      "startTime":"2018-11-25T01:00:00.000Z",
      "homeTeam":{  
      "teamID":"OKC",
      "finalScore":0
     },
       "awayTeam":{  
       "teamID":"DEN",
       "finalScore":0
     },
       "finished":false,
       "seasonPhase":"Regular",
       "year":"2018-2019"
     },
     ...
 ]
 ```

Mainnet address: [https://api.suredbits.com/nba/v0/games](https://api.suredbits.com/nba/v0/games)

Testnet address: [https://test.api.suredbits.com/nba/v0/games](https://test.api.suredbits.com/nba/v0/games)

Method | HTTPS Request | Description
 ------- | --------- | ------------
 get     |  GET games/year/month/day | Returns data for games on that scheduled for that date. 
 get     |  GET games/year/month/day/teamId | Returns data for games played by a specific team on that date.  

<aside class="warning">Due to inconsistencies in how NBA publishes game start times, some start times may be inaccurate.</aside>

## Players

> Example Players Request

> https://api.suredbits.com/nba/v0/players/Kevin/Durant

```json
[  
    {  
       "playerId":201142,
       "firstName":"Kevin",
       "lastName":"Durant",
       "fullName":"Kevin Durant",
       "team":"GSW",
       "profileUrl":"",
       "birthDate":"2018-10-19T11:43:30.426Z",
       "status":"Active",
       "rookieYear":2007,
       "lastYear":2018
    }
]


```

Mainnet address: [https://api.suredbits.com/nba/v0/players](https://api.suredbits.com/nba/v0/players)

Testnet address: [https://test.api.suredbits.com/nba/v0/players](https://test.api.suredbits.com/nba/v0/players)

Method | HTTPS Request | Description
 ------- | --------- | ------------
get      | GET players/lastName/firstName | Returns biographical information for a specific player. 


## Team

> Example Team Roster Request 

> https://api.suredbits.com/nba/v0/team/DEN/roster

```json
[ 
   { 
      "playerId":202918,
      "firstName":"Xavier",
      "lastName":"Silas",
      "fullName":"Xavier Silas",
      "team":"DEN",
      "profileUrl":"",
      "birthDate":"2018-10-14T16:18:10.918Z",
      "status":"Active",
      "rookieYear":2011,
      "lastYear":2018
   },
   ...
]
```

> Example Team Schedule Request 

> https://api.suredbits.com/nba/v0/team/CHI/schedule

> Example Team Schedule Data

```json
[  
    {  
       "gameId":21600073,
       "startTime":"2016-11-05T00:00:00.000Z",
       "homeTeam":{  
       "teamID":"CHI",
       "finalScore":104
     },
       "awayTeam":{  
       "teamID":"NYK",
       "finalScore":117
     },
       "finished":true,
       "seasonPhase":"Regular",
       "year":"2016-2017",
     }
]

```

Mainnet address: [https://api.suredbits.com/nba/v0/team](https://api.suredbits.com/nba/v0/team)

Testnet address: [https://test.api.suredbits.com/nba/v0/team](https://test.api.suredbits.com/nba/v0/team)

Method | HTTPS Request | Description
 ------- | --------- | ------------
get      | GET team/teamId/roster | Returns data for a specific team's roster for current year.
get      | GET team/teamId/schedule | Returns data for a specific team's schedule for current year. 
get      | GET team/teamId/roster/season | Returns data for a specific team's roster for specific year. 
get      | GET team/teamId/schedule/season | Returns data for a specific team's schedule for a specific year. 

### Team Ids

| Team Id | Team                   | Team ID | Team                   |
| ------- | ---------------------- | ------- | ---------------------- |
| ATL     | Atlanta Hawks          | PHI     | Philadelphia 76ers     |
| MIA     | Miami Heat             | DET     | Detroit Pistons        |
| BKN     | Brooklyn Nets          | PHX     | Phoenix Suns           |
| MIL     | Milwaukee Bucks        | GSW     | Golden State Warriors  |
| BOS     | Boston Celtics         | POR     | Portland Trail Blazers |
| MIN     | Minnesota Timberwolves | HOU     | Houston Rockets        |
| CHA     | Charlotte Hornets      | SAC     | Sacramento Kings       |
| NOP     | New Orleans Pelicans   | IND     | Indiana Pacers         |
| CHI     | Chicago Bulls          | SAS     | San Antonio Spurs      |
| NYK     | New York Knicks        | LAC     | Los Angeles Clippers   |
| CLE     | Cleveland Cavaliers    | TOR     | Toronto Raptors        |
| OKC     | Oklahoma City Thunder  | LAL     | Los Angeles Lakers     |
| DAL     | Dallas Mavericks       | UTA     | Utah Jazz              |
| ORL     | Orlando Magic          | MEM     | Memphis Grizzlies      |
| DEN     | Denver Broncos         | WAS     | Washington Wizards     |

## Stats

> Example Stats Request

> https://api.suredbits.com/nba/v0/stats/21600854/201142

> Example Player Stats Data (Kevin Durant)

```json
[  
    {  
       "playerId":201142,
       "min":0,
       "fgm":0,
       "fga":0,
       "tpm":0,
       "tpa":0,
       "ftm":0,
       "fta":0,
       "plusminus":0,
       "off":0,
       "deff":0,
       "tot":0,
       "ast":0,
       "pf":0,
       "st":0,
       "to":0,
       "bs":0,
       "pts":0
    }
]

```

Mainnet address: [https://api.suredbits.com/nba/v0/stats](https://api.suredbits.com/nba/v0/stats)

Testnet address: [https://test.api.suredbits.com/nba/v0/stats](https://test.api.suredbits.com/nba/v0/stats)

Method | HTTPS Request | Description
 ------- | --------- | ------------
 get     | GET stats/gameId/playerId | Returns data about individual player by `gameId` and `playerId`.
 get     | GET stats/lastName/firstName/year/month/day | Returns data by individual player by `firstName` and `lastName`.

# NFL Data Websocket (Deprecated)

## NFL Websocket Endpoints

This is the paid service url **wss://api.suredbits.com/nfl/v0** on mainnet.

This is the free service url **wss://test.api.suredbits.com/nfl/v0** on testnet.

## Info

> Example request

```json
{
   "channel": "info", 
  "uuid": "d7975109-e6d0-47ae-9c26-531d553c420b"
}
```
```javascript 

import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const info = await nfl.info()
```

This provides a check and confirmation on the status of the API. 

> Example data

```json
{
  "uuid": "1771601c-0fe8-4387-b2ce-be9a0abe1356",
  "data":
      {
        "version":"8",
        "lastRosterDownload":"2018-08-13T17:07:53.668Z",
        "seasonType":"Preseason",
        "seasonYear":2018,
        "week":"NflPreSeasonWeek1"
       }
 }
```

```javascript
{
  version: '8',
  lastRosterDownload: '2018-08-13T17:07:53.668Z',
  seasonType: 'Preseason',
  seasonYear: 2018,
  week: 'NflPreSeasonWeek1'
}
```

## Games

> Example request Games

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const games = await nfl.games({ week: 1, seasonPhase: 'Regular', year: 2017 })
```

```json
{
  "channel":"games", 
  "week":1, 
  "seasonPhase" : "Regular", 
  "year" : 2017, 
  "uuid": "8ccbd2d9-65aa-401e-a056-44d543544d47"
}
```


> Example of Games data

```javascript
[
  {
    gsisId: '2017091006',
    gameKey: '57241',
    startTime: '2017-09-10T17:00:00.000Z',
    week: 'NflWeek1',
    dayOfWeek: 'Sunday',
    seasonYear: 2017,
    seasonType: 'Regular',
    finished: true,
    homeTeam: {
      team: 'MIA',
      score: 0,
      scoreQ1: 0,
      scoreQ2: 0,
      scoreQ3: 0,
      scoreQ4: 0,
      turnovers: 0,
    },
    awayTeam: {
      team: 'TB',
      score: 0,
      scoreQ1: 0,
      scoreQ2: 0,
      scoreQ3: 0,
      scoreQ4: 0,
      turnovers: 0,
    },
    timeInserted: '2017-08-04T18:29:15.669Z',
    timeUpdate: '2018-06-08T19:34:44.063Z',
  },
  // more elements omitted for brevity
]
```

```json
 {
   "uuid": "8ccbd2d9-65aa-401e-a056-44d543544d47",
   "data":
    [
      {
      "gsisId":"2017091006",
      "gameKey":"57241",
      "startTime":"2017-09-10T17:00:00.000Z",
      "week":"NflWeek1",
      "dayOfWeek":"Sunday",
      "seasonYear":2017,
      "seasonType":"Regular",
      "finished":true,
      "homeTeam":{
        "team":"MIA",
        "score":0,
        "scoreQ1":0,
        "scoreQ2":0,
        "scoreQ3":0,
        "scoreQ4":0,
        "turnovers":0
        },
      "awayTeam":{
        "team":"TB",
        "score":0,
        "scoreQ1":0,
        "scoreQ2":0,
        "scoreQ3":0,
        "scoreQ4":0,
        "turnovers":0
      },
      "timeInserted":"2017-08-04T18:29:15.669Z",
      "timeUpdate":"2018-06-08T19:34:44.063Z",
     },
     ...
    ]
 }
```

The **Games** channel returns data for specific games. 

**Completed and upcoming games**

The available fields to query data from completed and upcoming NFL games are as follows:

**Required fields**

Field | Type | Example
------ | ------- | ------
`uuid` | String | "123e4567-e89b-12d3-a456-426655440000" 
`week` | Integer |  1, 2, 3 etc...
`seasonPhase` | String |   Preaseason, Regular, or Postseason 


**Optional fields**

Field | Type | Example
------ | ------- | --------
`year` | Integer |  2009, 2010, 2011, etc. 
`teamId` | String  |  CHI, MIN, GB, MIA etc. <a href="#TeamID">See Team ID Table</a>

**Live games**

You can also query for games that are currently playing. The available fields are as follows: 

**Required fields**

Field | Type | Example
------ | ------- | ------
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"
`realtime` | Boolean (true) | true 

**Optional fields**

Field | Type | Example
------ | ------- | ------
`teamId` | String  |  CHI, MIN, GB, MIA etc. <a href="#TeamID">See Team ID Table</a>


## Players

> Example request Players

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const players = await nfl.players({ firstName: 'Randy', lastName: 'Moss' })
```

```json
{
  "channel":"players", 
  "lastName" : "Moss", 
  "firstName" : "Randy", 
  "uuid": "dfd2a7d4-3a36-4624-96c4-80f0c166d447ok"
}
```

> Example Players data

```javascript
[
  {
    playerId: '00-0011754',
    gsisName: 'R.Moss',
    fullName: 'Randy Moss',
    firstName: 'Randy',
    lastName: 'Moss',
    team: 'UNK',
    position: 'UNK',
    profileId: 2502220,
    profileUrl: 'http://www.nfl.com/player/randymoss/2502220/profile',
    birthDate: '2/13/1977',
    college: 'Marshall',
    yearsPro: 14,
    height: 76,
    weight: 210,
    status: 'Unknown',
  }
]
```

```json

{  
   "uuid":"c8aa064c-51d9-4910-ab2d-add823bce374",
   "data":[  
      {  
         "playerId":"00-0011754",
         "gsisName":"R.Moss",
         "fullName":"Randy Moss",
         "firstName":"Randy",
         "lastName":"Moss",
         "team":"UNK",
         "position":"UNK",
         "profileId":2502220,
         "profileUrl":"http://www.nfl.com/player/randymoss/2502220/profile",
         "birthDate":"2/13/1977",
         "college":"Marshall",
         "yearsPro":14,
         "height":76,
         "weight":210,
         "status":"Unknown"
      }
   ]
}
```

  

The **Players** channel returns data for particular players by `name`.  

The required fields to request NFL Player data are as follows: 

**Required Fields**

Field | Type | Example
------ | ----- | -----
`uuid` | String | "123e4567-e89b-12d3-a456-426655440000"
`firstName` | String |  Randy 
`lastName` | String |  Moss 


## Team

> Example request Rosters

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const roster = await nfl.roster({ teamId: 'MIN' })
```

```json

{
  "channel": "team", 
  "teamId": "MIN", 
  "retrieve": "roster", 
  "uuid": "db69a9d5-13c3-42a0-958a-623630a0fc81"
}

```

> Example request Rosters in Year

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const roster = await nfl.roster({ teamId: 'MIN', year: 2018 }

```

```json
{
  "channel": "team", 
  "teamId": "MIN", 
  "retrieve": "schedule", 
  "year": 2018, 
  "uuid": "[uuid]"
}
```

> Example of Roster data

```javascript
[
  {
    playerId: '00-0027981',
    gsisName: 'K.Rudolph',
    fullName: 'Kyle Rudolph',
    firstName: 'Kyle',
    lastName: 'Rudolph',
    team: 'MIN',
    position: 'TE',
    profileId: 2495438,
    profileUrl: 'http://www.nfl.com/player/kylerudolph/2495438/profile',
    uniformNumber: 82,
    birthDate: '11/9/1989',
    college: 'Notre Dame',
    yearsPro: 8,
    height: 78,
    weight: 265,
    status: 'Active',
  },
  // more elements omitted for brevity
]
```

```json
{
  "uuid":"db69a9d5-13c3-42a0-958a-623630a0fc81",
  "data":
    [
      {
        "playerId":"00-0027981",
        "gsisName":"K.Rudolph",
        "fullName":"Kyle Rudolph",
        "firstName":"Kyle",
        "lastName":"Rudolph",
        "team":"MIN",
        "position":"TE",
        "profileId":2495438,
        "profileUrl":"http://www.nfl.com/player/kylerudolph/2495438/profile",
        "uniformNumber":82,
        "birthDate":"11/9/1989",
        "college":"Notre Dame",
        "yearsPro":8,"height":78,
        "weight":265,
        "status":"Active",
       },
       ...
    ]
  }
```
  
> Example request Schedules
  
```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const schedule = await nfl.schedule({ teamId: 'CHI' })
```

```json
{
  "channel": "team", 
  "teamId": "CHI", 
  "retrieve": "schedule", 
  "uuid": "ede60177-f218-40ff-8fde-605f29a8bfce"
}
```


>Example of Schedule data

```javascript
[
  {
    gsisId: '2017091001',
    gameKey: '57236',
    startTime: '2017-09-10T170000.000Z',
    week: 'NflWeek1',
    dayOfWeek: 'Sunday',
    seasonYear: 2017,
    seasonType: 'Regular',
    finished: true,
    homeTeam: {
      team: 'CHI',
      score: 17,
      scoreQ1: 0,
      scoreQ2: 10,
      scoreQ3: 0,
      scoreQ4: 7,
      turnovers: 0,
    },
    awayTeam: {
      team: 'ATL',
      score: 23,
      scoreQ1: 3,
      scoreQ2: 7,
      scoreQ3: 3,
      scoreQ4: 10,
      turnovers: 1,
    },
    timeInserted: '2017-08-04T182915.669Z',
    timeUpdate: '2018-06-08T192330.452Z',
  },
  // more elements omitted for brevity
]
```

```json
 {
   "uuid": "ede60177-f218-40ff-8fde-605f29a8bfce",
   "data":
    [
      {
        "gsisId":"2017091001",
        "gameKey":"57236",
        "startTime":"2017-09-10T170000.000Z",
        "week":"NflWeek1",
        "dayOfWeek":"Sunday",
        "seasonYear":2017,
        "seasonType":"Regular",
        "finished":true,
        "homeTeam":
      {
        "team":"CHI",
        "score":17,
        "scoreQ1":0,
        "scoreQ2":10,
        "scoreQ3":0,
        "scoreQ4":7,
        "turnovers":0
      },
    "awayTeam":
      {
        "team":"ATL",
        "score":23,
        "scoreQ1":3,
        "scoreQ2":7,
        "scoreQ3":3,
        "scoreQ4":10,
        "turnovers":1
      },
    "timeInserted":"2017-08-04T182915.669Z",
    "timeUpdate":"2018-06-08T192330.452Z",
    },
    ...
   ]
 }
```

The **Team** channel returns data for `roster` or `schedule` or a given NFL team.


The required fields to request NFL Team & Roster data are as follows:

**Required fields** 

Field | Type | Example 
------ | ----- | ------
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000" 
`teamId` | String |  CHI, MIN, MIA  etc.
`retrieve` | String |  roster or schedule 

**Optional Fields**

Field | Type | Example
------| ----- | ------
`year` | Integer | 2018,  2015, 2011, etc. 

NOTE: the `year` field defaults to current year. 

<h3 id="TeamID"> Team ID Table</h3>

Team Id	| City & Name | TeamID | City & Name
-------- | ----------- | ------ | ---------
ARI	| Arizona Cardinals	| LA   | Los Angeles Rams
ATL	| Atlanta Falcons	| MIA  | Miami Dolphins
BAL	| Baltimore Ravens	| MIN | Minnesota Vikings
BUF	| Buffalo Bills	NE	| NE  | New England Patriots
CAR	| Carolina Panthers	| NO | New Orleans Saints
CHI	| Chicago Bears	NYG	| NYG | New York Giants
CIN	| Cincinnati Bengals	| NYJ	| New York Jets
CLE	| Cleveland Browns	| OAK	| Oakland Raiders
DAL	| Dallas Cowboys	| PHI	| Philadelphia Eagles
DEN	| Denver Broncos	| PIT	| Pittsburgh Steelers
DET	| Detroit Lions	SD	| SD   | San Diego Chargers
GB	| Green Bay Packers	| SEA	| Seattle Seahawks
HOU	| Houston Texans	| SF	| San Francisco 49ers
IND	| Indianpolis Colts	| TB	| Tampa Bay Buccaneers
JAC	| Jacksonville Jaguars	| TEN	| Tennessee Titans
KC	| Kansas City Chiefs	| WAS	| Washington Redskins


## Stats 

> Example request Stats #1

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const stats = await nfl.statsById({ 
  gameId: '2016101604', 
  playerId: '00=0027973', 
  statType: 'passing' 
})
```

```json
{
  "channel":"stats", 
  "statType" : "passing", 
  "gameId" : "2016101604", 
  "playerId" : "00-0027973",
  "uuid": "4312144f-a0a9-4c23-bfd5-01405813c2c9"
}
```
> Example request Stats #2

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nfl = await Sockets.nfl(ln)
const stats = await nfl.statsByNameAndWeek({
  firstName: 'Drew',
  lastName: 'Brees',
  seasonPhase: 'Regular',
  statType: 'passing',
  week: 1,
  year: 2017,
})
```
```json
{
    "channel":"stats", 
    "lastName" : "Brees", 
    "firstName" : "Drew", 
    "year": 2017, 
    "week" : 1, 
    "seasonPhase" : "Regular", 
    "statType" : "passing",
    "uuid": "4312144f-a0a9-4c23-bfd5-01405813c2c9"
}

```

> Example of Stats data

```javascript
[
  {
    att: 37,
    cmp: 27,
    cmpAirYds: 167,
    inCmp: 10,
    inCmpAirYds: 75,
    passingInt: 0,
    sack: 1,
    sackYds: -7,
    passingTds: 1,
    passingTwoPointAttempt: 0,
    passingTwoPointAttemptMade: 0,
    passingTwoPointAttemptMissed: 0,
    passingYds: 291,
  }
]
```

```json
{
  "uuid":"4312144f-a0a9-4c23-bfd5-01405813c2c9",
  "data":
    [
      {
        "att":37,
        "cmp":27,
        "cmpAirYds":167,
        "inCmp":10,
        "inCmpAirYds": 75,
        "passingInt":0,
        "sack":1,
        "sackYds":-7,
        "passingTds":1,
        "passingTwoPointAttempt":0,
        "passingTwoPointAttemptMade":0,
        "passingTwoPointAttemptMissed":0,
        "passingYds":291,
       },
       ...
    ]
}

```

The **Stats** channel returns data for an individual `player`or `game`.

To query by `gameId` and `playerId`:

**Required field for Stats by Id**


Field | Type | Example
------ | ----- | -------
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"
`channel` | String| stats
`statType` | String | passing, rushing, receiving, defense
`gameId` | String | 2016101604
`playerId` | String | 00-0027973


To query by `name` and `week`:

**Required fields for Stats by Name and Week**

Field | Type | Example
------ | ------- | -----
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"
`channel` | String | stats
`statType` | String | passing, rushing, receiving, defense
`year` | Integer | 2016, 2017
`week` | Integer  | 1, 2... 
`seasonPhase` | String  | Preseason, Regular, Postseason* 
`firstName`  | String | Drew
`lastName` | String | Brees

# NBA Data Websocket (Deprecated)

## NBA Websocket Endpoints

This is the paid service url **wss://api.suredbits.com/nba/v0** on mainnet.

This is the free version url **wss://test.api.suredbits.com/nba/v0** on testnet. 

## Info

> Example request Info

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const info = await nba.info()
```

```json
{
  "channel": "info", 
  "uuid": "123e4567-e89b-12d3-a456-426655440000"
}
```

> Example of Info data

```javascript
{
  seasonYear: '2018-2019',
  seasonPhase: 'Regular',
  version: 0,
  lastUpdated: Date('2018-11-15T21:58:50.490Z'),
}
```

```json
{  
   "uuid":"123e4567-e89b-12d3-a456-426655440000",
   "data":{  
      "seasonYear":"2018-2019",
      "seasonPhase":"Regular",
      "version":0,
      "lastUpdated":"2018-11-15T21:58:50.490Z"
      
    }
}
```

The `Info` channel returns high level information of the current status of the `NBA` endpoint. 

Field | Type | Example
------ | ----- | -------
`uuid` | String |  "123e4567-e89b-12d3-a456-426655440000" 


## Games

> Example request Games

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const games = await nba.games({ year: 2018, month: 11, day: 24 })
```

```json
{
  "channel": "games", 
  "year": 2018, 
  "month": 11, 
  "day": 24, 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```

> Example request Games with TeamId

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const games = await nba.games({ year: 2016, month: 12, day: 20, teamId: 'CHI' })
```

```json
{
  "channel": "games", 
  "year": 2016, 
  "month": 12, 
  "day": 20, 
  "teamId": "CHI", 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```

> Example Games data

```javascript
[
  {
    gameId: 21800280,
    startTime: Date('2018-11-25T01:00:00.000Z'),
    homeTeam: {
      teamID: 'WAS',
      finalScore: 0,
    },
    awayTeam: {
      teamID: 'NOP',
      finalScore: 0,
    },
    finished: false,
    seasonPhase: 'Regular',
    year: '2018-2019',
  },
  {
    gameId: 21800282,
    startTime: Date('2018-11-25T01:00:00.000Z'),
    homeTeam: {
      teamID: 'OKC',
      finalScore: 0,
    },
    awayTeam: {
      teamID: 'DEN',
      finalScore: 0,
    },
    finished: false,
    seasonPhase: 'Regular',
    year: '2018-2019',
  },
  {
    gameId: 21800285,
    startTime: Date('2018-11-25T01:30:00.000Z'),
    homeTeam: {
      teamID: 'GSW',
      finalScore: 0,
    },
    awayTeam: {
      teamID: 'SAC',
      finalScore: 0,
    },
    finished: false,
    seasonPhase: 'Regular',
    year: '2018-2019',
  },
  {
    gameId: 21800284,
    startTime: Date('2018-11-25T01:30:00.000Z'),
    homeTeam: {
      teamID: 'MIL',
      finalScore: 0,
    },
    awayTeam: {
      teamID: 'SAS',
      finalScore: 0,
    },
    finished: false,
    seasonPhase: 'Regular',
    year: '2018-2019',
  },
  {
    gameId: 21800279,
    startTime: Date('2018-11-25T00:30:00.000Z'),
    homeTeam: {
      teamID: 'CLE',
      finalScore: 0,
    },
    awayTeam: {
      teamID: 'HOU',
      finalScore: 0,
    },
    finished: false,
    seasonPhase: 'Regular',
    year: '2018-2019',
  },
  {
    gameId: 21800281,
    startTime: Date('2018-11-25T01:00:00.000Z'),
    homeTeam: {
      teamID: 'MIN',
      finalScore: 0,
    },
    awayTeam: {
      teamID: 'CHI',
      finalScore: 0,
    },
    finished: false,
    seasonPhase: 'Regular',
    year: '2018-2019',
  },
]
```

```json
{  
   "uuid":"3f4f2853-e84f-4a29-b807-8a471e59ca44",
   "data":[  
      {  
         "gameId":21800280,
         "startTime":"2018-11-25T01:00:00.000Z",
         "homeTeam":{  
            "teamID":"WAS",
            "finalScore":0
         },
         "awayTeam":{  
            "teamID":"NOP",
            "finalScore":0
         },
         "finished":false,
         "seasonPhase":"Regular",
         "year":"2018-2019"
      },
      {  
         "gameId":21800282,
         "startTime":"2018-11-25T01:00:00.000Z",
         "homeTeam":{  
            "teamID":"OKC",
            "finalScore":0
         },
         "awayTeam":{  
            "teamID":"DEN",
            "finalScore":0
         },
         "finished":false,
         "seasonPhase":"Regular",
         "year":"2018-2019"
      },
      {  
         "gameId":21800285,
         "startTime":"2018-11-25T01:30:00.000Z",
         "homeTeam":{  
            "teamID":"GSW",
            "finalScore":0
         },
         "awayTeam":{  
            "teamID":"SAC",
            "finalScore":0
         },
         "finished":false,
         "seasonPhase":"Regular",
         "year":"2018-2019"
      },
      {  
         "gameId":21800284,
         "startTime":"2018-11-25T01:30:00.000Z",
         "homeTeam":{  
            "teamID":"MIL",
            "finalScore":0
         },
         "awayTeam":{  
            "teamID":"SAS",
            "finalScore":0
         },
         "finished":false,
         "seasonPhase":"Regular",
         "year":"2018-2019"
      },
      {  
         "gameId":21800279,
         "startTime":"2018-11-25T00:30:00.000Z",
         "homeTeam":{  
            "teamID":"CLE",
            "finalScore":0
         },
         "awayTeam":{  
            "teamID":"HOU",
            "finalScore":0
         },
         "finished":false,
         "seasonPhase":"Regular",
         "year":"2018-2019"
      },
      {  
         "gameId":21800281,
         "startTime":"2018-11-25T01:00:00.000Z",
         "homeTeam":{  
            "teamID":"MIN",
            "finalScore":0
         },
         "awayTeam":{  
            "teamID":"CHI",
            "finalScore":0
         },
         "finished":false,
         "seasonPhase":"Regular",
         "year":"2018-2019"
      }
   ]
}
```

The **Games** channel returns statistics about specific games played.  

**Completed and upcoming games**

The available fields to query data from completed and upcoming NBA games are as follows:

**Required Fields**

Field | Type | Example
------ | ----- | -------
`uuid` | String | "123e4567-e89b-12d3-a456-426655440000"
`channel` | String |  games 
`year` | Integer  | 2016, 2017 and 2018 
`month` | Integer  | 3, 8, 12 etc..
`day` | Integer |  Follows typical calendar convention: 2, 17, 28, etc...

<aside class="notice">NOTE: We only support from year 2016 to current. </aside>

To search for a game by a specific team, add an optional field for `teamId`

**Optional fields**

| Field                                   | Type   | Example                                                                                             |
| --------------------------------------- | ------ | --------------------------------------------------------------------------------------------------- |
| `teamId` | String | ATL, CLE, PHX, LAC etc. <a href="#NBATeamID">See Team ID Table</a> |

**Live games**
You can also query for games that are currently playing. The available fields are as follows: 

**Required fields**

| Field                                      | Type           | Example                                                                 |
| ------------------------------------------ | -------------- | ----------------------------------------------------------------------- |
| `uuid` | String         | "123e4567-e89b-12d3-a456-426655440000" 
| `realtime` | Boolean (true) | true                                  |

**Optional fields**

| Field                                   | Type   | Example                                                                                             |
| --------------------------------------- | ------ | --------------------------------------------------------------------------------------------------- |
| `teamId` | String | ATL, CLE, PHX, LAC etc. <a href="#NBATeamID">See Team ID Table</a> |



## Players

> Example request Players

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const players = await nba.players({ firstName: 'Kevin', lastName: 'Durant' }
```

```json
{
  "channel": "players", 
  "lastName": "Durant", 
  "firstName": "Kevin", 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```

> Example Players data (Kevin Durant)

```javascript
[
  {
    playerId: 201142,
    firstName: 'Kevin',
    lastName: 'Durant',
    fullName: 'Kevin Durant',
    team: 'GSW',
    profileUrl: '',
    birthDate: Date('2018-10-19T11:43:30.426Z'),
    status: 'Active',
    rookieYear: 2007,
    lastYear: 2018,
  },
]
```

```json
{  
   "uuid":"3f4f2853-e84f-4a29-b807-8a471e59ca44",
   "data":[  
      {  
         "playerId":201142,
         "firstName":"Kevin",
         "lastName":"Durant",
         "fullName":"Kevin Durant",
         "team":"GSW",
         "profileUrl":"",
         "birthDate":"2018-10-19T11:43:30.426Z",
         "status":"Active",
         "rookieYear":2007,
         "lastYear":2018
      }
   ]
}
```

The **Players** channel returns biographical information about specific players. For individual player statistics, see the **Stats** channel 

**Required Fields**

| Field                                      | Type   | Example                                                                 |
| ------------------------------------------ | ------ | ----------------------------------------------------------------------- |
| `uuid`  | String | "123e4567-e89b-12d3-a456-426655440000"  |
| `channel` | String |  players                                 |
| `firstName` | String |  Kevin                                   |
| `lastName` | String |  Durant                                 |


## Team

> Example request for Roster

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const roster = await nba.roster({ teamId: 'DEN' }
```

```json
{
  "channel": "team", 
  "retrieve": "roster",
  "teamId": "DEN", 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```
> Example request with season

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const roster = await nba.roster({ season: '2016-2017', teamId: 'GSW' })
```

```json
{
  "channel": "team", 
  "retrieve": "schedule", 
  "teamId": "GSW",
  "season": "2016-2017", 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```
> Example request for Schedule 

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const schedule = await nba.schedule({ teamId: 'CHI' })
```

```json
{
  "channel": "team", 
  "teamId": "CHI",
  "retrieve": "schedule", 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```

> Example of team Schedule (Chicago Bulls)

```javascript
[
  {
    gameId: 21600073,
    startTime: Date('2016-11-05T00:00:00.000Z'),
    homeTeam: {
      teamID: 'CHI',
      finalScore: 104,
    },
    awayTeam: {
      teamID: 'NYK',
      finalScore: 117,
    },
    finished: true,
    seasonPhase: 'Regular',
    year: '2016-2017',
  }, 
  // more elements omitted for brevity
]
```

```json
{  
   "uuid":"3f4f2853-e84f-4a29-b807-8a471e59ca44",
   "data":[  
      {  
         "gameId":21600073,
         "startTime":"2016-11-05T00:00:00.000Z",
         "homeTeam":{  
            "teamID":"CHI",
            "finalScore":104
         },
         "awayTeam":{  
            "teamID":"NYK",
            "finalScore":117
         },
         "finished":true,
         "seasonPhase":"Regular",
         "year":"2016-2017",
      }
   ]
}
...

```
The **Teams** channel returns information such as `rosters` or `schedules` for specific teams.  

**Required Fields**

| Field                                     | Type   | Example                                                                                                                  |
| ----------------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------ |
| `uuid` | String | "123e4567-e89b-12d3-a456-426655440000"                                                 |
| `channel` | String | teams                                                                                    |
| `teamId` | String | CHI, LAC, MIA, etc... |
| `retrieve` | String | roster or schedule                                     |

**Optional Fields**

| Field                                   | Type   | Example                                    |
| --------------------------------------- | ------ | ------------------------------------------ |
| `season` | String | 2016-2017 |


<h3 id="NBATeamID"> Team ID Table</h3>

| Team ID | Team                   | Team ID | Team                   |
| ------- | ---------------------- | ------- | ---------------------- |
| ATL     | Atlanta Hawks          | PHI     | Philadelphia 76ers     |
| MIA     | Miami Heat             | DET     | Detroit Pistons        |
| BKN     | Brooklyn Nets          | PHX     | Phoenix Suns           |
| MIL     | Milwaukee Bucks        | GSW     | Golden State Warriors  |
| BOS     | Boston Celtics         | POR     | Portland Trail Blazers |
| MIN     | Minnesota Timberwolves | HOU     | Houston Rockets        |
| CHA     | Charlotte Hornets      | SAC     | Sacramento Kings       |
| NOP     | New Orleans Pelicans   | IND     | Indiana Pacers         |
| CHI     | Chicago Bulls          | SAS     | San Antonio Spurs      |
| NYK     | New York Knicks        | LAC     | Los Angeles Clippers   |
| CLE     | Cleveland Cavaliers    | TOR     | Toronto Raptors        |
| OKC     | Oklahoma City Thunder  | LAL     | Los Angeles Lakers     |
| DAL     | Dallas Mavericks       | UTA     | Utah Jazz              |
| ORL     | Orlando Magic          | MEM     | Memphis Grizzlies      |
| DEN     | Denver Broncos         | WAS     | Washington Wizards     |


## Stats 

> Example request Stats by ID

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const stats = await nba.statsById({ gameId: '21600854', playerId: '201142' }
```

```json
{
  "channel": "stats", 
  "gameId": "21600854", 
  "playerId": "201142", 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```

> Example request for Stats by Name

```javascript
import { Lnd, Sockets } from 'sb-api'
const ln = await Lnd()

const nba = await Sockets.nba(ln)
const stats = await nba.statsByName({ 
  firstName: 'Kevin', 
  lastName: 'Durant', 
  year: 2017, 
  month: 12, 
  day: 12 
})
```

```json
{
  "channel": "stats", 
  "lastName": "Durant", 
  "firstName": "Kevin", 
  "year": 2017, 
  "month": 12, 
  "day": 12, 
  "uuid": "3f4f2853-e84f-4a29-b807-8a471e59ca44"
}
```

> Example of player Stats data (Kevin Durant)

```javascript
[
  {
    playerId: 201142,
    min: 0,
    fgm: 0,
    fga: 0,
    tpm: 0,
    tpa: 0,
    ftm: 0,
    fta: 0,
    plusminus: 0,
    off: 0,
    deff: 0,
    tot: 0,
    ast: 0,
    pf: 0,
    st: 0,
    to: 0,
    bs: 0,
    pts: 0,
  }
]
```

```json
{  
   "uuid":"3f4f2853-e84f-4a29-b807-8a471e59ca44",
   "data":[  
      {  
         "playerId":201142,
         "min":0,
         "fgm":0,
         "fga":0,
         "tpm":0,
         "tpa":0,
         "ftm":0,
         "fta":0,
         "plusminus":0,
         "off":0,
         "deff":0,
         "tot":0,
         "ast":0,
         "pf":0,
         "st":0,
         "to":0,
         "bs":0,
         "pts":0
      }
   ]
}
```

The **Stats** channel returns data for individual players and allows you to query by `gameId`, `playerId` or by specific player `name`.

**Required Fields for Stats by Id**

Field | Type | Example 
------ | ------ | ------
`uuid`  | String | "123e4567-e89b-12d3-a456-426655440000" 
`channel` | String | stats 
`gameId` | String  | "21600854"
`playerId` | String | "201142"


**Required Field for Stats by Name**

| Field                                      | Type    | Example                                                                                                                                                   |
| ------------------------------------------ | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `uuid`   | String  | "123e4567-e89b-12d3-a456-426655440000"                                                                                   |
| `channel`  | String  | stats                                                                                                                    |
| `year` | Integer | 2016, 2017 and 2018                                     |
| `month` | Integer | 2, 6, 10 etc..                                         |
| `day` | Integer | Follows typical calendar convention: 3, 18, 25, etc... |
| `firstName` | String  | Kevin                                                                                                                |
| `lastName`  | String  | Durant                                                                                                                   |

# Contact Us
Follow us on twitter <a href="https://twitter.com/Suredbits">@Suredbits</a>

Join our Slack channel <a href="https://join.slack.com/t/suredbits/shared_invite/enQtNzc0OTA1MjM4NzIxLWJkZDRkMTU5NmYzM2IzMmI2MzVhODQwZjYyZDljMjcwYzIwMzljMWRhY2I0ODZlOWY1OWU3ZmFjNzA2MDczN2Q">Suredbits Slack</a>
 
Email us at <a href="mailto:support@suredbits.com">support@suredbits.com</a>

# Homepage

<a href="https://www.suredbits.com"> Return to Suredbits.com </a>

