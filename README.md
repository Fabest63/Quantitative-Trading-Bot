# 🧠 Deep Q-Network (DDQN) Quantitative Trading System

![Status](https://img.shields.io/badge/Status-Proprietary%20%2F%20Commercial-red)
![Architecture](https://img.shields.io/badge/Architecture-Event--Driven-orange)
![Model](https://img.shields.io/badge/Model-Double%20DQN-blueviolet)
![Environment](https://img.shields.io/badge/Environment-Custom%20Gymnasium-success)

## 📖 Project Overview

This repository documents the architecture and performance metrics of a proprietary **Deep Reinforcement Learning (DRL)** agent designed for autonomous high-frequency trading in Forex and Equity markets.

Unlike traditional heuristic strategies, this system utilizes a **Double Deep Q-Network (DDQN)** to learn optimal execution policies ($\pi^*$) directly from high-dimensional market data. The agent is trained within a **custom-built simulation environment** that rigorously models market microstructure to prevent look-ahead bias and ensure realistic policy transfer.

> **Note:** The source code, model weights (`.pth`), and hyperparameter configurations are **private** due to commercial intellectual property constraints.

---

## 🏗 System Architecture

The system is built on a modular, event-driven architecture using Python 3.10+ and PyTorch. It is designed for low-latency inference and high-throughput data ingestion.



### 1. Data Pipeline & Feature Engineering
* **Ingestion:** Real-time Websocket clusters (`asyncio`) handling L2/L3 order book data.
* **Preprocessing:** On-the-fly normalization (Z-Score) and feature extraction using rolling windows.
* **State Space ($S_t$):** A continuous vector combining:
    * **Market Microstructure:** Order flow imbalance, tick velocity, spread dynamics.
    * **Technical Indicators:** RSI, MACD, Bollinger Bands (dynamic), ATR.
    * **Macro Context:** Volatility indices (VIX) and correlation matrices.

### 2. The Agent (Double DQN)
To mitigate the maximization bias inherent in standard Q-Learning, the agent employs a **Double DQN** architecture:
* **Separation of Concerns:** Uses the *Online Network* to select actions and the *Target Network* to evaluate them.
* **Dueling Network Structure:** Splits the Q-value estimation into two streams:
    * $V(s)$: Value of the state.
    * $A(s, a)$: Advantage of each action.
* **Prioritized Experience Replay (PER):** Samples transitions with high TD-error more frequently to learn from "surprise" events.

---

## 🌍 Proprietary Simulation Environment (Custom Gym)

A critical component of this project is the **custom OpenAI Gym (Gymnasium) environment**, built from scratch to simulate realistic market conditions. Standard open-source wrappers often fail to model execution costs accurately.

### Key Simulation Features
* **Realistic Execution:**
    * **Dynamic Spreads:** Trades are executed at Ask/Bid, not Mid-price.
    * **Slippage Model:** Impact calculated as a function of trade size vs. available liquidity depth.
    * **Latency Simulation:** Introduces stochastic delays between signal and execution.
* **Reward Engineering:**
    * Optimization target is **Differential Sharpe Ratio** rather than raw PnL.
    * Penalties for high drawdown variance and excessive portfolio turnover (churning).
## 🛠 Tech Stack

* **Core Language:** `Python 3.10+`
* **Deep Learning:** `PyTorch` (CUDA optimized for GPU training).
* **RL Framework:** `Stable-Baselines3` / Custom `Gymnasium` implementation.
* **Data Processing:** `Pandas`, `NumPy`, `TA-Lib`.
* **Optimization:** `Optuna` (Hyperparameter tuning).

---

## 🔒 License & Copyright

**Copyright © 2025 Alisium. All Rights Reserved.**

This software, including the architectural design, custom environment logic, and trained model weights, is the proprietary intellectual property of the author.

* **Strictly Closed Source:** The source code is not available for public use.
* **No Commercial Use:** Unauthorized copying, distribution, reverse engineering, or commercial deployment of this system or its documentation is strictly prohibited.
* **Inquiries:** For technical due diligence regarding the architecture or commercial licensing, please contact me directly.

---

### ⚠️ Risk Disclosure
**Experimental Technology.** Reinforcement Learning models in finance are stochastic. Past performance in simulation does not guarantee future results in live markets due to changing market regimes, liquidity constraints, and execution latency. This repository is for engineering demonstration purposes only and does not constitute financial advice.

