# API server repo + docs

*We're working on this*

---

## Contents

- Endpoints
- Statuses
- Authentication

---

## Endpoints

> All endpoints are prefixed by https://api.babbl.dev/v1/

### `GET status/`
Test endpoint to check availibility of this server


### `GET get_articles/`
*Gets articles with sentiment info for the requested ticker(s), formatted to return as list of article objects*

**Args**\
key - Your API key\
tickers - Comma-separated tickers\
*limit* - (Optional, default 10) limit of articles to return for each ticker\
*days* - (Optional, default 14) number of days to look back for articles

**Important**\
Backend will default to lower article count of articles between limit and days if both are provided.

example - `GET https://api.babbl.dev/v1-1/get_articles?key=<your key>&tickers=PLTR,NVDA&limit=1`
```json                                                                                                                                      
[
  {
    "entities": "PLTR", 
    "main_ticker": "PLTR",
    "optimism": 0.0,
    "pessimism": 0.0,
    "reactive": 0.0,
    "speculative": 12.5,
    "timestamp": "2021-05-24",
    "title": "Palantir Technologies Strikes $32.5M Deal With US Air Force | Benzinga",
    "url": "https://cloud.iexapis.com/v1/news/article/16c0f337-0081-449d-842b-ab33562c310e",
    "x_graph": 10.141261811587285,
    "y_graph": 0.0
  },
  {
    "entities": "BBY, TOL, VIX, OKTA, NVDA, COST",
    "main_ticker": "NVDA",
    "optimism": 19.05,
    "pessimism": 9.52,
    "reactive": 9.52,
    "speculative": 114.29,
    "timestamp": "2021-05-24",
    "title": "Expected Moves This Week: Nvidia, Salesforce, Snowflake, Costco, Bitcoin And More | Benzinga",
    "url": "https://cloud.iexapis.com/v1/news/article/4f611e48-f16d-4aa5-8fc0-af0473ddc85a",
    "x_graph": 85.0,
    "y_graph": 85.0
  }
]
```


### `GET get_articles/`
*Gets articles with sentiment info for the requested ticker(s)*

**Args**\
key - Your API key\
tickers - Comma-separated tickers\
*limit* - (Optional, default 10) limit of articles to return for each ticker\

example - `GET https://api.babbl.dev/v1/get_articles?key=<your key>&tickers=SHOP,AAPL&limit=1`
```json
{
  "AAPL": [
    {
      "entities": "AMZN, BBY, CALL, BUY, FB, AAPL",
      "optimism": 20.59,
      "pessimism": 14.71,
      "reactive": 23.53,
      "speculative": 52.94,
      "timestamp": "2021-05-11",
      "title": "Entering Final 'Run into Earnings' Wave... | Benzinga",
      "url": "https://cloud.iexapis.com/v1/news/article/a90a65e0-a083-4bae-8d30-57a792af3b0e"
    }
  ],
  "SHOP": [
    {
      "entities": "JMP, CAP, J&J, O, IRR, SE",
      "optimism": 17.5,
      "pessimism": 11.5,
      "reactive": 55.0,
      "speculative": 42.5,
      "timestamp": "2021-05-12",
      "title": "Facebook's Crypto Project Reboots With Smaller Ambitions | Yahoo Finance",
      "url": "https://cloud.iexapis.com/v1/news/article/1d03e363-ffcb-46ec-9710-5c5de3d01714"
    }
  ]
}
```


### `GET populated_tickers/`
*See which tickers currently have been populated in all tables, i.e. which tickers are supported*

**Args**\
key - Your API key\

example - `GET https://api.babbl.dev/v1/populated_tickers?key=<your key>`
```json
{
  "data": [
    {
      "mentions": 124,
      "ticker": "PLTR"
    },
    {
      "mentions": 1557,
      "ticker": "AAPL"
    },
    {
      "mentions": 40,
      "ticker": "SNDL"
    },
    ...
  ],
  "meta": {
    "all_tickers": [
      "PLTR",
      "AAPL",
      "SNDL",
      ...
    ]
  }
}
```

### `GET ticker_snippets/`
*Gets raw snippets with sentiment info for the requested ticker(s)*

**Args**\
key - Your API key\
tickers - Comma-separated tickers\
*days* - (Optional, default 10) look-back range for days to pull snippets\
*max* - (Optional, default 10) maximum snippets to return for each ticker

