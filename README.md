# Earnings Alpha Signal (Independent Quantitative Research)

A systematic alpha signal pipeline that extracts NLP sentiment 
scores from SEC EDGAR earnings call transcripts and tests whether 
tone surprise predicts short-term abnormal stock returns.

## Research Question
Can the sentiment of executive language in earnings calls - 
independent of reported EPS numbers - predict short-term 
abnormal stock returns?

## Methodology

### 1. Data Collection
- Earnings call transcripts pulled from SEC EDGAR via 
  sec-edgar-downloader across 5 S&P 500 companies
  (AAPL, MSFT, GOOGL, META, AMZN) over 15 earnings events
- Price data and EPS actuals/estimates pulled via yfinance

### 2. NLP Sentiment Scoring
- Used FinBERT - a BERT model fine-tuned on financial text - 
  to score CEO remarks and Q&A sections
- Constructed a "tone surprise" metric by comparing current 
  sentiment score against the trailing average for that company

### 3. Signal Construction
- Combined tone surprise with earnings surprise 
  (actual EPS vs estimated EPS) into a composite alpha signal
- Composite signal = weighted combination of NLP sentiment 
  deviation and standardized earnings beat/miss

### 4. Statistical Analysis
- Event study using Fama-French 3-factor model to compute 
  Cumulative Abnormal Returns (CAR) over [-1, +3] day window
- OLS regression: CAR ~ earnings_surprise + tone_surprise
- R² = 0.23; earnings surprise associated with 3.3% higher 
  CAR (p = 0.097)

### 5. Backtest
- Long-short portfolio: long top quartile composite signal, 
  short bottom quartile
- Backtest period: 15 earnings events across 5 companies
- Annualized return: 12.53% vs 9.13% for SPY benchmark
- Sharpe ratio: 0.54
- Max drawdown: -20.42%

## Results Summary

| Metric | Value |
|--------|-------|
| Annualized Return | 12.53% |
| SPY Benchmark | 9.13% |
| Sharpe Ratio | 0.54 |
| Max Drawdown | -20.42% |
| R² (OLS) | 0.23 |
| Earnings Surprise Beta | 3.3% higher CAR (p=0.097) |

## Limitations
- Small sample size (5 companies, 15 events) limits 
  statistical power
- p = 0.097 suggests directional signal but not 
  conclusive at conventional significance levels
- No transaction costs or slippage modeled in backtest
- Look-ahead bias possible if transcript timestamps 
  not carefully controlled

## Tools & Libraries
Python, FinBERT, statsmodels, quantstats, Fama-French 
data via pandas-datareader, yfinance, Tableau

## Dashboard
Interactive Tableau visualization available at:
[Earnings Alpha Dashboard](https://public.tableau.com/app/profile/hansini.rajesh/viz/earnings-alpha/earnings-alphadashboard?publish=yes)

## Structure
```
earnings-alpha/
├── data/
│   ├── AAPL_earnings.csv
│   ├── AAPL_prices.csv
│   ├── AMZN_earnings.csv
│   ├── AMZN_prices.csv
│   ├── GOOGL_earnings.csv
│   ├── GOOGL_prices.csv
│   ├── META_earnings.csv
│   ├── META_prices.csv
│   ├── MSFT_earnings.csv
│   ├── MSFT_prices.csv
│   ├── backtest_metrics.csv
│   ├── car_results.csv
│   ├── features.csv
│   ├── portfolio_performance.csv
│   ├── sentiment_scores.csv
│   └── transcripts_clean.json
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_sentiment.ipynb
│   ├── 03_features.ipynb
│   ├── 04_stats.ipynb
│   └── 05_backtest.ipynb
├── .gitignore
├── requirements.txt
└── README.md
```

## Future Work
- Expand to 30+ S&P 500 companies across multiple sectors
- Add options flow data as additional signal
- Implement proper walk-forward backtesting
- Add transaction cost modeling
