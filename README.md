# Financial Ratio Analyzer

A Python tool that pulls a public company's balance sheet and income statement 
data (via the yfinance API) and calculates three key financial ratios:

- **Current Ratio** — measures short-term liquidity
- **Return on Equity (ROE)** — measures profitability relative to shareholder equity
- **Operating Margin** — measures profit retained per dollar of revenue

## How to run
1. Install the required package: `pip install yfinance`
2. Run the script: `python financial_ratio_analyzer.py`
3. Enter any stock ticker (e.g. AAPL, MSFT, TSLA) to see its ratios
4. Type `quit` to exit
