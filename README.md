# 🤖 Algo-Trading_Bot

This project implements an algorithmic trading strategy that makes intelligent buy/sell decisions for the **SPY ETF** using financial news sentiment analysis powered by **FinBERT**. The strategy is developed using the [Lumibot](https://lumibot.org/) trading framework and integrates with the Alpaca API for brokerage and news data.

---

## 🚀 Overview

- Uses Alpaca’s News API to fetch the latest SPY-related headlines.
- Applies FinBERT to classify sentiment as **positive** or **negative**.
- Executes market orders based on sentiment confidence.
- Implements stop-loss and take-profit risk controls.
- Backtests the strategy with historical data using Yahoo Finance.

---

## 🧠 Strategy Logic

| Condition | Action |
|----------|--------|
| Sentiment = `positive` and probability > `0.999` | Buy SPY |
| Sentiment = `negative` and probability > `0.999` | Sell SPY |
| Last trade was `buy` and sentiment becomes `negative` | Exit position |
| Last trade was `sell` and sentiment becomes `positive` | Re-enter long position |

The bot allocates **50% of available cash** for each trade and places:
- 🛑 Stop loss at 5% loss
- 🎯 Take profit at 20% gain (for buys), or 20% drop (for shorts)

---

## 🧰 Tech Stack

| Tool | Purpose |
|------|---------|
| **Python** | Main programming language |
| **Lumibot** | Backtesting & trading framework |
| **Alpaca API** | Broker + news feed |
| **FinBERT** | NLP-based sentiment analysis |
| **YahooDataBacktesting** | Historical data source for testing |

---

## 📦 Installation

```bash
pip install lumibot
pip install alpaca-trade-api
pip install timedelta
# Add your finbert_utils.py file to the project directory
```

▶️ How to Run
Update your Alpaca API keys in the script:

```python
API_KEY = "your_api_key"
API_SECERET = "your_api_secret"
Then backtest the strategy:
```
Then backtest the strategy:

```python
from datetime import datetime

start_date = datetime(2020, 1, 1)
end_date = datetime(2023, 1, 1)

strategy.backtest(
    YahooDataBacktesting,
    start_date,
    end_date,
    parameters={"symbol":"SPY", "cash_at_risk":0.5}
)

```

To run live on Alpaca (paper trading):

```python
trader = Trader()
trader.add_strategy(strategy)
trader.run_all()
```

📊 Output
Your performance chart (if plotted) will show:

- 🔵 MLTrader portfolio growth

- 🔴 SPY benchmark performance

- 🔻/🔺 Buy/sell markers

- 🟩 Cash movement


📈 Potential Improvements

- Add logging to track each trade (date, price, sentiment).

- Include Sharpe ratio and drawdown analysis.

- Expand to multi-asset strategies (e.g., TSLA, AAPL).

- Enable trailing stop-loss or dynamic position sizing.

⚠️ Disclaimer
This project is intended for educational purposes only. It is not financial advice. Use in live environments at your own risk.

🧠 Acknowledgements
- FinBERT by ProsusAI

- Alpaca Markets

- Lumibot Framework

