# Earnings Alpha Signal

An end-to-end quantitative research pipeline that extracts NLP sentiment 
signals from earnings call transcripts and tests whether they predict 
short-term abnormal stock returns.

## Hypothesis
The tone of earnings call transcripts contains alpha beyond the standard 
EPS surprise signal — and combining both into a composite signal can drive 
a profitable long-short equity strategy.

## Workflow
1. **Data Collection** - SEC EDGAR 8-K filings + yfinance price and EPS data
2. **NLP Scoring** - FinBERT sentiment scoring on prepared remarks sections
3. **Feature Engineering** - Tone surprise + earnings surprise → composite signal
4. **Event Study** - Fama-French 3-factor abnormal returns (CAR) around earnings dates
5. **Statistics** - OLS regression and t-tests testing signal vs CAR
6. **Backtest** - Long-short portfolio vs SPY benchmark
7. **Dashboard** - Tableau Public interactive visualization

## Key Results
- Earnings surprise is marginally significant (p=0.097) with 3.3% CAR per 1σ
- Long-short strategy returned 7.73% vs SPY 5.67% over the backtest period
- R-squared of 0.23 — signals explain ~23% of CAR variation

## Companies Analyzed
AAPL, MSFT, GOOGL, META, AMZN (2025-2026)

## Tools
Python, FinBERT, statsmodels, quantstats, Tableau Public

## Dashboard
[View Interactive Dashboard](https://public.tableau.com/app/profile/hansini.rajesh/viz/earnings-alpha/earnings-alphadashboard?publish=yes)

## Notebooks
| Notebook | Description |
|---|---|
| 01_data_collection | SEC EDGAR scraping + yfinance EPS and price data |
| 02_sentiment | FinBERT scoring of transcript text |
| 03_features | Tone surprise + earnings surprise + composite signal |
| 04_stats | Fama-French event study + OLS regression |
| 05_backtest | Long-short portfolio backtest vs SPY |
