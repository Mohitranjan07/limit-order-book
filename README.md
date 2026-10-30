# Limit Order Book — Trading Dashboard & Strategy Lab

An interactive quantitative trading research platform and market data dashboard built with **Plotly Dash** and **Python**.

This application simulates and visualizes real-time market microstructure, order book dynamics, econometric signals, and quantitative execution strategies.

---

## Features

- **Interactive LOB Depth Chart**: Dynamic 5-level bid/ask mountain depth visualization with an interactive timeline scrubber and playback animation controls.
- **P&L & Drawdown Analytics**: Tracks equity curves, per-tick returns, running drawdowns, and comprehensive risk metrics (Annualized Return, Sharpe, Sortino, Calmar, Max Drawdown, Probabilistic Sharpe Ratio (PSR), and Deflated Sharpe Ratio (DSR)).
- **Order Flow Imbalance (OFI)**: Rolling multi-level order flow tracking based on Cont, Kukanov & Stoikov (2014) with regression slope ($\beta$) price impact estimates.
- **HMM Market Regime Detection**: Unsupervised 2-state Gaussian Hidden Markov Model (Baum-Welch algorithm & Viterbi decoding) classifying low-volatility vs. high-volatility market regimes.
- **Strategy Comparison Lab**: Runs side-by-side evaluations of four distinct algorithmic strategies on a structured synthetic market:
  - **Moving Average Crossover** (Trend-following)
  - **OFI Momentum** (Order book pressure)
  - **Buy & Hold** (Passive benchmark)
  - **Mean Reversion** (Price deviation fading)

---

## Quick Start

### 1. Prerequisites
- **Python 3.10+** (Tested and verified up to Python 3.14)
- Git

### 2. Clone and Setup Environment

```bash
git clone https://github.com/Mohitranjan07/limit-order-book.git
cd limit-order-book

# Create a virtual environment
python -m venv .venv

# Activate the virtual environment
# Windows (PowerShell):
.\.venv\Scripts\Activate.ps1
# Windows (cmd.exe):
.\.venv\Scripts\activate.bat
# Linux / macOS:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

---

## Running the Application

### Development Server (Plotly Dash)

**Windows (PowerShell):**
```powershell
$env:PYTHONPATH = "python"
python python/dashboard/app.py
```

**macOS / Linux:**
```bash
PYTHONPATH=python python python/dashboard/app.py
```

Once running, navigate to:
```
http://localhost:8050
```

---

### Production WSGI Server

The project includes `wsgi.py` and supports cross-platform production WSGI deployment:

- **Windows (using Waitress):**
  ```powershell
  $env:PYTHONPATH = "python"
  waitress-serve --listen=127.0.0.1:8050 wsgi:server
  ```

- **Linux / macOS (using Gunicorn):**
  ```bash
  PYTHONPATH=python gunicorn wsgi:server --bind 0.0.0.0:8050
  ```

---

### Standalone Strategy Lab Simulation

To run the out-of-sample backtest comparison across multiple seeds directly in the terminal:

**Windows (PowerShell):**
```powershell
$env:PYTHONPATH = "python"
python python/backtester/strategy_lab.py
```

**macOS / Linux:**
```bash
PYTHONPATH=python python python/backtester/strategy_lab.py
```

---

## Project Structure

```
limit-order-book/
├── python/
│   ├── dashboard/              # Plotly Dash web application
│   │   ├── app.py              # Main dashboard application entry point
│   │   ├── replay_generator.py # Synthetic session data generator
│   │   ├── lob_depth_chart.py  # LOB Depth visualization
│   │   ├── ofi_panel.py        # Order Flow Imbalance panel
│   │   ├── pnl_panel.py        # P&L and drawdown charts
│   │   ├── regime_panel.py     # HMM regime classification
│   │   ├── strategy_panel.py   # Strategy comparison plots
│   │   └── assets/             # CSS styling and dark theme
│   ├── backtester/             # Event-driven backtester & strategy lab
│   │   ├── engine.py           # Core simulation engine and order types
│   │   ├── portfolio.py        # Position tracking and PnL accounting
│   │   ├── strategy_lab.py     # Multi-strategy benchmark runner
│   │   └── tearsheet.py        # Performance reporting
│   ├── microstructure/         # Market microstructure models (OFI, etc.)
│   ├── signals/                # Quantitative signal generation & HMM
│   ├── execution/              # Execution algorithms (VWAP, TWAP, Almgren-Chriss)
│   ├── risk/                   # Risk management & Kelly criterion sizers
│   └── validation/             # Cross-validation & statistical testing
├── pyproject.toml              # Project configuration and metadata
├── requirements.txt            # Python dependencies (Waitress & Gunicorn compatible)
├── wsgi.py                     # WSGI production server entry point
├── .gitignore                  # Git ignore rules
└── README.md                   # Documentation
```

---


