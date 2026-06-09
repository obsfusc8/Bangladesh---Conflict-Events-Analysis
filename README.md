## Bangladesh Conflict & Demonstration Dynamics (2010–2026)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-20BEFF?logo=kaggle&logoColor=white)](https://www.kaggle.com)
[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![ACLED](https://img.shields.io/badge/Data-ACLED-red)](https://acleddata.com)
[![License](https://img.shields.io/badge/License-Research%20%2F%20Educational-yellow)](https://acleddata.com/terms-of-use/)

> Exploratory data analysis of 16 years of political violence, civilian-targeting, and protest mobilisation in Bangladesh - using the ACLED monthly dataset.

---

## Overview

This notebook dissects the temporal dynamics of armed conflict and civil unrest in Bangladesh from **January 2010 through May 2026** across three ACLED event categories:

| Code | Series | Variables |
|------|--------|-----------|
| `PV` | Political Violence | Events, Fatalities |
| `CT` | Civilian Targeting | Events, Fatalities |
| `DM` | Demonstrations | Events |

The analysis surfaces **seasonal rhythms**, **structural breaks**, **electoral violence cycles**, and the **statistical relationship** between event volume and human cost - producing publication-ready visualisations throughout.

---

## Analysis Sections

| # | Section | What it covers |
|---|---------|----------------|
| 1 | **Data Loading & Preprocessing** | Excel ingestion, date parsing, rolling averages, wide-format merge |
| 2 | **Descriptive Statistics** | Mean, median, std, skewness, kurtosis, CV for all series |
| 3 | **Full Time-Series Overview** | Monthly bars + 3-month & 12-month MAs with annotated political events |
| 4 | **Annual Aggregates & YoY Change** | Grouped bar charts, stacked fatalities, year-on-year % change, fatality rates |
| 5 | **Seasonal Heat-Maps** | Year × Month pivot heatmaps per category |
| 6 | **Monthly Seasonality Profile** | Box-plots + mean trend lines by calendar month |
| 7 | **Correlation Analysis** | Events-vs-fatalities OLS regression + cross-series Pearson matrix |
| 8 | **Distribution Analysis** | Histograms, KDE, Q-Q plots for normality assessment |
| 9 | **Seasonal Decomposition (STL)** | Additive decomposition: observed / trend / seasonal / residual |
| 10 | **Autocorrelation (ACF / PACF)** | 36-lag ACF and PACF for all three series |
| 11 | **Composite Dashboard** | Single-figure synthesis: stacked area, pie share, cumulative fatalities, top-10 months, bubble chart |
| 12 | **Statistical Summary** | Narrative findings and statistical test results |

---

## Key Findings

<details>
<summary><strong>1 · Long-Term Escalation</strong></summary>

All three series show a persistent upward trend across 16 years. Demonstration events grew from ~50–90/month in 2010–2012 to over 200–300/month by 2024–2025. This structural escalation reflects deepening political polarisation rather than reporting artefacts.

</details>

<details>
<summary><strong>2 · The July–August 2024 Rupture</strong></summary>

The student-led uprising against the Hasina government produced the highest civilian-targeting fatality month on record - **268 deaths** in a single month - and political violence events peaked at **334/month** (nearly 4× the pre-2024 average). Post-August 2024 activity shifted to a new, structurally higher baseline.

</details>

<details>
<summary><strong>3 · Electoral Violence Cycles</strong></summary>

Clear spikes cluster around election years - **2013–14** (10th Parliament), **2018** (11th Parliament), and **2024** (12th Parliament) - confirming that Bangladesh's contested electoral politics consistently translates into measurable physical violence.

</details>

<details>
<summary><strong>4 · Seasonality</strong></summary>

November–December consistently registers the highest PV and demonstration activity, coinciding with end-of-year political agitations. May–June shows relative lows in PV. No strong Islamic-calendar seasonality is detectable at monthly granularity.

</details>

<details>
<summary><strong>5 · Events–Fatalities Relationship</strong></summary>

Pearson r (PV) ≈ 0.55–0.65: a moderate positive correlation with a notable fat tail (skewness ~4.0 for PV fatalities). A small number of months account for a disproportionate share of deaths — consistent with episodic mass-casualty events rather than uniformly lethal low-intensity conflict.

</details>

<details>
<summary><strong>6 · Short-Term Persistence</strong></summary>

Statistically significant autocorrelation at lags 1–3 for all series - a violent month tends to be followed by another violent month. The 12-month seasonal lag is weaker but visible.

</details>

<details>
<summary><strong>7 · Demonstration–Violence Decoupling</strong></summary>

Despite aggregate positive correlation (r ≈ 0.7), protests and organised violence show periods of decoupling - most notably during **COVID suppression (2020–21)** and **early 2026** - suggesting the two phenomena respond to different trigger conditions.

</details>

---

## Dependencies

```python
pandas
numpy
matplotlib
seaborn
scipy
statsmodels
openpyxl   # Excel file reading
```

Install all at once:

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels openpyxl
```

---

## Dataset

Data is sourced from the **Armed Conflict Location & Event Data Project (ACLED)**.

```
/kaggle/input/bangladesh-conflict-events/
├── bangladesh_political_violence_events_and_fatalities_by_month-year_as-of-04jun2026.xlsx
├── bangladesh_civilian_targeting_events_and_fatalities_by_month-year_as-of-04jun2026.xlsx
└── bangladesh_demonstration_events_by_month-year_as-of-04jun2026.xlsx
```

Each file contains a `Data` sheet with `Year`, `Month`, `Events`, and (for PV/CT) `Fatalities` columns.

> **Note:** 2026 figures cover January–May only (partial year).

---

## Visualisations

<p align="center">
  <img src="https://i.postimg.cc/6qj1j4wf/fig-01-timeseries.png" alt="Time-series overview" width="100%">
</p>
<p align="center"><em><strong>Fig 1 · Monthly Time-Series Overview</strong>  Event counts (bars) overlaid with 3-month (dashed) and 12-month (white) rolling averages. Shaded bands mark key political periods: the 2013–14 election violence, the 2015 BNP blockade, and the July 2024 student uprising — the sharpest discontinuity in the entire 16-year record.</em></p>

---

<table>
<tr>
<td width="50%">
<img src="https://i.postimg.cc/SRTtTYkq/fig-02-annual.png" alt="Annual aggregates" width="100%">
<p align="center"><em><strong>Fig 2 · Annual Aggregates & YoY Change</strong>  Four panels: grouped event counts, stacked fatality totals, year-on-year % change, and per-event fatality rates. The 2024 column dominates every panel.</em></p>
</td>
<td width="50%">
<img src="https://i.postimg.cc/J7Pg4vJJ/fig-03-heatmap.png" alt="Seasonal heatmaps" width="100%">
<p align="center"><em><strong>Fig 3 · Seasonal Heat-Maps</strong>  Year × Month pivot grids for all three series. Q4 cells consistently run hot for political violence; demonstrations scatter more evenly across the calendar.</em></p>
</td>
</tr>
</table>

---

<table>
<tr>
<td width="50%">
<img src="https://i.postimg.cc/Kjqsq3xh/fig-04-seasonality.png" alt="Monthly seasonality" width="100%">
<p align="center"><em><strong>Fig 4 · Monthly Seasonality Profile</strong>  Box-plots aggregated across all years with means marked by white diamonds. Right-skewed boxes across November–December confirm the end-of-year political agitation cycle.</em></p>
</td>
<td width="50%">
<img src="https://i.postimg.cc/PJ3F3vTk/fig-05-scatter.png" alt="Events vs fatalities regression" width="100%">
<p align="center"><em><strong>Fig 5 · Events vs. Fatalities (OLS)</strong>  Points coloured by year on a plasma scale. The loose scatter and fat upper tail signal non-linear, shock-driven lethality — most months cluster low; a handful of crisis months pull the regression line steeply.</em></p>
</td>
</tr>
</table>

---

<table>
<tr>
<td width="50%">
<img src="https://i.postimg.cc/Pf2cr9Zv/fig-06-corrmat.png" alt="Correlation matrix" width="100%">
<p align="center"><em><strong>Fig 6 · Cross-Series Correlation Matrix</strong>  Lower-triangle Pearson heatmap. PV and CT events are tightly coupled (r ≈ 0.8+), while demonstrations show moderate positive co-movement — but their periodic decoupling is what makes the series analytically interesting.</em></p>
</td>
<td width="50%">
<img src="https://i.postimg.cc/Dy0NW6Pz/fig-07-distributions.png" alt="Distributions" width="100%">
<p align="center"><em><strong>Fig 7 · Distribution Analysis</strong>  Histograms with KDE overlays and Q-Q plots. All three series are right-skewed and leptokurtic; the long right tails are driven almost entirely by 2024 crisis months.</em></p>
</td>
</tr>
</table>

---

<p align="center">
  <img src="https://i.postimg.cc/2SBXG5tc/fig-08-decomposition.png" alt="STL decomposition" width="100%">
</p>
<p align="center"><em><strong>Fig 8 · STL Seasonal Decomposition</strong>  Additive decomposition across all three series (rows) into observed, trend, seasonal, and residual components (columns). The trend panel reveals the structural upward shift post-2020; the seasonal component shows the recurring annual pulse independent of crisis spikes.</em></p>

---

<p align="center">
  <img src="https://i.postimg.cc/02j46n0s/fig-09-acf.png" alt="ACF and PACF" width="100%">
</p>
<p align="center"><em><strong>Fig 9 · Autocorrelation (ACF) & Partial Autocorrelation (PACF)  36 Lags</strong> — Significant spikes at lags 1–3 confirm short-term persistence: a violent month predicts the next. The 12-month seasonal echo is weaker but visible, reflecting Bangladesh's annual political calendar.</em></p>

---

<p align="center">
  <img src="https://i.postimg.cc/Cxf67KtV/fig-10-dashboard.png" alt="Composite dashboard" width="100%">
</p>
<p align="center"><em><strong>Fig 10 · Composite Intelligence Dashboard</strong>  A single publication-ready frame synthesising all three series: stacked area overview with fatality trend, event-share pie, cumulative fatality curves, top-10 deadliest months, annual bubble chart (bubble size ∝ total fatalities), and mean monthly profiles — everything needed for a briefing at a glance.</em></p>

---

## Highlighted Political Events

The time-series visualisations annotate the following periods:

| Period | Event |
|--------|-------|
| 2013–2014 | Election Violence (10th Parliament) |
| Jan–Jun 2015 | BNP Blockade Campaign |
| Nov 2018–Jan 2019 | 11th Parliamentary Elections |
| Oct–Dec 2021 | Durga Puja Communal Violence |
| Jul–Sep 2024 | Student-Led Uprising / Hasina Ouster |
| Dec 2024–Jan 2025 | Post-Transition Political Shift |

---

## Attribution & Usage

Data sourced from the **Armed Conflict Location & Event Data Project (ACLED)**  [acleddata.com](https://acleddata.com).

This notebook is compiled for **research and educational use only**. All underlying data rights are reserved by ACLED. Cite as:

```
ACLED (2026). Bangladesh Conflict Data. Armed Conflict Location & Event Data Project.
Retrieved June 2026, from https://acleddata.com
```

---

## Contributing

Suggestions, additional analyses, or extended datasets are welcome via pull request or issue.
