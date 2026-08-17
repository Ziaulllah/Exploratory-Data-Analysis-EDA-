# Exploratory Data Analysis (EDA)

Jupyter notebooks covering exploratory data analysis in Python: data inspection, missing-value handling, duplicate detection, outlier handling, and visualization (distributions, correlation, categorical breakdowns). The repo contains two separate notebooks plus a pre-generated automated profiling report.

## Contents

| File | Description |
|---|---|
| `EDA.ipynb` | A broad, tutorial-style walkthrough of EDA techniques in pandas: numerical vs. categorical typing, binning (`qcut`/`cut`), groupby aggregates, duplicate handling, mixed-type columns, missing-value visualization with `missingno`, missing-value imputation strategies (mean/median/mode, forward/backward fill), datetime formatting, correlation matrices, pairplots, boxplots, and automated profiling with `ydata-profiling` (formerly `pandas-profiling`). Uses `data.csv` and `missing_values_data_auto_mpg.csv`. |
| `EDA and Visualization.ipynb` | A focused, task-structured EDA and visualization exercise on the Titanic dataset: load data, handle missing values (median imputation for `Age`/`Fare`), check duplicates, detect/remove outliers with the IQR method, and visualize with bar charts, histograms, and a correlation heatmap. Ends with a written "Key Findings" section (see below). **Note:** this notebook reads `Titanic-Dataset.csv`, which is not included in this repository — see Datasets below. |
| `output.html` | Pre-generated `ydata-profiling` HTML report for `data.csv`. Open it directly in a browser to view the full automated profile (variable summaries, correlations, missing-value overview) without running any code. |
| `data.csv` | IBM HR Analytics Employee Attrition dataset — 1,471 rows, 35 columns (age, department, job role, income, attrition, satisfaction scores, etc.). Used throughout `EDA.ipynb`. |
| `missing_values_data_auto_mpg.csv` | Auto MPG dataset — 398 rows, 9 columns, with a small number of missing/placeholder (`?`) values in `horsepower`. Used in `EDA.ipynb` to demonstrate missing-value detection and imputation. |
| `Supervised learning.png`, `Unsupervised learning.png`, `Reinforcement learning.png` | General machine-learning-type reference images. Not referenced by either notebook or by the README — kept as-is but not part of the analysis. |
| `first_demo_class.py`, `first_demo_class_02.py` | Empty placeholder files, not used by the analysis. |

## Datasets

- **`data.csv`** (included) — IBM HR Analytics Employee Attrition & Performance dataset.
- **`missing_values_data_auto_mpg.csv`** (included) — Auto MPG dataset, adapted to include missing values for teaching purposes.
- **`Titanic-Dataset.csv`** (**not included**) — required by `EDA and Visualization.ipynb`. This is the standard Kaggle Titanic dataset (`train.csv`/`Titanic-Dataset.csv`, columns include `Survived`, `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `Cabin`, `Embarked`). To run that notebook, download the dataset (e.g. from [Kaggle's Titanic competition](https://www.kaggle.com/c/titanic/data)) and place it in the repo root as `Titanic-Dataset.csv`.

## Tech stack

Python, pandas, NumPy, Matplotlib, Seaborn, [missingno](https://github.com/ResidentMario/missingno), [ydata-profiling](https://github.com/ydataai/ydata-profiling) (formerly `pandas-profiling`), Jupyter.

## Key findings (Titanic analysis, from `EDA and Visualization.ipynb`)

**Missing values**
- `Age` and `Fare` had missing values, handled with median imputation.
- `Cabin` had a large proportion of missing values.
- `Embarked` had a few missing values, which were removed.

**Duplicates**
- No duplicate rows were found.

**Outliers (IQR method)**
- `Age` had one outlier (80 years old), removed.
- `SibSp` had outliers at 3, removed.
- `Parch` had an outlier at 4, removed.
- `Fare` had multiple high-value outliers (e.g. 512.33); removing them could affect downstream insights.

**Distributions and correlations**
- More passengers did not survive than did.
- Most passengers were third class (`Pclass`).
- More males than females were aboard.
- Most passengers embarked from Southampton (`S`).
- Most passengers were between 20–40 years old.
- Most passengers had zero or one family member aboard (`SibSp`/`Parch`).
- `Fare` was right-skewed (a small number of very high fares).
- Strongest positive correlation: `Pclass` and `Fare` (higher-class passengers paid more).
- `Pclass` and `Survived` were notably correlated (first-class passengers had higher survival rates).

No equivalent "key findings" write-up exists for `EDA.ipynb`, which is written as a technique-by-technique reference rather than a dataset-insight report — its value is the demonstrated methodology (see Contents table above).

## Setup

```bash
git clone https://github.com/Engrziaullah/Exploratory-Data-Analysis-EDA-.git
cd Exploratory-Data-Analysis-EDA-
pip install pandas numpy matplotlib seaborn missingno ydata-profiling jupyter
```

## Usage

- **View the automated profiling report:** open `output.html` directly in a browser — no setup required.
- **Run the notebooks:**
  ```bash
  jupyter notebook
  ```
  Then open `EDA.ipynb` or `EDA and Visualization.ipynb`. `EDA.ipynb` and `missing_values_data_auto_mpg.csv`/`data.csv` will run as-is from the repo root. `EDA and Visualization.ipynb` requires `Titanic-Dataset.csv` to be added first (see Datasets above).
