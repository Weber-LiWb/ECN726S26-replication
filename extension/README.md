# Extension Analysis: Specification Curve Analysis of Bar-Gill et al. (2024)

## How to Run

1. Ensure dependencies are installed (from the parent directory):
   ```bash
   pip install -r ../requirements.txt
   ```

2. Open and run the notebook:
   ```bash
   jupyter notebook extension.ipynb
   ```
   Then: **Kernel → Restart & Run All**

   The notebook is designed for single-click execution. All results are exported
   automatically to the `output/` directory.

## Output Files

| File | Description |
|------|-------------|
| `output/all_specs.csv` | Full specification curve results (~160 specifications) |
| `output/meta_regression.csv` | Meta-regression coefficients (γ) |
| `output/summary_stats.csv` | Summary statistics for key variables |
| `output/quantity_specs.csv` | Quantity outcome supplementary results (7 specs) |
| `output/spec_curve.png` | Main specification curve figure |
| `output/c_sensitivity.png` | Sensitivity of δ̂ to choice of c in log(GMV + c) |

## Data

The analysis reads data from the parent directory:
- `../panelCln_noCustID_Sample.csv` — Seller-week panel (~10% sample, 423,706 obs)
- `../SlrLvlCln_noCustID_Sample.csv` — Seller-level data (18,422 sellers)

These are ~10% samples of the full dataset. Point estimates may differ from the
paper but qualitative patterns (which modeling choices matter most) are preserved.

