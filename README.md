## Trader Behavior vs Market Sentiment Analysis
Overview

This project analyzes how trader performance and risk behavior change across market sentiment regimes using real trading data from Hyperliquid and the Bitcoin Fear & Greed Index.
The goal is to uncover actionable behavioral signals that can inform sentiment-aware trading strategies in crypto markets.

Problem Statement

Market sentiment often drives crowd behavior in crypto trading, but its impact on actual trader profitability and risk-taking is less clear.

This analysis answers:

Do traders perform better during Fear or Greed regimes?

How does risk exposure (trade size, participation, conviction) change with sentiment?

Can sentiment be used as a regime filter for smarter trading decisions?

Datasets
1. Historical Trader Data (Hyperliquid)

    211k+ trades

    Fields include trade size, PnL, fees, direction, timestamps

    Aggregated to daily metrics for analysis

2. Bitcoin Fear & Greed Index

    Daily sentiment scores

    Collapsed into two regimes:

    Fear (Fear + Extreme Fear)

    Greed (Greed + Extreme Greed)

Methodology

Data Cleaning & Normalization

Timestamp standardization

Removal of invalid trades

Daily aggregation

Feature Engineering (Daily Level)

Total trades

Total & average PnL

Win rate

Average trade size (risk proxy)

Long/short conviction ratio

Sentiment Alignment

Inner join on date

Neutral/unclassified days excluded

Statistical Validation

Mann–Whitney U tests (non-normal distributions)

Distribution-level comparison between Fear and Greed

Key Findings

Fear regimes outperform Greed in both daily PnL and trading activity.

Traders exhibit higher conviction and participation during Fear, consistent with contrarian behavior.

Greed regimes show reduced activity and weaker performance, likely due to crowding risk.

Risk exposure during Fear is selective, not reckless—higher returns without disproportionate trade size inflation.

Actionable Insights

Contrarian Opportunity: Favor selective long exposure during Fear regimes.

Risk Management: Reduce exposure during Greed to avoid crowded trades.

Regime-Aware Sizing: Use sentiment as a gating signal for position sizing and trade frequency.

Strategy Design: Incorporate sentiment regimes into systematic trading rules.

Repository Structure
ds_debasmita_chatterjee/
├── notebook_1.ipynb        # Full reproducible analysis (Google Colab)
├── historical_data.csv     # Input: Hyperliquid trades
├── fear_greed_index.csv    # Input: Market sentiment
├── csv_files/
│   └── final_daily_dataset.csv
├── outputs/
│   ├── pnl_by_sentiment.png
│   └── trade_size_by_sentiment.png
└── ds_report.pdf           # Final summarized insights

How to Run

Open notebook_1.ipynb in Google Colab

Upload the two input CSV files

Run cells top to bottom — no additional setup required

Tools & Libraries

Python

Pandas

Matplotlib

SciPy

Google Colab

Notes

This project focuses on behavioral signal extraction, not predictive modeling.
Future extensions could include per-account performance analysis, leverage dynamics, and intraday sentiment signals.

Author: Debasmita Chatterjee
