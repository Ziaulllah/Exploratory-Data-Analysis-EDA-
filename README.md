# EDA Complete Guide

A pandas/seaborn exploratory data analysis reference: a broad technique-by-technique
walkthrough plus one full applied case study, with an automated profiling report
included.

## Overview

This repository documents exploratory data analysis (EDA) workflows in Python —
the process of inspecting a dataset, cleaning it, and understanding its structure
and relationships before any modeling happens. It solves the problem of having to
re-derive the same EDA boilerplate (missing-value handling, outlier detection,
distribution and correlation visualization) on every new dataset by collecting it
in one place as runnable, documented notebooks.

It contains two notebooks with different scopes:

- **`EDA.ipynb`** — a broad reference notebook working through dozens of pandas/EDA
  techniques individually (typing, binning, groupby aggregation, mixed-type
  handling, missing-value imputation strategies, datetime formatting, correlation
  analysis) against the IBM HR Attrition and Auto MPG datasets. It is written as a
  technique-by-technique log rather than a single narrative, and its value is the
  breadth of methods demonstrated.
- **`EDA and Visualization.ipynb`** — a focused, end-to-end case study on the
  Titanic dataset: load, clean, detect and remove outliers (IQR method),
  visualize, and conclude with a written findings summary.

A pre-generated `ydata-profiling` HTML report (`output.html`) is also included for
`data.csv`, viewable directly in a browser with no setup.

## Key Features

- Missing-value detection and multiple imputation strategies (mean, median, mode,
  forward-fill, backward-fill), including visual inspection with `missingno`
  (bar chart, heatmap, matrix).
- Duplicate-row detection and removal.
- Outlier detection and removal using the IQR method, with before/after boxplots.
- Categorical binning with `pd.cut` and `pd.qcut` (equal-width vs. quantile-based).
- Distribution visualization (histograms, bar charts) and relationship analysis
  (correlation heatmaps, `sns.pairplot`).
