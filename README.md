# 📉 Stock Market Crash Analysis

## Overview

In this project, we analyzed **30 years of historical Indian stock market data**, focusing on the **BSE Sensex** to identify, understand, and visualize market crash patterns.
We explored how historical downturns like those in **1997**, **2008–2009**, and **2020** evolved, and developed an **Early Warning System (EWS)** to detect potential signs of future market stress using rolling return and volatility metrics.

---

## 📊 Data Preparation

We began by **loading and cleaning** the Sensex dataset (`sensex.csv`).
The first row contained invalid column headers, which we removed. We then:

* Converted the `'Price'` column to datetime (renamed as `'Date'`),
* Sorted the data by date, and
* Set `'Date'` as the DataFrame index for time series analysis.

This process resulted in a clean dataset of **6,835 daily records** spanning from **1997 to 2025**, with columns for **Close**, **High**, **Low**, **Open**, and **Volume**.

---

## 📈 Step 1: Analyzing Daily Returns

We calculated the **daily percentage change** in closing prices to measure short-term market fluctuations:

```python
df['Daily_Return'] = df['Close'].pct_change() * 100
```

A daily crash was defined as a **drop greater than or equal to 5%**.
Using **Plotly visualizations**, we highlighted these crash days on the Sensex closing price chart.

### Insight:

* Major daily crashes aligned with **global or domestic financial crises**, particularly during **2008** and **2020**.
* Despite several sharp declines, the Sensex displayed **long-term resilience and upward recovery** over the decades.

---

## 📉 Step 2: Analyzing Drawdowns

We computed the **cumulative maximum** and **drawdown**, representing how far the index fell from its historical peak:

```python
df['Cumulative_Max'] = df['Close'].cummax()
df['Drawdown'] = (df['Close'] - df['Cumulative_Max']) / df['Cumulative_Max'] * 100
```

We visualized drawdowns over time and highlighted periods exceeding **-20%**.

### Insight:

* Severe drawdowns appeared around **1997–1998**, **2000–2001**, **2008–2009**, and **2020**, often exceeding **-50%**.
* Each deep trough corresponded to a **major global or domestic economic crisis**.

---

## 🧩 Step 3: Identifying Crash Clusters

We grouped **contiguous crash days** (within three days apart) into clusters to capture continuous periods of market stress.
Each cluster was defined by a start and end date.

### Example Output:

```
Cluster 1: 1997-11-12 to 1997-12-26 (Total days: 31)
Cluster 49: 2008-08-18 to 2009-01-23 (Total days: 116)
Cluster 79: 2020-03-16 to 2020-04-03 (Total days: 19)
```

### Insight:

* Clusters captured **the duration and intensity** of each market downturn.
* Longer clusters like **2008–2009** reflected **prolonged market instability**, while shorter ones like **2020** reflected **sharp but brief collapses**.

---

## 🔍 Step 4: Visualizing Crash Periods

We zoomed into the **1997**, **2008–2009**, and **2020** crash clusters to visualize:

* **Closing Prices**
* **Daily Returns**
* **Drawdowns**

Each visualization included a 30-day window before and after the crash to capture build-up and recovery phases.

### Insight:

* The **1997 crash** showed a moderate yet extended decline.
* The **2008–2009 crash** was the **most severe**, with returns plummeting amid the global financial crisis.
* The **2020 crash**, though steep, was followed by a **quicker recovery**, illustrating improved market adaptability.

---

## ⚠️ Step 5: Developing an Early Warning System (EWS)

We designed an **Early Warning System** using **rolling statistics** of returns and volatility.

We simulated synthetic **2025 market data** (250 trading days) to test the system, generating three phases:

1. Stable growth (normal volatility),
2. Pre-crash stress (negative drift, rising volatility),
3. Post-crash recovery.

We computed:

* **10-day Rolling Mean Return**
* **10-day Rolling Volatility**

An early warning was triggered when:

* Rolling mean return < **-0.5%**
* Rolling volatility > **2%**

### Example Warning Output:

```
2025-08-13  Mean Return: -0.72% | Volatility: 2.31%
2025-09-23  Mean Return: -1.37% | Volatility: 2.00%
2025-09-29  Mean Return: -1.32% | Volatility: 2.02%
```

### Insight:

* Warning signals appeared **shortly before and during the crash**, confirming their **predictive potential**.
* The EWS provided a **data-driven approach to risk management**, alerting analysts to abnormal volatility patterns before severe losses occurred.

---

## 📘 Summary of Key Insights

1. **Historical Resilience:**
   Despite recurring crashes, the Sensex consistently rebounded to new highs, showing strong market recovery behavior.

2. **Crisis Patterns:**
   Major drawdowns typically coincided with **global crises**—Asian Financial Crisis (1997), Global Financial Crisis (2008), and COVID-19 Pandemic (2020).

3. **Early Warning Effectiveness:**
   Rolling return and volatility metrics successfully flagged **pre-crash warning zones**, highlighting their value for **proactive market monitoring**.

4. **Behavioral Cycles:**
   Crashes often followed **periods of optimism and low volatility**, underlining the cyclical nature of financial markets.

---

## 🧭 Conclusion

This project demonstrated how **quantitative analysis** can uncover critical insights about **market dynamics** and **crash behavior** over decades.
By combining traditional metrics (like drawdown and daily returns) with **rolling statistical indicators**, we were able to build a **simple yet effective early warning model**.

Such analytical frameworks empower **data scientists, traders, and financial analysts** to:

* Detect early signs of instability,
* Understand the anatomy of crashes, and
* Develop more **robust risk management strategies**.

Ultimately, this analysis reaffirmed that while **market crashes are inevitable**, **data-driven insights** can significantly reduce their impact.
