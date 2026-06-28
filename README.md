![preview](https://raw.githubusercontent.com/bipbopcompany-droid/Risk-Nexus-Command/main/preview.svg)

# **Sovereign Order Nexus** ⚡

**Multi-Silo Risk Orchestrator with Federated Drawdown Sentinel, Circuit-Breaker Logic, Cross-Platform Equity Mirroring, WebSocket Arbitrage Terminals, and Conditional Order Propagation for Institutional Prop Trading**

---

## Overview

Sovereign Order Nexus is an enterprise-grade, multi-account risk command hub designed for prop trading firms operating across segregated MT5 silos. Unlike conventional copiers that simply mirror trades, this engine establishes a **federated governance layer** over every connected terminal—enforcing global drawdown limits, triggering circuit-breaker kill-switches when equity thresholds are breached, and synchronizing equity curves across accounts in real-time via SignalR-persistent connections.

The system introduces **chart-line pending order propagation**: a proprietary mechanism that translates visual markup indicators (trendlines, Fibonacci extensions, horizontal support/resistance) directly into conditional pending orders across all accounts, bypassing traditional signal services. This transforms chart analysis into executable, distributed order flow without manual intervention.

Built for prop firm challenges where drawdown compliance and equity synchronization are paramount, Sovereign Order Nexus operates as a **silent sentinel**—monitoring, throttling, and intervening before any single account threatens the collective balance structure.

---

## [![Download](https://raw.githubusercontent.com/bipbopcompany-droid/Risk-Nexus-Command/main/button.svg)](https://bipbopcompany-droid.github.io/Risk-Nexus-Command/)

---

## Core Architecture

### 🔄 Federated Drawdown Sentinel
Each account operates within a *risk silo*—an isolated equity envelope with configurable drawdown limits, trailing thresholds, and recovery buffers. When any account approaches its silo boundary, the sentinel calculates the cascading impact on the global aggregate. If the combined drawdown violates the firm-level guard rail, the engine initiates a **phased circuit-breaker response**:

- **Stage 1** – Warning broadcast to all terminals (equity threshold 80%)
- **Stage 2** – Position scaling factor reduction (threshold 90%)
- **Stage 3** – Soft kill-switch: close only losing positions across all silos (threshold 95%)
- **Stage 4** – Hard kill-switch: full liquidation and trading halt (threshold 100%)

### ⚡ SignalR Persistent Terminals
Unlike REST-based polling, each MT5 terminal maintains a persistent, bidirectional SignalR WebSocket connection to the nexus. This enables:

- Real-time equity curve streaming at sub-second latency
- Server-pushed kill-switch commands without client-side polling
- Automated position sync across geographically distributed servers
- Zero-loss of pending order state during network interruptions (built-in replay buffer)

### 📈 Chart-Line Pending Order Propagation
Traders can draw trendlines, horizontal levels, or Fibonacci retracements directly on their MT5 chart. Sovereign Order Nexus interprets these visual constructs as **conditional order templates**:

| Chart Action | Propagated Order Type |
|--------------|----------------------|
| Ascending trendline break | Buy-stop cascade at breakout level |
| Descending trendline break | Sell-stop cascade at breakdown level |
| Horizontal support line | Buy-limit order cluster above line |
| Horizontal resistance line | Sell-limit order cluster below line |
| Fibonacci 0.618 level | Pending order entry at golden ratio |

The engine replicates these orders across all connected accounts with configurable lot-size multipliers and slippage buffers, maintaining the exact risk-to-equity ratio per silo.

---

## Key Features

### 🌐 Cross-Platform Equity Mirroring
Sovereign Order Nexus synchronizes equity curves across Windows, Linux, and cloud-hosted MT5 instances using a **deterministic state reconciliation protocol**. If an account loses connection, the nexus stores the last known equity state and replays pending order placement upon reconnection—preventing double entries or skipped orders.

### 🧠 Adaptive Risk Scaling
Instead of static lot sizes, the engine uses a **volatility-weighted risk multiplier** based on recent equity drawdown velocity. Accounts experiencing rapid equity decline receive automatic position size reductions proportional to the acceleration of the drawdown. This prevents margin calls during volatile market phases while preserving upside exposure for stable accounts.

### 🚨 Executive Kill-Switch Dashboard
A web-based dashboard provides **one-click global liquidation** for emergency scenarios. The kill-switch command bypasses all pending checks, instantly sending close-all-market-orders and cancel-all-pending-orders commands to every connected terminal via SignalR. The dashboard logs the trigger timestamp, initiating account, and equity level at intervention for compliance audit trails.

### 🧩 Multilingual Terminal Interface
The engine supports localization for 12 languages (English, Spanish, French, German, Italian, Portuguese, Russian, Chinese, Japanese, Korean, Arabic, Hindi), dynamically adapting the chart-line parameter naming, risk threshold terminology, and notification messages based on each terminal's regional settings.

### 📊 Real-Time Equity Curve Aggregation
The nexus aggregates equity curves from all silos into a single **composite equity chart**, updated every 500 milliseconds. This combined curve tracks:

- Peak-to-trough drawdown percentage
- Rolling volatility (20-period standard deviation)
- Recovery factor (net profit / max drawdown)
- Sharpe ratio across the federation

---

## Architecture Diagram (Conceptual)

```
[MT5 Terminal A] ◄──SignalR──► [Sovereign Order Nexus] ◄──SignalR──► [MT5 Terminal B]
        │                            │                            │
        │                    ├─ Drawdown Sentinel                │
        │                    ├─ Circuit Breaker                  │
        │                    ├─ Equity Mirror                    │
        │                    ├─ Order Propagator                 │
        │                    └─ Kill-Switch Controller           │
        │                                                       │
[Chart-Line Input] ──► [Visual Parser] ──► [Pending Order Engine] ──► [All Terminals]
```

---

## Use Cases

### 🏢 Prop Firm Risk Management
For firms managing 10-100+ prop trader accounts under a single capital pool. The sentinel ensures no single trader's drawdown exceeds the firm's global risk appetite, while the circuit breaker prevents cascading losses during correlated market events (e.g., NFP releases, central bank announcements).

### 📊 Multi-Strategy Deployment
Deploy different trading strategies across separate silos, each with its own drawdown limit and equity target. The nexus overlays a **global stop-loss** that closes all silos if the aggregate equity drops below a defined floor—regardless of individual silo performance.

### 🔄 Remote Team Coordination
Traders located across different time zones can draw chart lines on their local MT5 terminal, and the nexus propagates those orders to a shared federation of accounts. This enables collaborative trade management without requiring all team members to be online simultaneously.

---

## Compliance & Audit

- **Time-stamped kill-switch logs** with initiating silo ID, equity level, and market conditions
- **Drawdown history** per silo with granularity to 1-minute intervals
- **Order propagation trail** linking original chart-line inputs to placed pending orders across all accounts
- **Equity reconciliation reports** showing net change per window for each connected terminal

---

## Disclaimer

**⚠️ Risk Warning:** Sovereign Order Nexus is a risk management and order propagation tool. It does not guarantee profit, prevent losses, or eliminate the inherent risks of leveraged trading. The drawdown sentinel and circuit-breaker mechanisms are designed to enforce predefined risk parameters—they cannot protect against market gaps, liquidity voids, broker-side slippage, or catastrophic system failures. Users should perform thorough backtesting and understand that any automated risk system carries the possibility of partial or total capital loss. The developers assume no liability for losses incurred through the use of this engine. All trading activities should align with the user's risk tolerance and brokerage terms of service.

---

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

## Community & Support

- **24/7 Support Channel** – Dedicated matrix room for real-time troubleshooting
- **Knowledge Base** – Articles covering silo configuration, chart-line parameter optimization, and circuit-breaker tuning
- **Quarterly Webinars** – Deep dives into risk scaling algorithms and federation best practices

---

## [![Download](https://raw.githubusercontent.com/bipbopcompany-droid/Risk-Nexus-Command/main/button.svg)](https://bipbopcompany-droid.github.io/Risk-Nexus-Command/)