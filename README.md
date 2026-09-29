# 📈 Mutual Fund Plan with Python

A Python data analysis project that builds a **long-term mutual fund plan** from Nifty 50 stock prices. It selects companies with **high return (ROI) and low risk**, assigns each one an investment weight, and projects what a monthly SIP could grow to over 1, 3, 5 and 10 years.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Dataset](#-dataset)
- [Methodology](#-methodology)
- [Results](#-results)
- [SIP Projection](#-sip-projection)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Repository Structure](#-repository-structure)
- [Limitations](#-limitations)
- [Disclaimer](#-disclaimer)
- [Author](#-author)

---

## 🎯 Project Overview

Mutual funds pool money from many investors and spread it across a diversified set of stocks. This project shows, step by step, how such a plan can be designed with data: measure each stock's **risk** and **return**, keep only the stocks that balance both, and weight them so that calmer stocks get more money.

---

## ✅ Objectives

1. Explore Nifty 50 closing prices and check data quality.
2. Measure **volatility (risk)**, **average growth rate**, and **ROI** for every company.
3. Select companies with **above-median ROI** and **below-median volatility**.
4. Allocate investment across the selected companies using **inverse-volatility weighting**.
5. Compare the plan against the highest-growth stocks (risk vs. return trade-off).
6. Project the value of a monthly SIP with a yearly step-up over 1, 3, 5 and 10 years.

---

## 🗂 Dataset

| Item | Detail |
|---|---|
| **File** | `nifty50_closing_prices.csv` |
| **Content** | Daily closing prices (INR) of 49 Nifty 50 companies |
| **Period** | 1 Jan 2024 to 30 May 2025 (348 trading days) |
| **Columns** | `Date` plus one column per ticker (e.g., `RELIANCE.NS`, `TCS.NS`, `HDFCBANK.NS`) |
| **Missing values** | None found |

---

## 🔬 Methodology

| Step | What was done | How |
|---|---|---|
| 1. Load & clean | Read the CSV, convert `Date` to datetime, check nulls | `pandas` |
| 2. Price trends | Line chart of all 49 stocks over time | `plotly` |
| 3. Risk | Standard deviation of closing price per stock | `.std()` |
| 4. Growth | Average daily percentage change per stock | `.pct_change().mean()` |
| 5. ROI | (Final price − Initial price) / Initial price × 100 | Direct calculation |
| 6. Stock selection | ROI **above median** AND volatility **below median** | Boolean filter |
| 7. Weighting | Weight = (1 / volatility) ÷ sum of (1 / volatility) | Inverse-volatility ratio |
| 8. Comparison | Risk and ROI of the plan vs. the top-10 growth stocks | Horizontal bar charts |
| 9. SIP projection | Monthly compounding with a 10% yearly increase in SIP amount | Custom future-value function |

---

## 📊 Results

### Selected companies and investment allocation

Eleven companies met both conditions. Their ROI over the period and the resulting allocation:

| Company | ROI (%) | Allocation (%) |
|---|---|---|
| TATASTEEL | 17.5 | 29.3 |
| ONGC | 24.6 | 15.0 |
| POWERGRID | 27.9 | 12.9 |
| BPCL | 48.3 | 12.5 |
| HDFCLIFE | 20.2 | 6.4 |
| SBIN | 31.4 | 6.3 |
| CIPLA | 18.2 | 4.6 |
| BAJFINANCE | 39.2 | 4.4 |
| ICICIBANK | 45.9 | 3.1 |
| ADANIPORTS | 37.3 | 2.9 |
| SBILIFE | 27.0 | 2.6 |

### Reference lists from the analysis

- **Most volatile stocks:** SHREECEM, BAJAJ-AUTO, DIVISLAB, ULTRACEMCO, MARUTI
- **Highest average daily growth:** BHARTIARTL, M&M, DIVISLAB, BPCL, ADANIPORTS
- **Highest ROI:** BHARTIARTL (84.2%), M&M (76.0%), DIVISLAB (69.9%), BPCL (48.3%), ICICIBANK (45.9%)

### Key insight

There is a clear **risk vs. reward trade-off**. The mutual fund basket has lower volatility and moderate returns, which suits conservative, long-term investors. The high-growth stocks offer higher potential returns but with bigger price swings.

---

## 💰 SIP Projection

Assumptions used in the notebook:

- Starting SIP: **₹5,000 per month**
- SIP amount **increases 10% every year**
- Monthly compounding
- Average annual return of about **13.2%** (an example ROI array of 12.5%, 13.2% and 14.0% is used in the code)

| Period | Total Invested* | Projected Value |
|---|---|---|
| 1 year | ₹60,000 | ₹64,480 |
| 3 years | ₹1,98,600 | ₹4,51,777 |
| 5 years | ₹3,66,306 | ₹13,22,809 |
| 10 years | ₹9,56,246 | ₹72,90,275 |

*Total invested is the sum of all monthly contributions with the 10% yearly step-up.

The takeaway: consistent investing plus compounding grows wealth sharply over the long term.

---

## 🛠 Tech Stack

- **Python 3**
- **pandas** for data handling
- **NumPy** for calculations
- **Plotly** for interactive charts
- **Jupyter Notebook / Google Colab**

---

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   cd <your-repo-name>
   ```
2. Install the dependencies:
   ```bash
   pip install pandas numpy plotly jupyter
   ```
3. Place `nifty50_closing_prices.csv` in the project folder and update the file path in the first code cell, for example:
   ```python
   data = pd.read_csv("nifty50_closing_prices.csv")
   ```
4. Open and run the notebook:
   ```bash
   jupyter notebook mutual_fund_plan.ipynb
   ```

---

## 📂 Repository Structure

```
├── mutual_fund_plan.ipynb          # Main analysis notebook
├── nifty50_closing_prices.csv      # Input data
└── README.md                       # Project documentation
```

---

## ⚠️ Limitations

- **Risk is measured as the standard deviation of price levels**, which is influenced by how high a stock's price is. Using the standard deviation of daily **returns** would give a fairer comparison across stocks.
- **ROI covers about 17 months** and is not annualized.
- The SIP projection uses an **assumed average return (~13.2%)**, not a return computed from the selected stocks.
- The analysis uses **past prices only**; past performance does not guarantee future results.
- No transaction costs, taxes, or fund expense ratios are included.

---

## 📢 Disclaimer

This project is for **educational purposes only** and is not financial advice. Please consult a qualified financial advisor before investing.

---

## 👤 Author

**Your Name**
- GitHub: [@your-username](https://github.com/your-username)
- LinkedIn: [Your Profile](https://linkedin.com/in/your-profile)

---

⭐ If you found this project useful, consider giving the repository a star!
