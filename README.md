# Overview
This document provides instructions on how to access our World Sentiment Analysis API

- [User information](#user-information)
- [User watchlist](#user-watchlist)
- [Supported brokerages](#supported-brokerages)
- [User brokerage](#user-brokerage)
- [User linked brokerages](#user-linked-brokerages)
- [User holdings](#user-holding)
- [Recommended large dips](#recommended-large-dips)
- [Popular Topics](#popular-topics)
- [Company information](#company-information)
- [Company historical data](#historical-company-data)
- [Topic historical data](#historical-topic-data)
- [Is market open](#check-if-market-is-open)
- [Enter a position](#buy-a-position)
- [Schedule to enter a position](#schedule-to-buy-a-position)
- [Exit a position](#sell-a-position)
- [Schedule to exit a position](#schedule-to-sell-a-position)


## User information

This end point returns information about the user

### Sample call

```
HTTP GET
  https://truesight.me/api/me
```

### Sample response

```json
{
  "id":                 INTEGER,  // The user id
  "email":              STRING,   // The user email
  "name":               STRING,   // The name of the user
  "project_enabled":    BOOLEAN,  // Is user about to see the projects module
  "trading_enabled":    BOOLEAN,  // Is user able to trade if he links his brokerage account
  "upgraded":           BOOLEAN,  // Can user see the large dips report or is required to 
  "technical_enabled":  BOOLEAN,  // Can user see all the technical indicators or just simple view
  "contact_email":      STRING,   // The email address to contact the user by
  "paper_trading":      BOOLEAN,  // Is the user currently in paper trading mode
  "brokerage_linked":   BOOLEAN,  // Has the user linked her brokerage account
  "brokerage_name":     STRING    // The name of the user's brokerage  
  "portfolio_value":    FLOAT,    // The value of the user's portfolio
  "cash_balance":       FLOAT     // The user's cash balance in her brokerage account
}
```



## User watchlist

This end point returns the companies the user is watching

### Sample call

```
HTTP GET
  https://truesight.me/api/watchlist
```

### Sample response

```json
[
  {
    "stock_symbol":     STRING,  // The stock symbol of the company
    "company_name":     STRING,  // The name of the company
    "exchange":         STRING,  // The exchange the company is traded on
    "current_rsi":      FLOAT,   // The current RSI of the company
    "daily_fluctuation": FLOAT,   // The historical average daily flucuation of the company's share price in percentage
    "latest_price":     FLOAT    // The latest share price of the company
  }
  ...
]
```

## Supported brokerages
This end point returns all the brokerages currently supported

### Sample call

```json
HTTP GET
  https://truesight.me/api/supported_brokerages
```

### Sample response

```json
[
  {
    "display_name": STRING,   // The display name for the default brokage
    "name":         STRING,   // The name for the brokage
  },
  ...
]  
```

## User brokerage
This end point returns the default brokerage of the user

### Sample call

```json
HTTP GET
  https://truesight.me/api/brokerage?brokerage=NEW_DEFAULT_BROKERAGE
```

#### Parameters

- NEW_DEFAULT_BROKERAGE: STRING - the new brokerage to be set as the default for the user
  - available options:
    - amtd
    - coinbase_pro
    - paper_trade_brokerage

### Sample response

```json
{
  "display_name": STRING,   // The display name for the default brokage
  "name":         STRING,   // The name for the brokage

}  
```

## User linked brokerages
This end point returns all the brokerages the user has established linkage to

### Sample call

```json
HTTP GET
  https://truesight.me/api/linked_brokerages
```

### Sample response

```json
[
  {
    "display_name": STRING,   // The display name for the default brokage
    "name":         STRING,   // The name for the brokage
  },
  ...
]  
```

## User holdings

This end point returns the current holdings of the user

### Sample call

```json
HTTP GET
  https://truesight.me/api/holdings
```

### Sample response

```json
[
  {
    "stock_symbol":      STRING,   // The stock symbol of the company
    "company_name":      STRING,   // The name of the company
    "exchange":          STRING,   // The exchange the company is traded on
    "expected_returns":  FLOAT,    // The expected returns in percentages after successfully exiting 
    "performance":       FLOAT,    // The returns in percentages right now
    "quantity":          INTEGER,  // The number of shares held in this position
    "daily_fluctuation":  FLOAT,    // The historical average daily flucuation of the company's share price in percentage
    "target_exit_price": FLOAT,    // The price we are expecting to exit this position
    "latest_price":      FLOAT,    // The latest share price of the company
    "entry_price":       FLOAT,    // The price when the position was purchased
    "entry_date":        STRING    // The date the position was purchased - YYYY-MM-DD
  }  
  ...
]
```



## Recommended large dips

This end point returns the list of companies our system detected abnormalies in

### Sample call

```json
HTTP GET
  https://truesight.me/api/large_dips
```

### Sample response

```json
[
  {
    "stock_symbol":     STRING,  // The stock symbol of the company
    "company_name":     STRING,  // The name of the company
    "exchange":         STRING,  // The exchange the company is traded on    
    "sector_id":        STRING,  // The id of the sector
    "sector_name":      STRING,  // The name of the sector
    "current_rsi":      FLOAT,   // The current RSI of the company
    "daily_fluctuation": FLOAT,  // The historical average daily flucuation of the company's share price in percentage
    "latest_price":     FLOAT    // The latest share price of the company
    "direction":        STRING   // bullish or bearish
  }
  ...
]
```

## Popular Topics

This end point returns the list of topics our system detected to be most popular today

### Sample call

```json
HTTP GET
  https://truesight.me/api/popular_topics
```

### Sample response

```json
[
  {
    "name":             STRING,  // The name of the topic
    "url":              STRING,  // The page of the topic
    "img_url":          STRING,  // The image for the topic
    "feed":             STRING,  // The url to get the sentiment feed for the topic
  }
  ...
]
```


## Company information

This end point returns details about the company given stock symbol

### Sample call

```json
HTTP GET
  https://truesight.me/api/company?stock_symbol=:STOCK_SYMBOL
```

#### Parameters

- STOCK_SYMBOL: STRING - the stock symbol of the company

### Sample response

```json
{
    "stock_symbol":      STRING,  // The stock symbol of the company
    "company_name":      STRING,  // The name of the company
    "exchange":          STRING,  // The exchange the company is traded on    
    "latest_price":      FLOAT,   // The latest share price of the company  
    "buy_this_dip":      BOOLEAN, // If model recommends we buy the current dip
    "exit_position":     BOOLEAN, // If model recommends we sell our position
    "sector":             STRING,  // The sector of the company
    "industry":           STRING,  // The industry of the company
    "market_cap":         FLOAT,   // The current market capitalization of the company
    "52_week_high":       FLOAT,   // The highest price over the past 52 weeks
    "52_week_low":       FLOAT,   // The lowest price over the past 52 weeks
    "beta":               FLOAT,   // The beta of the company
    "daily_flucuation":  FLOAT,   // The historical average daily flucuation of the company's share price in percentage
    "company_strength":  FLOAT,   // Indicator of how company recovered historically from large dips
    "category_strength": FLOAT,   // Indicator of how the category recovered historically from large dips  
  
  
  
    // Attributes returned only if user is holding position,   
    "expected_returns":  FLOAT,    // The expected returns in percentages after successfully exiting 
    "performance":       FLOAT,    // The returns in percentages right now
    "quantity":          INTEGER,  // The number of shares held in this position
}
```



## Historical company data

This end point returns the historical daily close data of the company for the past 180 days

### Sample call

```json
HTTP GET
  https://truesight.me/api/company/daily_trades?stock_symbol=:STOCK_SYMBOL
```

#### Parameters

- STOCK_SYMBOL: STRING - the stock symbol of the company

### Sample response

```json
[
   {
     "close_date":        STRING, // the date closed in the format YYY-MM-DD
     "close_price":       FLOAT,  // the closed price on the date
     "sma_180":           FLOAT,  
     "sma_7":             FLOAT,  
     "sma_30":            FLOAT,  
     "bollinger_upper":   FLOAT,       
     "bollinger_lower":   FLOAT,       
     "macd_histogram":    FLOAT,            
     "rsi":               FLOAT                 
   },
   ...
]
```


## Historical topic data

This end point returns the historical daily sentiment data of the topic for the past 180 days

### Sample call

```json
HTTP GET
  https://truesight.me/api/topic/:TOPIC_ID
```

#### Parameters

- TOPIC_ID: INTEGER - the integer of the topic

### Sample response

```json
[
   {
     "summary_date":      STRING, // the date closed in the format YYY-MM-DD
     "magnitude":         FLOAT,  // the closed price on the date
     "polarity":          FLOAT,  
     "subjectivity":      FLOAT,  
     "sma_14":            FLOAT                 
   },
   ...
]
```



## Check if market is open

This api returns if the market is open

### Sample call

```json
HTTP GET
  https://truesight.me/api/market_open
```

### Sample response

```json
{
  "brokerage":  STRING,  // The brokerage the user is linked to
  "is_open":    BOOLEAN  // True if the market is open right now
}
```



## Enter a position

Call this API if user wants to enter a position now. Only use this when the market is open

### Sample call

```json
HTTP POST
  https://truesight.me/api/buy?stock_symbol=:STOCK_SYMBOL
```

#### Parameters

- STOCK_SYMBOL: STRING - the stock symbol of the company

### Sample response

```json
{
  "status":       STRING,   // The string to display to the user
  "stock_symbol": STRING,   // The stock symbol of the company bought
  "quantity":     INTEGER,  // The number of shares held in this position
  "entry_price":       FLOAT,    // The price when the position was purchased  
}
```



## Schedule to enter a position

Call this API if user wants to enter a position but the market is not open

### Sample call

```json
HTTP POST
  https://truesight.me/api/bid?stock_symbol=:STOCK_SYMBOL
```

#### Parameters

- STOCK_SYMBOL: STRING - the stock symbol of the company

### Sample response

```json
{
  "status":       STRING,   // The string to display to the user
  "stock_symbol": STRING,   // The stock symbol of the company bought
  "quantity":     INTEGER,  // The number of shares held in this position
  "entry_price":       FLOAT,    // The price when the position was purchased  
}
```





## Exit a position

Call this API if user wants to exit a position now. Only use this when the market is open

### Sample call

```json
HTTP POST
  https://truesight.me/api/sell?stock_symbol=:STOCK_SYMBOL
```

#### Parameters

- STOCK_SYMBOL: STRING - the stock symbol of the company

### Sample response

```json
{
  "status":       STRING,   // The string to display to the user
  "stock_symbol": STRING,   // The stock symbol of the company bought
  "quantity":     INTEGER,  // The number of shares held in this position
  "entry_price":  FLOAT,    // The price when the position was purchased  
}
```



## Schedule to exit a position

Call this API if user wants to exit a position but the market is not open

### Sample call

```json
HTTP POST
  https://truesight.me/api/ask?stock_symbol=:STOCK_SYMBOL
```

#### Parameters

- STOCK_SYMBOL: STRING - the stock symbol of the company

### Sample response

```json
{
  "status":       STRING,   // The string to display to the user
  "stock_symbol": STRING,   // The stock symbol of the company bought
  "quantity":     INTEGER,  // The number of shares held in this position
  "entry_price":  FLOAT,    // The price when the position was purchased  
}
```

