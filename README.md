# 📈 News Sentiment vs Stock Returns – Mini Research Project

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A self‑contained data science project that explores the correlation between daily news sentiment and stock returns.  
It features **two robust Python scripts** – one that attempts to fetch real data (with automatic fallback to synthetic) and one that runs entirely on synthetic data. No API keys required!

---

## 🔍 What This Project Does
- Fetches (or generates) daily **stock returns** for a configurable list of tickers (AAPL, TSLA, NVDA, MSFT, GOOGL).
- Scores news headlines using **FinBERT** (or VADER as fallback) – if real headlines are available.
- If real data is unavailable, generates realistic **synthetic returns** (random walk) and **synthetic sentiment** weakly correlated with returns.
- Computes **same‑day** and **next‑day** (lag‑1) Pearson correlations.
- Produces publication‑ready **scatter plots**, **regression lines**, and **time‑series visualisations**.
- Saves all plots as high‑resolution PNG files.

---

## 🚀 Two Scripts – Choose Your Flavour

| Script | Description | When to Use |
|--------|-------------|-------------|
| **`sentiment_ultra_robust.py`** | Tries to fetch real news (via yfinance) and real returns. If either fails, falls back to synthetic data. Uses FinBERT/VADER for sentiment. | You want to attempt real data but guarantee the code always runs. |
| **`sentiment_synthetic.py`** | 100% synthetic – generates returns and sentiment instantly. No external dependencies beyond standard data science libraries. | You want a guaranteed quick demo, or you're testing the pipeline without internet. |

Both scripts produce the **same outputs** (correlations, plots, statistics) so you can compare the results.

---

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/eggsyconway-6174/news-sentiment-stocks.git
   cd news-sentiment-stocks


   🚀 News Sentiment vs Stock Returns (Fully Synthetic Demo)
📅 Period: 2026-02-07 to 2026-03-09 (21 trading days)
📈 Tickers: AAPL, TSLA, NVDA, MSFT, GOOGL
============================================================
🔄 Generating synthetic returns...
🔄 Generating synthetic sentiment...

📊 Merged data: 105 rows

🔗 Overall Pearson correlation (same‑day): 0.3124
🔗 Overall Pearson correlation (sentiment → next day return): 0.0452

📈 Per‑ticker correlations:
   AAPL (same‑day): 0.2871 (n=21)
   AAPL (next‑day): 0.0321 (n=20)
   ...
