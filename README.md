# Replication: "Helping Small Businesses Become More Data-Driven"

**Paper:** Sagit Bar-Gill, Erik Brynjolfsson, Nir Hak (2024). "Helping Small Businesses Become More Data-Driven: A Field Experiment on eBay." *Management Science* 70(11): 7345–7372. https://doi.org/10.1287/mnsc.2021.02026

---

## Overview

This repository contains a Python replication of all main tables and figures from the paper, using the sample data provided in the original replication package.

The paper studies the causal impact of eBay's **Seller Hub (SH)** — a data-rich analytics dashboard — on small-to-medium e-retailer (SME) performance. SH was rolled out in 2016 using a staggered randomized design, enabling a generalized difference-in-differences (DiD) identification strategy. The main finding is that SH access increases weekly sales by 3.6% on average (ITT).

---

## Repository Contents

| File | Description |
|---|---|
| `replication.ipynb` | Main replication notebook (Python) |
| `panelCln_noCustID_Sample.csv` | Seller-week panel data (~10% sample, 423,706 obs) |
| `SlrLvlCln_noCustID_Sample.csv` | Seller-level data (same ~10%, 18,422 sellers) |
| `surveySample.csv` | Survey data (~20% sample, 60 respondents) |
| `CatEPIDSample.csv` | Listing-level category data (Appendix A5.7) |
| `bar-gill-et-al-2024-...pdf` | The paper being replicated |

### Note on Data

The full dataset (184,222 sellers) is proprietary eBay data. Researchers can request access by emailing Brad Sanders at bradsanders@ebay.com. This replication uses the ~10% sample data provided in the original replication package.

---

## How to Run

### 1. Install dependencies

```bash
pip install pyfixest pandas numpy matplotlib seaborn statsmodels scipy jupyter
```

### 2. Open the notebook

```bash
jupyter notebook replication.ipynb
```

### 3. Run all cells

Use **Kernel → Restart & Run All** to reproduce all results end-to-end.

---

## What is Replicated

| Item | Section | Description |
|---|---|---|
| Table 1 | §3.3 | SH Adoption and Changes in DDD (logistic + OLS, survey data) |
| Figure 2 | §3.3 | Average Reported DDD Components: Adopters vs. Non-Adopters |
| Figure 3 | §4 | Sales Trends Before/After Ramp-Up (parallel trends visualization) |
| Table 2 | §5.1 | ITT and TOT-IV Estimates of SH Impact on Sales |
| Figure 4 | §5.1 | Event Study: Relative Time Model coefficients |
| Table 3 | §5.2 | SH Impact on Quantity, Price, Feedback, and New Listings |
| Table 4 | §5.2 | Heterogeneous Effects by Product Category Homogeneity |
| Table 5 | §5.3 | Moderating Role of Performance Monitoring |
| Table D.1 | Appendix D | Dynamic Impacts: Relative Time Model for All Outcomes |
| KW Test | §6.1 | Kruskal-Wallis balance test across ramp-up groups |

Appendices are not replicated.

---

## Empirical Design

The paper exploits the **staggered rollout** of SH across 7 ramp-up cohorts (May 12 – August 8, 2016), where sellers were randomly assigned to cohorts based on their hashed eBay user ID modulo 100. This creates a **generalized DiD** setting:

$$\log(Sales_{sw}) = \alpha_s + \beta_w + \delta \cdot SHaccess_{sw} + \varepsilon_{sw}$$

where $\alpha_s$ are seller fixed effects, $\beta_w$ are week fixed effects, and SEs are clustered at the seller level.

The paper also estimates TOT effects using SH access as an instrument for SH adoption (2SLS/IV), and a relative time model to verify parallel pre-trends.

---

## Note on Sample Data Results

Because this replication uses ~10% of panel sellers and ~20% of survey respondents, standard errors are larger and some point estimates differ from the paper. Key qualitative findings are consistent:

- ITT coefficient on sales is positive (paper: 0.035***)
- First-stage coefficient is ~0.29 (paper: 0.295***)
- Homogeneous category interaction is positive (paper: 0.130***)
- Performance monitoring amplifies the SH effect (paper: 0.014***)

---

## Software Environment

- Python 3.10+
- pyfixest 0.40+ (high-dimensional FE regression and IV, mirrors R's `fixest`/`lfe`)
- pandas, numpy, matplotlib, seaborn, statsmodels, scipy

Original analysis was conducted in R using `lfe::felm` for fixed-effects regressions.