example - `GET https://api.babbl.dev/v1/ticker_snippets?key=<ur key>&tickers=AAPL,PTON&max=2&days=3`
```json
{
  "AAPL": {
    "snippet_count": 2,
    "snippets": [
      {
        "optimistic": 1.0,
        "pessimistic": 0.0,
        "reactive": 1.0,
        "speculative": 0.0,
        "text": "The iPhone app for BitMart, a cryptocurrency exchange associated with quick listing of meme coins such as Shiba Inu (SHIB) and SafeMoon (SAFEMOON), gained ground on Apple Inc\u2019s (NASDAQ:AAPL) App Store",
        "tick": "AAPL",
        "timestamp": "2021-05-12",
        "title": "Rich people ditched NYC for these random cities | New York Post"
      },
      {
        "optimistic": 0.0,
        "pessimistic": 1.0,
        "reactive": 1.0,
        "speculative": 0.0,
        "text": "Price Action: Apple shares closed nearly 0.7% lower at $125.91 in Tuesday\u2019s regular trading and fell 0.15% in the after-hours session.",
        "tick": "AAPL",
        "timestamp": "2021-05-12",
        "title": "Is Apple Working On A Nintendo Switch Clone? | Benzinga"
      }
    ]
  },
  "PTON": {
    "snippet_count": 0,
    "snippets": []
  }
}
```

### *Amended* `GET v1-1/ticker_snippets/`
*Gets raw snippets with sentiment info for the requested ticker(s)*

**Args**\
key - Your API key\
tickers - Comma-separated tickers\
*days* - (Optional, default 10) look-back range for days to pull snippets\
*max* - (Optional, default 10) maximum snippets to return for each ticker

example - `GET https://api.babbl.dev/v1-1/ticker_snippets?key=<ur key>&tickers=PLTR,NVDA&max=1`
```json
[
  {
    "optimistic": 1.0,
    "pessimistic": 0.0,
    "reactive": 1.0,
    "speculative": 0.0,
    "text": "Meme stock rally \u2013 GME, AMC, PLTR and MVIS:\nChart prepared by Warren Venketas, Refinitiv\n--- Written by Warren Venketas for DailyFX.com\nContact and follow Warren on Twitter: @WVenketas\nDailyFX provides forex news and technical analysis on the trends that influence the global currency markets.",
    "main_ticker": "PLTR",
    "timestamp": "2021-05-27",
    "title": "Bitcoin (BTC), Gold, Gamestop (GME) & AMC \u2013 FinTwit Trends to Watch | DailyFX"
  },
  {
    "optimistic": 1.0,
    "pessimistic": 1.0,
    "reactive": 0.0,
    "speculative": 1.0,
    "text": "Directional Spreads\nHere are bearish credit call spread examples in NVDA based on the expected move (better thought of as \u201cnot bullish\u201d:\n\n\u00a0\nAnd here are bullish credit put spread examples in NVDA, based on the expected move (better thought of as \u201cnot bearish\u201d:\n\nOptions AI puts the expected move at the heart of its trading platform.",
    "main_ticker": "NVDA",
    "timestamp": "2021-05-26",
    "title": "Wednesday Earnings. NVIDIA, Snowflake: Expected Moves And Trading With Credit Spreads | Benzinga"
  }
]
```

### `GET timeseries_sentiment/`
*Gets daily scores for the ticker(s) passed in*

**Args**\
key - Your API key\
tickers - Comma-separated tickers\
*days* - (Optional, default 10) look-back range for days to analyze\

example - `GET https://api.babbl.dev/v1/timeseries_sentiment?key=<ur key>&tickers=MSFT,TSLA&days=3`
```json
{
  "MSFT": {
    "2021-05-10": 0.0,
    "2021-05-11": 0.75,
    "2021-05-12": 0.0
  },
  "TSLA": {
    "2021-05-10": 0.0,
    "2021-05-11": 0.014204202914857366,
    "2021-05-12": -0.03903966470144858
  }
}
```


## User Management Section

*Endpoints dealing with managing User Accounts*

###   `POST v1/watchlist_addition/`
*Adds a single ticker to a user's watchlist*

**Args**\
key - Your API key\
uname - User's ID\
tick - Ticker to add to watchlist\

**Important**\
Returns HTTP 418 if user is already at their maximum watchlist size.\
Returns HTTP 200 on success.

example - `POST https://api.babbl.dev/v1/watchlist_addition`\
ARGS:
```json
{
  "key": "<ur key>",
  "uname": "<alphanum User ID>",
  "tick": "<Ticker to be added>"
}
```
Response(s):\
HTTP 200 -- Success\
HTTP 400 -- Malformed Request, Missing required Arg\
HTTP 403 -- Access Denied, API Key\
HTTP 418 -- Action wasn't performed, User at max Watchlist items already

###   `POST v1/watchlist_delete/`
*Removes a single ticker from a user's watchlist*

**Args**\
key - Your API key\
uname - User's ID\
tick - Ticker to remove from watchlist\

**Important**\
Returns HTTP 200 on success, not currently catching attempting to delete
a non-existent ticker for a given user. Also currently would delete duplicate
tickers for a user, e.g. if a user has 2 TSLA's in their watchlist, this 
would delete both.

example - `POST https://api.babbl.dev/v1/watchlist_delete`\
ARGS:
```json
{
  "key": "<ur key>",
  "uname": "<alphanum User ID>",
  "tick": "<Ticker to be added>"
}
```
Response(s):\
HTTP 200 -- Success\
HTTP 400 -- Malformed Request, Missing required Arg\
HTTP 403 -- Access Denied, API Key\

