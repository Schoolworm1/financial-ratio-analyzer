import yfinance as yf

def get_ratios(ticker_symbol):
    """Fetch data and calculate ratios for a given ticker. Returns True on success."""
    print(f"\nFetching financial statement data for {ticker_symbol}...\n")
    company = yf.Ticker(ticker_symbol)

    try:
        balance_sheet = company.balance_sheet
        financials = company.financials

        if balance_sheet.empty or financials.empty:
            print(f"No data found for '{ticker_symbol}'. Check that the ticker is correct.")
            return False

        current_assets = balance_sheet.loc['Current Assets'].iloc[0]
        current_liabilities = balance_sheet.loc['Current Liabilities'].iloc[0]
        net_income = financials.loc['Net Income'].iloc[0]
        stockholders_equity = balance_sheet.loc['Stockholders Equity'].iloc[0]
        operating_income = financials.loc['Operating Income'].iloc[0]
        total_revenue = financials.loc['Total Revenue'].iloc[0]

        current_ratio = current_assets / current_liabilities
        roe = (net_income / stockholders_equity) * 100
        operating_margin = (operating_income / total_revenue) * 100

        print(f"--- {ticker_symbol.upper()} Financial Ratios (Most Recent Fiscal Year) ---")
        print(f"• Current Ratio (Liquidity):     {current_ratio:.2f}")
        print(f"• Return on Equity (ROE %):      {roe:.2f}%")
        print(f"• Operating Margin (%):          {operating_margin:.2f}%")
        print("=========================================")
        return True

    except KeyError as e:
        print(f"Accounting Error: Missing line item {e}. This company may report its "
              f"statements differently (common with banks, REITs, or foreign filers).")
        return False
    except Exception as e:
        print(f"Error: Could not parse statements. Details: {e}")
        return False


def main():
    print("=========================================")
    print("      FINANCIAL RATIO ANALYZER            ")
    print("=========================================")
    print("Type a ticker symbol to analyze it, or type 'quit' to exit.\n")

    while True:
        ticker_symbol = input("Enter ticker symbol (e.g. AAPL, MSFT, TSLA): ").strip().upper()

        if ticker_symbol.lower() == "quit":
            print("\nGoodbye!")
            break

        if not ticker_symbol:
            print("Please enter a ticker symbol.\n")
            continue

        get_ratios(ticker_symbol)
        print()  # blank line before next prompt


if __name__ == "__main__":
    main()
