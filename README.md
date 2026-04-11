# Earnings Alpha Signal

A quantitative research project that extracts NLP sentiment signals 
from earnings call transcripts and tests whether they predict 
short-term abnormal stock returns.

## Workflow
- Data collection: SEC EDGAR transcripts + yfinance price/EPS data
- NLP: FinBERT sentiment scoring on CEO remarks and Q&A sections
- Statistics: Event study methodology + OLS regression
- Backtest: Long-short portfolio strategy
- Dashboard: Tableau Public interactive visualization

## Companies Analyzed
AAPL, MSFT, GOOGL, META, AMZN

## Tools
Python, FinBERT, statsmodels, quantstats, Tableau
