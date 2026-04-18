# ECN 729 Term Project — Replication + Extension

Python replication and specification-curve extension of:

> Bar-Gill, S., Brynjolfsson, E., & Hak, N. (2024). Helping Small Businesses
> Become More Data-Driven: A Field Experiment on eBay. *Management Science*,
> 70(11), 7345–7372. https://doi.org/10.1287/mnsc.2021.02026

The project has **two deliverables**, each living in its own subdirectory:

| Part | Directory | Deliverable |
|---|---|---|
| 1. Replication of the paper's main tables and figures | [`replication/`](replication/) | `replication/replication.ipynb` → `replication/replication.pdf` |
| 2. Specification-curve extension + AEA-style term paper | [`extension/`](extension/) | `extension/extension.ipynb` + `extension/paper/main.tex` → `extension/Li_ECN729_TermPaper.pdf.pdf` |

Each subdirectory has its own README with detailed instructions:
- [`replication/README.md`](replication/README.md) — which tables/figures are replicated, how to run
- [`extension/README.md`](extension/README.md) — specification curve design, output files

---

## Directory Layout

```
ECN726S26-replication/
├── README.md                         ← (this file)
├── LICENSE
├── requirements.txt                  ← Python dependencies for both parts
│
├── panelCln_noCustID_Sample.csv      ← Seller-week panel (~10% sample, 423,706 obs)
├── SlrLvlCln_noCustID_Sample.csv     ← Seller-level data  (~10% sample, 18,422 sellers)
├── surveySample.csv                  ← Survey data        (~20% sample, 60 respondents)
├── CatEPIDSample.csv                 ← Listing-level category data (Appendix A5.7)
├── bar-gill-et-al-2024-...pdf        ← The original paper being replicated
│
├── replication/                      ← Part 1: reproducing the original results
│   ├── README.md
│   ├── replication.ipynb             ← Main notebook (Python, ~760 lines, 16 cells)
│   ├── replication.pdf               ← Exported notebook
│   ├── Figure2_DDD_Components.png
│   ├── Figure3_SalesTrends.png
│   └── Figure4_EventStudy.png
│
└── extension/                        ← Part 2: specification-curve analysis
    ├── README.md
    ├── HANDOVER.md                   ← Design notes + references for the term paper
    ├── extension.ipynb               ← Runs the 160-specification curve
    ├── Li_ECN729_TermPaper.pdf.pdf   ← Compiled term paper (final PDF)
    │
    ├── output/                       ← Figures and tables consumed by the paper
    │   ├── spec_curve.png            ← Figure 1 in the paper
    │   ├── c_sensitivity.png         ← Figure 2 in the paper
    │   ├── meta_regression.csv       ← Underlying data for Table 3
    │   ├── all_specs.csv             ← All 160 specifications
    │   ├── quantity_specs.csv        ← Supplementary (Quantity outcome)
    │   └── summary_stats.csv         ← Summary stats
    │
    └── paper/                        ← LaTeX source for the term paper
        ├── main.tex                  ← AEA-style article (double-spaced, 14 pp.)
        ├── main.pdf                  ← Compiled output
        ├── main.aux / .log / .out    ← LaTeX build artifacts
```

---

## How to Run

### 1. Install Python dependencies (once)

```bash
pip install -r requirements.txt
```

Python 3.10+ is required. A virtual environment at `.venv/` is already configured.
Core stack: `pyfixest` (high-dimensional FE / IV, mirrors R's `fixest`), `pandas`,
`numpy`, `statsmodels`, `scipy`, `matplotlib`, `seaborn`.

### 2. Replicate the paper's main results

```bash
jupyter notebook replication/replication.ipynb
```

Use **Kernel → Restart & Run All**. Reproduces Tables 1–5, D.1 and Figures 2–4.
See [`replication/README.md`](replication/README.md) for the full mapping.

### 3. Run the specification-curve extension

```bash
jupyter notebook extension/extension.ipynb
```

Use **Kernel → Restart & Run All**. Fits all 160 specifications, writes figures
and CSVs to `extension/output/`.

---

## Data

The four CSVs at the repo root are **~10% samples** (panel, seller-level,
category) and **~20% sample** (survey) released with the original replication
package. The full dataset (184,222 sellers) is proprietary eBay data; researchers
can request access via Brad Sanders (`bradsanders@ebay.com`).

Because the sample is partial, standard errors are larger and point estimates
differ slightly from the published paper. Qualitative findings are preserved.