- Automated profiling report generation via `ydata-profiling`.
- A written key-findings summary for the Titanic case study.

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3 |
| Data handling | pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Missing-data visualization | [missingno](https://github.com/ResidentMario/missingno) |
| Automated profiling | [ydata-profiling](https://github.com/ydataai/ydata-profiling) (formerly `pandas-profiling`) |
| Environment | Jupyter Notebook |

No API keys, external services, or databases are used.

## Project Architecture

Both notebooks follow the same general EDA workflow; the diagram below shows the
shared pipeline shape, with the Titanic notebook (`EDA and Visualization.ipynb`)
as the concrete example that runs it end-to-end.

```mermaid
flowchart LR
    A[Raw CSV Dataset] --> B[Data Cleaning<br/>missing values, duplicates, outliers]
    B --> C[Exploratory Statistics<br/>describe, dtypes, groupby]
    C --> D[Visualization<br/>bar charts, histograms, heatmaps]
    D --> E[Written Insights<br/>Key Findings]
    A -.data.csv only.-> F[ydata-profiling]
    F --> G[output.html]
```

`EDA.ipynb` covers the same stages (cleaning, statistics, visualization) but as
independent technique demonstrations rather than one continuous pipeline run.

## Project Structure

```
EDA-Complete-Guide/
├── EDA.ipynb                          # Broad technique-by-technique EDA reference
├── EDA and Visualization.ipynb        # Titanic case study (requires external CSV, see Installation)
├── output.html                        # Pre-generated ydata-profiling report for data.csv
├── data.csv                           # IBM HR Analytics Employee Attrition dataset (1,471 rows, 35 columns)
├── missing_values_data_auto_mpg.csv   # Auto MPG dataset with injected missing values (398 rows, 9 columns)
├── requirements.txt                   # Python dependencies
├── LICENSE                            # MIT
├── Supervised learning.png            # Reference images, not used by either notebook
├── Unsupervised learning.png          #   (see Limitations)
└── Reinforcement learning.png         #
```

## Installation

```bash
git clone https://github.com/Engrziaullah/EDA-Complete-Guide.git
cd EDA-Complete-Guide
pip install -r requirements.txt
```

Requires Python 3.8+. No specific interpreter version is pinned in this
repository.

## Configuration

No environment variables, API keys, or configuration files are required. All
datasets used by `EDA.ipynb` are included in the repository. `EDA and
Visualization.ipynb` requires one additional file — see Usage below.

## Usage

**View the pre-generated profiling report** — open `output.html` directly in a
browser, no setup required.

**Run the notebooks:**

```bash
jupyter notebook
```

- `EDA.ipynb` runs as-is from the repo root (uses `data.csv` and
  `missing_values_data_auto_mpg.csv`, both included).
- `EDA and Visualization.ipynb` requires `Titanic-Dataset.csv`, which is **not**
  included in this repository. Download it from
  [Kaggle's Titanic competition](https://www.kaggle.com/c/titanic/data) and place
  it in the repo root before running.

## How It Works

Each notebook loads a CSV into a pandas DataFrame, then runs it through a
clean → explore → visualize sequence. Missing values are handled with
`fillna`/`dropna` using mean, median, mode, or fill-based strategies depending on
the section; duplicates are checked with `duplicated()`/`drop_duplicates()`;
outliers are flagged and removed using the IQR method (values outside
`Q1 - 1.5×IQR` to `Q3 + 1.5×IQR`); and results are visualized with Seaborn
(count plots, histograms, boxplots, correlation heatmaps). The automated
profiling report is generated separately by running `ydata-profiling`'s
`ProfileReport` against `data.csv` and exporting it to `output.html`.

## Results / Demo

The Titanic case study (`EDA and Visualization.ipynb`) concludes with these
findings, computed directly from the notebook's output:

- **Missing values:** `Age` and `Fare` were imputed with the median; `Cabin` had
  a large proportion missing; the few missing `Embarked` rows were dropped.
- **Duplicates:** none found.
- **Outliers (IQR method):** one `Age` outlier (80 years) removed; `SibSp` and
  `Parch` outliers removed; `Fare` had multiple high-value outliers left in place
  since removing them could distort fare-based insights.
- **Distributions:** most passengers were third class, aged 20–40, embarked from
  Southampton, and did not survive; `Fare` was right-skewed.
- **Correlations:** `Pclass` and `Fare` showed the strongest correlation
  (higher-class passengers paid more); `Pclass` and `Survived` were also notably
  correlated (first-class passengers had higher survival rates).

No equivalent findings summary exists for `EDA.ipynb` — it is a technique
reference rather than a dataset-insight report, so its value is the demonstrated
methodology rather than a set of conclusions.

## Future Improvements

- Add a `requirements.txt` version pin (currently unpinned) once a target
  environment is fixed.
- Consolidate the technique demonstrations in `EDA.ipynb` into a single narrative
  notebook with a findings summary, matching the structure of `EDA and
  Visualization.ipynb`.
- Bundle or auto-download `Titanic-Dataset.csv` (e.g. via the Kaggle API) so `EDA
  and Visualization.ipynb` runs without a manual download step.

## Limitations

- `EDA.ipynb` is an exploratory reference notebook, not a polished tutorial — it
  contains some dead-end cells and scratch content from the original
  learning process.
- `EDA and Visualization.ipynb` cannot run out of the box; it depends on an
  external file not included in this repository (see Installation).
- `output.html` is a static snapshot generated at one point in time — it does not
  update automatically if `data.csv` changes.
- `Supervised learning.png`, `Unsupervised learning.png`, and
  `Reinforcement learning.png` are general machine-learning reference images
  unrelated to the EDA content in this repository; they are not used by either
  notebook.

## Contributing

This is a personal reference/portfolio project and is not actively seeking
contributions. Issues and suggestions are still welcome via GitHub Issues.

## License

MIT — see [LICENSE](LICENSE).

## Author

**Zia Ullah** — [LinkedIn](https://www.linkedin.com/in/engr-ziaullah-7672ab260)
