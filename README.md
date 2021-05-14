# API server repo + docs

*We're working on this*

---

## Endpoints

> All endpoints are prefixed by https://api.babbl.dev/v1/

### `GET status/`
Test endpoint to check availibility of this server

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
