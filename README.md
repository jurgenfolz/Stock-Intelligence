# Stock Intelligence

Do you follow the financial markets and enjoy using Power BI? You’re in the right place. This repo contains a Power BI  report for analyzing stock market data using Yahoo Finance APIs. It can be refreshed anywhere and **does not require an API key**.
![alt text](Screenshots\mainPage.png)

## Usage

1. **IMPORTANT: Edit `PathtoTickersCSV`** parameter to point to your local CSV with ticker symbols.
![alt text](Screenshots\transformData.png)
![alt text](Screenshots\editPrameters.png)
2. **Adjust `Interval` and `Range`** parameters as needed (e.g., `"1d"`, `"1wk"`, `"1mo"`, and ranges like `"1y"`, `"5y"`, etc.).  
3. **Refresh** the dataset. Power BI will retrieve the data from Yahoo Finance’s unofficial endpoints and populate the tables.

## Project Overview

- **File**: `Stock Intelligence.pbip` (using the new Power BI TMDL and PBIR format).  
- **Main Components**:
  - **factIndicators**: Stores daily open, high, low, close, and volume data per ticker, fetched via Yahoo Finance’s chart endpoint.
  - **dFundamentals3M**: Quarterly (“3M”) metrics such as `quarterlyPeRatio`, `quarterlyPbRatio`, etc.
  - **dFundamentalsTTM**: Trailing Twelve Months (TTM) metrics such as `trailingPeRatio`, `trailingMarketCap`, etc.
  - **dTickers**: Info about each ticker (symbol, exchange, market times).

## Data Source (Unofficial Yahoo Finance API)

- **factIndicators** pulls OHLC data from: https://query1.finance.yahoo.com/v8/finance/chart/
- **dFundamentals** pulls fundamental timeseries from: https://query1.finance.yahoo.com/ws/fundamentals-timeseries/v1/finance/timeseries/

Since these are **unofficial endpoints**, they can change or break without notice.

## Parameters

1. **PathtoTickersCSV**  
 - Points to a single-column CSV of ticker symbols.  
 - Example:
   ```
   Ticker
   AAPL
   MSFT
   TSLA
   ```
2. **Interval** (e.g., `"1d"`)  
3. **Range** (e.g., `"1y"`)

By default, the project fetches daily data for the last year (`1d` / `1y`).

## Metrics

### Daily Metrics (factIndicators)
- **ClosePrice**, **OpenPrice**, **HighPrice**, **LowPrice**  
- **TotalVolume**  
- **SimpleMovingAverage**  
- **PriceChange**, **PriceChangeRelative**


## Fundamentals Overview

- **P/E Ratio**  
  Compares a company's share price to its earnings per share (EPS). A quick valuation method for how much investors pay per dollar of earnings.  
  **Formula:** $` {P/E} = \frac{\text{Price per share}}{\text{EPS}}`$ 

- **Forward P/E**  
  Uses *forecasted* EPS instead of historical EPS to reflect expected future earnings.  
  **Formula:** $` \text{Forward P/E} \approx \frac{\text{Price per share}}{\text{Projected EPS}} `$ 

- **PEG Ratio**  
  Adjusts the P/E ratio by the company’s earnings growth rate. Helps indicate whether P/E is high or justified by growth.  
  **Formula:** $` \text{PEG} = \frac{\text{P/E Ratio}}{\text{Earnings Growth}} `$ 

- **P/S Ratio**  
  Price-to-Sales compares share price to revenue per share. Often used for evaluating companies with little or no earnings.  
  **Formula:** $` \text{P/S} = \frac{\text{Price per share}}{\text{Revenue per share}} `$ 

- **P/B Ratio**  
  Price-to-Book compares share price to book value (assets minus liabilities). Indicates how the market values a firm’s net assets.  
  **Formula:** $` \text{P/B} = \frac{\text{Price per share}}{\text{Book Value per share}} `$ 

- **Market Cap**  
  Represents total equity value. Simple gauge of company size.  
  **Formula:** $` \text{Market Cap} = \text{Share Price} \times \text{Shares Outstanding} `$ 

- **EV (Enterprise Value)**  
  Approximate takeover value that adds net debt to Market Cap. Includes debt and cash adjustments.  
  **Formula:** $` \text{EV} = \text{Market Cap} + \text{Total Debt} - \text{Cash} `$ 

- **EV / EBITDA**  
  Measures how “expensive” a company is relative to its operating earnings (EBITDA).  
  **Formula:** $` \frac{\text{EV}}{\text{EBITDA}} `$ 

- **EV / Revenue**  
  Similar to EV/EBITDA but uses top-line revenue. Useful for unprofitable or early-stage firms.  
  **Formula:** $` \frac{\text{EV}}{\text{Revenue}} `$ 


## Notes

- **Unofficial API**: The Yahoo Finance calls may break or change at any time.
- **CSV** must have one column named `Ticker`, listing each symbol to include.
- **This is for **analysis/visualization** only, not high-frequency trading.
- **Project File**: `Stock Intelligence.pbip` (TMDL and PBIR format).


