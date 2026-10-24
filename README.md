# Data Science Fundamentals Mid Project

# Shehryar Khurram (FA25-BDS-045)
# Muhammad Rafay (FA25-BDS-035)
# 3rd Semester
# Supermarket Sales Data Analysis 🛒📊

**Data Science Fundamentals — Midterm Lab Exam Project (R)**

A complete, reproducible data analysis pipeline that takes a **deliberately dirty,
real-world-style supermarket sales export** (12,575 transactions, 2022–2025) and carries
it through every stage of the data science workflow — entirely in R, using only the
tools taught in the course labs (base R + `dplyr` + `tidyr` + base plotting).

> Raw file → Exploration → Descriptive Statistics → Cleaning → Preprocessing →
> Transformation → Visualization → Interpreted Business Findings

---

## 📌 Highlights

| Stage | What was done |
|---|---|
| **Dataset** | 12,575 rows × 11 columns of retail transactions (Kaggle: *Retail Store Sales — Dirty for Data Cleaning*) |
| **Data quality** | 7,229 missing cells detected and resolved — including **609 unit prices recovered algebraically** (`Total ÷ Quantity`) instead of deleted |
| **Statistics** | Full descriptive toolkit: mean, median, mode (via `table()`), variance, SD, IQR, coefficient of variation (73.1% → high-variation spending) |
| **Transformations** | Date decomposition, spending-level binning (`case_when`), min–max normalization, label hygiene (`trimws`) |
| **Visualizations** | 6 base-R charts: histogram, bar chart, boxplot, scatter (r = 0.712), pie, monthly revenue line |
| **Key findings** | Revenue is nearly equal across 8 categories & 3 payment methods; Online vs In-store split 50.5/49.5; stable revenue band with no seasonality |

## 🗂 Repository Structure

```
supermarket-sales-analysis/
├── data/
│   └── retail_store_sales.csv           # raw dataset (Kaggle source)
├── scripts/
│   └── supermarket_sales_analysis.R     # full pipeline — 10 commented sections
├── outputs/
│   ├── cleaned_sales_data.csv           # cleaned + transformed dataset (16 cols)
│   └── plots/                           # the 6 report figures (PNG)
├── report/
│   ├── Supermarket_Sales_Analysis_Report.docx
│   └── Supermarket_Sales_Analysis_Report.pdf
├── supermarket_sales_analysis.Rproj
└── README.md
```

## ▶️ How to Run

1. Open `supermarket_sales_analysis.Rproj` in **RStudio**.
2. Install packages once: `install.packages(c("dplyr", "tidyr"))`
3. Open `scripts/supermarket_sales_analysis.R` and run it **section by section**
   (Ctrl+Enter). Every section prints its results to the console with explanations.
4. Find the cleaned dataset in `outputs/` and the charts in `outputs/plots/`.

*Tested with R 4.4.3, dplyr 1.2.1, tidyr 1.3.2 — no other dependencies.*

## 🧹 Cleaning Decisions (the heart of the project)

| Problem | Rows | Decision |
|---|---|---|
| Blank strings in text columns | 7,229 cells | Converted to proper `NA` (missing ≠ category) |
| Price missing, Total & Quantity present | 609 | **Reconstructed**: `Price = Total / Quantity` — exact algebra, zero data loss |
| Quantity + Total missing together | 604 | Quantity → median (6); Total recomputed — keeps 4.8% of data alive |
| Item missing | 1,213 | Explicit `Unknown Item` label |
| Discount flag missing | 4,199 (33.4%) | New honest level `Not Recorded` (inventing True/False would fabricate facts) |
| Duplicate rows | 0 found | `distinct()` run anyway as a safety net |

Every decision ends with a verifiable audit: **0 missing values** and the identity
`Total.Spent = Price.Per.Unit × Quantity` holding exactly on all 12,575 rows.

## 📊 Key Results

- **Total revenue:** 1,637,367 across 12,575 transactions (avg basket 130.21, median 110)
- **Balanced portfolio:** best category (Butchers, 218,153) earns only ~15% more than the weakest (Milk Products, 189,892)
- **Omnichannel:** Online 50.5% vs In-store 49.5% of transactions
- **Right-skewed spending:** mean > median; CV = 73.1% (high variation)
- **Stable over time:** monthly revenue oscillates in a 39k–52k band with no trend or seasonality

## 📄 Report

The full 20-page project report (with all code, console outputs, statistics tables,
figures and interpretations) is in [`report/`](report/) — available as PDF and DOCX.

## 🙏 Acknowledgements

- Dataset: [Retail Store Sales — Dirty for Data Cleaning](https://www.kaggle.com/datasets/ahmedmohamed2003/retail-store-sales-dirty-for-data-cleaning) by Ahmed Mohamed on Kaggle
- Built with base R, [dplyr](https://CRAN.R-project.org/package=dplyr) and [tidyr](https://CRAN.R-project.org/package=tidyr)
- Course: Data Science Fundamentals, BS Data Science
