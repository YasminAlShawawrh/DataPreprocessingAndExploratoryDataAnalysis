# Data Preprocessing & Exploratory Data Analysis (EDA)

A Python-based data preprocessing and EDA pipeline applied to a synthetic customer churn dataset. The project covers the full preprocessing workflow — from raw data inspection to cleaned, scaled outputs ready for machine learning — along with a rich set of visualizations for churn analysis.


---

## Table of contents

- [Project overview](#project-overview)
- [Dataset](#dataset)
- [Pipeline steps](#pipeline-steps)
- [Output files](#output-files)
- [Technologies used](#technologies-used)
- [How to run](#how-to-run)

---

## Project overview

The goal of this project is to prepare a real-world-style customer dataset for machine learning by applying systematic preprocessing steps and generating visual insights about customer churn behavior.

---

## Dataset

- **File:** `customer_data.csv`
- **Target column:** `ChurnStatus` (binary — churn or not)
- **ID column:** `CustomerID`
- **Features include:** Gender, ProductType, SupportCalls, and other numeric/categorical attributes

---

## Pipeline steps

### 1 — Data loading & initial inspection
Loads the CSV and performs an initial exploration using `.head()`, `.info()`, and `.describe()` to understand structure, data types, and basic statistics.

### 2 — Handling missing data
- Counts and reports missing values (count + percentage)
- Fills numeric columns with the **median**
- Fills categorical columns with the **mode**
- Saves the cleaned dataset to `customer_data_cleaned.csv`

### 3 — Outlier detection & smoothing
- Detects outliers using **Z-score** (threshold: |z| > 3)
- Applies **quantile-based binning** (10 bins) to smooth outliers by replacing values with their bin median
- Reports standard deviation before and after smoothing per feature

### 4 — Feature scaling
Two scaling methods are applied and saved separately:

| Method | Description | Output file |
|---|---|---|
| Standardization | Zero mean, unit variance (z-score) | `customer_data_standardized.csv` |
| Min–Max normalization | Scales values to [0, 1] range | `customer_data_minmax.csv` |

### 5 — Exploratory data analysis (EDA)
All plots are saved automatically to the `assignment_outputs/figures/` directory.

**Univariate analysis:**
- Histograms for all numeric features
- Box plots for all numeric features
- Bar plots for all categorical features

**Bivariate analysis:**
- Scatter plots: each numeric feature vs `ChurnStatus`
- Bar plots: churn rate by each categorical feature

**Correlation analysis:**
- Heatmap of the full numeric correlation matrix
- Correlation ranking of all features against `ChurnStatus`

---

## Output files

```
assignment_outputs/
├── customer_data_cleaned.csv         # After missing value imputation
├── customer_data_post_outliers.csv   # After outlier smoothing
├── customer_data_standardized.csv    # Z-score scaled
├── customer_data_minmax.csv          # Min-max scaled
└── figures/
    ├── hist_*.png                    # Histograms
    ├── box_*.png                     # Box plots
    ├── bar_*.png                     # Categorical bar plots
    ├── scatter_*vsChurnStatus.png    # Scatter plots vs target
    ├── churnrate_by_*.png            # Churn rate by category
    └── correlation_matrix.png        # Correlation heatmap
```

---

## Technologies used

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, imputation |
| `numpy` | Numeric operations, Z-score calculation |
| `matplotlib` | All visualizations |
| `os` | Output directory management |

---

## How to run

1. Clone the repository:
```bash
git clone https://github.com/YasminAlShawawrh/DataPreprocessingAndExploratoryDataAnalysis.git
cd DataPreprocessingAndExploratoryDataAnalysis
```

2. Install dependencies:
```bash
pip install pandas numpy matplotlib
```

3. Update the dataset path in the script:
```python
DATA_PATH = "path/to/your/customer_data.csv"
```

4. Run the script:
```bash
python main.py
```

All cleaned CSVs and figures will be saved to the `assignment_outputs/` folder.
