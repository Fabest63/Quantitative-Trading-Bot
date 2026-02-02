# Quantitative Mean-Reversion Trading System

**Status:** Proprietary / Closed Source
**Tech Stack:** Python, Pandas, NumPy, REST APIs

## Project Overview
This repository hosts the documentation for a proprietary algorithmic trading system designed for high-frequency execution in cryptocurrency markets. The system identifies mean-reversion opportunities using statistical arbitrage techniques.

## Key Modules (Architecture)
* **Data Ingestion:** Real-time websocket connection for tick-data retrieval.
* **Signal Engine:** Custom implementation of Ornstein-Uhlenbeck process for mean calculation.
* **Execution Core:** Low-latency order management system (OMS) with rate-limit handling.
* **Risk Manager:** Dynamic position sizing based on volatility (ATR) and drawdown limits.

## Performance Metrics (Backtest)
* **Period:** 2019 - 2024
* **Sharpe Ratio:** > 2.0 (Theoretical)
* **Max Drawdown:** < 15%

---
**Note:** *The source code for this project is currently private due to commercialization and intellectual property (IP) constraints. For technical inquiries regarding the architecture, please contact me directly.*
