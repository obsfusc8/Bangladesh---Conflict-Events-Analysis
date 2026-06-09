## Bangladesh Conflict & Demonstration Dynamics (2010–2026)

[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-20BEFF?logo=kaggle&logoColor=white)](https://www.kaggle.com)
[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![ACLED](https://img.shields.io/badge/Data-ACLED-red)](https://acleddata.com)
[![License](https://img.shields.io/badge/License-Research%20%2F%20Educational-yellow)](https://acleddata.com/terms-of-use/)

> Exploratory data analysis of 16 years of political violence, civilian-targeting, and protest mobilisation in Bangladesh — using the ACLED monthly dataset.

---

## Overview

This notebook dissects the temporal dynamics of armed conflict and civil unrest in Bangladesh from **January 2010 through May 2026** across three ACLED event categories:

| Code | Series | Variables |
|------|--------|-----------|
| `PV` | Political Violence | Events, Fatalities |
| `CT` | Civilian Targeting | Events, Fatalities |
| `DM` | Demonstrations | Events |

The analysis surfaces **seasonal rhythms**, **structural breaks**, **electoral violence cycles**, and the **statistical relationship** between event volume and human cost — producing publication-ready visualisations throughout.

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

The student-led uprising against the Hasina government produced the highest civilian-targeting fatality month on record — **268 deaths** in a single month — and political violence events peaked at **334/month** (nearly 4× the pre-2024 average). Post-August 2024 activity shifted to a new, structurally higher baseline.

</details>

<details>
<summary><strong>3 · Electoral Violence Cycles</strong></summary>

Clear spikes cluster around election years — **2013–14** (10th Parliament), **2018** (11th Parliament), and **2024** (12th Parliament) — confirming that Bangladesh's contested electoral politics consistently translates into measurable physical violence.

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

Statistically significant autocorrelation at lags 1–3 for all series — a violent month tends to be followed by another violent month. The 12-month seasonal lag is weaker but visible.

</details>

<details>
<summary><strong>7 · Demonstration–Violence Decoupling</strong></summary>

Despite aggregate positive correlation (r ≈ 0.7), protests and organised violence show periods of decoupling — most notably during **COVID suppression (2020–21)** and **early 2026** — suggesting the two phenomena respond to different trigger conditions.

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

## Output Figures

| File | Description |
|------|-------------|
| `fig_01_timeseries.png` | Full monthly time series with rolling averages & event annotations |
| `fig_02_annual.png` | Annual aggregates, fatality stacks, YoY change, fatality rates |
| `fig_03_heatmap.png` | Year × Month seasonal heat-maps |
| `fig_04_seasonality.png` | Monthly box-plots and mean trends |
| `fig_05_scatter.png` | Events vs. fatalities regression plots |
| `fig_06_corrmat.png` | Cross-series Pearson correlation matrix |
| `fig_07_distributions.png` | Distribution histograms and Q-Q plots |
| `fig_08_decomposition.png` | STL decomposition panels (3 × 4) |
| `fig_09_acf.png` | ACF and PACF plots (36 lags) |
| `fig_10_dashboard.png` | Composite intelligence dashboard |

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

Data sourced from the **Armed Conflict Location & Event Data Project (ACLED)** — [acleddata.com](https://acleddata.com).

This notebook is compiled for **research and educational use only**. All underlying data rights are reserved by ACLED. Cite as:

```
ACLED (2026). Bangladesh Conflict Data. Armed Conflict Location & Event Data Project.
Retrieved June 2026, from https://acleddata.com
```

---

## Contributing

Suggestions, additional analyses, or extended datasets are welcome via pull request or issue.
