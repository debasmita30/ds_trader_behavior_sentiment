## Trader Behavior vs Market Sentiment Analysis
Objective

Quantify how market sentiment regimes (Fear vs Greed) influence trader performance, risk exposure, and behavior using historical execution data. The goal is to extract actionable trading rules driven by behavioral patterns rather than price prediction.

Datasets
1. Trader Execution Data (Hyperliquid)

Trade-level records (~211K rows)

Key fields used

account
symbol
execution_price
size
side
time
closedPnL
leverage

2. Bitcoin Fear & Greed Index

Daily market sentiment classification

Date	      Classification
YYYY-MM-DD	Fear / Greed

Methodology
A. Data Preparation

Cleaning

Removed invalid or zero-size trades
Standardized timestamps → UTC → daily granularity
Dropped duplicate rows

Aggregation (Daily Level per Account)

Metric	           Definition
Daily PnL	         Sum of closedPnL
Win Rate	         % of profitable trades
Avg Trade Size	   Mean absolute position size
Trade Count	       Number of executions
Long/Short Ratio	 Long volume / Short volume
Avg Leverage	     Mean leverage used

Sentiment Alignment

Converted sentiment to binary regimes:
Fear = Fear + Extreme Fear
Greed = Greed + Extreme Greed
Inner join on date
Neutral days excluded

B. Statistical Analysis

Because trading metrics are non-normal:
Mann–Whitney U test used for regime comparison
Distribution-level analysis instead of mean-only comparison
Evaluated differences in:
Daily PnL
Win rate
Trade frequency
Position size
Leverage usage

Key Findings

Performance Regime Effect
Median daily PnL significantly higher during Fear days.
Win rate distribution shifts positively under Fear.

Behavioral Shift
Traders increase participation (trade count ↑) during Fear.
Position sizing increases moderately, not proportionally to PnL → indicates selective conviction, not reckless risk.

Greed Regime Characteristics
Lower activity
Reduced profitability dispersion
Evidence of crowded positioning and weaker edge

Actionable Strategy Implications
Regime	          Behavioral Signal	                       Strategy Rule
Fear	            Higher conviction + better edge	         Allow higher trade frequency for proven traders
Fear	            Controlled size increase	               Moderate leverage expansion acceptable
Greed	            Lower edge + crowding	                   Reduce leverage and trade frequency
Greed             Lower dispersion	                       Favor mean-reversion / smaller targets

Repository Structure
ds_debasmita_chatterjee/
│
├── notebook_1.ipynb              # Full analysis pipeline
├── historical_data.csv           # Trader dataset
├── fear_greed_index.csv          # Sentiment dataset
│
├── csv_files/
│   └── final_daily_dataset.csv   # Engineered dataset
│
├── outputs/
│   ├── pnl_by_sentiment.png
│   └── trade_size_by_sentiment.png
│
└── ds_report.pdf                 # 1-page summary

How to Reproduce
Open notebook_1.ipynb in Google Colab
Upload:
historical_data.csv
fear_greed_index.csv
Run all cells (no external dependencies)

Tools Used
Python
Pandas
NumPy
Matplotlib
SciPy

Scope Notes
This project focuses on:
Behavioral pattern extraction
Regime-based performance differences

Not covered:
Price prediction
High-frequency or intraday modeling

Author
Debasmita Chatterjee
B.Tech Final Year | Data Science & Analytics
