## Trader Behavior vs Market Sentiment Analysis

### Objective

Quantify how market sentiment regimes (**Fear vs Greed**) influence trader performance, risk exposure, and behavior using historical execution data. The goal is to extract actionable trading rules driven by behavioral patterns rather than price prediction.

---

### Datasets

#### 1. Trader Execution Data (Hyperliquid)

Trade-level records (~211K rows)

**Key fields used**

- account
- symbol
- execution_price
- size
- side
- time
- closedPnL
- leverage

#### 2. Bitcoin Fear & Greed Index

Daily market sentiment classification

| Date | Classification |
|------|----------------|
| YYYY-MM-DD | Fear / Greed |

---

### Methodology

#### A. Data Preparation

**Cleaning**

- Removed invalid or zero-size trades
- Standardized timestamps to UTC and aggregated to daily level
- Dropped duplicate rows

**Aggregation (Daily Level per Account)**

| Metric | Definition |
|--------|-----------|
| Daily PnL | Sum of closedPnL |
| Win Rate | Percentage of profitable trades |
| Avg Trade Size | Mean absolute position size |
| Trade Count | Number of executions |
| Long/Short Ratio | Long volume divided by short volume |
| Avg Leverage | Mean leverage used |

**Sentiment Alignment**

- Converted sentiment into binary regimes
  - Fear = Fear + Extreme Fear
  - Greed = Greed + Extreme Greed
- Performed inner join on date
- Excluded neutral or missing sentiment days

---

#### B. Statistical Analysis

Because trading metrics are non-normal:

- Mann–Whitney U test used for regime comparison
- Distribution-level analysis instead of mean-only comparison

Metrics evaluated:

- Daily PnL
- Win rate
- Trade frequency
- Position size
- Leverage usage

---

### Key Findings

#### Performance Regime Effect

- Median daily PnL significantly higher during Fear days
- Win rate distribution shifts positively under Fear

#### Behavioral Shift

- Traders increase participation (trade count increases) during Fear
- Position sizing increases moderately, not proportional to PnL, indicating selective conviction rather than reckless risk

#### Greed Regime Characteristics

- Lower trading activity
- Reduced profitability dispersion
- Evidence of crowded positioning and weaker edge

---

### Actionable Strategy Implications

| Regime | Behavioral Signal | Strategy Rule |
|--------|-------------------|---------------|
| Fear | Higher conviction and better edge | Allow higher trade frequency for proven traders |
| Fear | Controlled size increase | Moderate leverage expansion acceptable |
| Greed | Lower edge and crowding | Reduce leverage and trade frequency |
| Greed | Lower dispersion | Favor mean-reversion and smaller targets |

---

### Repository Structure

