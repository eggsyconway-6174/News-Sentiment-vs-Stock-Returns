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

   ## 🧠 Methodology

The project follows a simple but robust pipeline:

1. **Data Acquisition**  
   - `ultra_robust` script: tries to fetch real headlines (via `yfinance.Ticker.news`) and real daily returns (via `yfinance.download`).  
   - If either fails, it seamlessly switches to **synthetic data** (random walk returns + weakly correlated sentiment).

2. **Sentiment Scoring**  
   - If `transformers` and `torch` are installed, it uses **FinBERT** (a financial domain BERT model) for state‑of‑the‑art sentiment.  
   - Otherwise, it falls back to **VADER** (rule‑based, fast but less accurate).

3. **Data Alignment**  
   - Headlines are aggregated to daily average sentiment per ticker.  
   - Merged with daily returns on `date` and `ticker`.

4. **Lag Analysis**  
   - A `return_tomorrow` column is created by shifting returns one day forward per ticker.  
   - This allows measuring if **today's sentiment predicts tomorrow's return**.

5. **Correlation & Visualisation**  
   - Pearson correlation coefficients are computed for both same‑day and next‑day relationships.  
   - Scatter plots with regression lines show the trend.  
   - Time‑series plots overlay sentiment and returns for a chosen ticker.

   ## 📊 Example Output

### Same‑Day Sentiment vs Return
![Same‑day plot](sentiment_vs_returns_sameday.png)

### Next‑Day Sentiment vs Return
![Next‑day plot](sentiment_vs_returns_nextday.png)

### Time Series (AAPL)
![AAPL timeseries](AAPL_timeseries.png)

## ⚙️ Customisation

You can easily modify the analysis by editing the configuration section at the top of each script:

```python
TICKERS = ['AAPL', 'TSLA', 'NVDA', 'MSFT', 'GOOGL']   # Add or remove tickers
END_DATE = datetime.now().date()                       # Change end date
START_DATE = END_DATE - timedelta(days=30)             # Adjust lookback period


## ❓ Troubleshooting

| Problem | Solution |
|---------|----------|
| `ModuleNotFoundError: No module named 'transformers'` | Install with `pip install transformers torch` or let the script fall back to VADER. |
| Yahoo Finance returns no data | The script auto‑switches to synthetic mode – this is expected during market holidays or rate limiting. |
| FinBERT loads slowly | First download is large (~500 MB); subsequent runs are fast. |
| Plots not showing | Ensure you have a GUI backend (e.g., `pip install PyQt5`) or save plots are saved as PNG. |
