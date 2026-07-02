
# Trader Performance Under Market Sentiment Regimes

**Bitcoin Fear & Greed Index vs. Hyperliquid Trading Outcomes**
Primetrade.ai — AI Internship Technical Assignment

## Overview

This project analyzes the relationship between Bitcoin market sentiment and trader
performance on Hyperliquid. Daily sentiment classifications (Extreme Fear → Extreme Greed)
are merged with 211K+ trade-level records across 32 accounts to quantify how profitability,
risk exposure, and trading behavior shift across sentiment regimes, and to identify which
traders perform best under each condition.

## Datasets

| Dataset | Description |
|---|---|
| `fear_greed_index.csv` | Daily Bitcoin market sentiment classification and index value |
| `historical_data.csv` | Trade-level execution data from Hyperliquid — account, coin, price, size, side, closed PnL, fees, timestamps |

## Methodology

1. **Data ingestion & validation** — schema checks, null/date validation, merge integrity check
2. **Sentiment-trade alignment** — trades joined to daily sentiment on date (99.997% match rate)
3. **Performance analysis** — win rate and average PnL per trade across five sentiment classes
4. **Risk exposure analysis** — position sizing behavior by sentiment regime
5. **Risk-adjusted metrics** — profit factor, Sharpe ratio, max drawdown, ROI computed per regime
6. **Trader segmentation** — ranking accounts by total PnL; identifying regime-agnostic and contrarian-strength traders
7. **Statistical testing** — Kruskal-Wallis test with epsilon-squared effect size to validate that observed differences are non-random
8. **Directional bias, asset-level, and temporal analysis** — supplementary checks on whether effects are driven by long/short positioning, individual assets, or time trends

## Key Findings

- Win rate and average PnL per trade are highest in Extreme Greed (89.2%) and lowest in
  Extreme Fear (76.2%) — a 13-point spread.
- Traders take their largest average positions during Fear (~$7,182) despite it being the
  lowest-win-rate regime — a mismatch between position sizing and demonstrated edge.
- Risk-adjusted metrics (profit factor, Sharpe ratio, max drawdown) show the highest-PnL
  regime is not necessarily the most consistent or lowest-risk one.
- A distinct subset of traders is profitable across every sentiment regime; a separate
  subset shows specific contrarian strength during Fear.
- The sentiment-performance relationship is statistically significant (Kruskal-Wallis,
  p < 0.001) but has a small effect size — sentiment is a contributing signal, not a
  dominant predictor.
- Long/short positioning is stable across sentiment regimes; observed effects trace back to
  position sizing and trade quality, not directional bias.
- Asset-level behavior can fully invert the aggregate pattern — at least one heavily-traded
  coin is unprofitable in Fear but strongly profitable in Greed.

## Recommendations

- Apply position-size limits during Fear/Extreme Fear regimes given the lower win rate.
- Use trader segmentation to study regime-agnostic and contrarian trading profiles.
- Treat sentiment as one input among several in any predictive framework, not a standalone signal.
- Validate any sentiment-based strategy overlay at the individual-asset level before applying it portfolio-wide.

## Tech Stack

Python · pandas · numpy · matplotlib · scipy (Kruskal-Wallis test)

## Repository Structure

```
trader_sentiment_analysis_v3.ipynb   # Full analysis notebook (executed, no errors)
trader_sentiment_analysis_v3.html    # Static HTML export for quick viewing
fear_greed_index.csv                 # Sentiment dataset
historical_data.csv                  # Trade-level dataset
```

## Limitations

Single calendar year (2024) of data; 32 accounts may not represent the broader trader
population; statistical tests assume trade-level independence, which is an approximation
given repeated trading by the same accounts. A `leverage` field referenced in the assignment
brief was not present in the delivered dataset — this analysis is scoped to the fields
actually available.
