## Trader Behavior vs Market Sentiment Analysis

### Objective

Analyze how **market sentiment regimes (Fear vs Greed)** influence **trader-level performance and behavior** using historical execution data. Focus is on behavioral signal extraction, not price prediction.

---

### Dataset

**Trader Execution Data (Hyperliquid)**  
~211K trades  

Key fields used:

- account  
- execution_price  
- size_usd  
- side  
- timestamp  
- closed_pnl  
- fee  

**Bitcoin Fear & Greed Index**

- Daily sentiment classification  

---

### Methodology

**Data Preparation**

- Removed invalid trades (zero size/price)  
- Converted timestamps and aggregated at trader–day level  
- Filtered low-activity days  
- Capped extreme PnL outliers (1–99 percentile)  

**Feature Engineering**

- Daily PnL per trader  
- Win rate  
- Median trade size  
- Trade count  
- Long/short ratio  

**Sentiment Alignment**

- Mapped Extreme Fear → Fear  
- Mapped Extreme Greed → Greed  
- Inner join on date  

**Statistical Approach**

- Mann–Whitney U test (non-parametric distributions)  
- Distribution comparison rather than mean-only  

---

### Key Insights

- Fear regimes show **higher trade accuracy (win rate ↑)**  
- Differences in PnL between regimes are **directional but not statistically significant**  
- Behavioral edge in Fear arises from **trade quality rather than increased activity**  
- High-activity traders display stronger sentiment sensitivity  
- Greed regimes show weaker edge and more dispersion compression  

---

### Strategy Implications

| Regime | Behavioral Signal | Strategy Rule |
|--------|------------------|---------------|
| Fear | Higher accuracy | Allow higher participation for proven traders |
| Fear | Selective conviction | Moderate leverage expansion acceptable |
| Greed | Reduced edge | Lower leverage and trade frequency |
| Greed | Compressed dispersion | Favor smaller targets / mean reversion |

---

### Reproducibility

Open **Trader_Behavior_vs_Market_Sentiment_Analysis.ipynb** in Google Colab and run all cells.

---

### Tools

- Python  
- Pandas  
- NumPy  
- Matplotlib  
- SciPy  
- Seaborn  

---

### Author

Debasmita Chatterjee  
Data Science & Analytics
