# EDA and Preprocessing Complete Guide

A pandas/scikit-learn reference covering the two stages that come before
modeling: exploratory data analysis and data preprocessing — cleaning,
categorical encoding, scaling, and normalization — demonstrated across four
real datasets.

## Overview

This repository documents the two pipeline stages that typically precede model
training: understanding a dataset (EDA) and preparing it for a model
(preprocessing). It was formed by merging two previously separate reference
repositories — `EDA-Complete-Guide` and `Data-preprocessing-` — into one
coherent guide, since both covered adjacent stages of the same workflow, used
overlapping techniques, and in one case the same dataset.

It contains five notebooks:

- **`EDA.ipynb`** — a broad reference notebook working through pandas EDA
  techniques individually (typing, binning, groupby aggregation, mixed-type
  handling, missing-value imputation, datetime formatting, correlation
  analysis) against the IBM HR Attrition and Auto MPG datasets.
- **`EDA and Visualization.ipynb`** — a focused, end-to-end case study on the
  Titanic dataset: load, clean, detect and remove outliers (IQR method),
  visualize, and conclude with a written findings summary.
- **`DataCleaning 6.1.ipynb`** — encoding-safe CSV loading, fuzzy-matching
  inconsistent category labels, outlier/skew visualization, min-max scaling,
  and Box-Cox normalization, against a dataset of university faculty records.
- **`Label Encoding 6.2.ipynb`** — ordinal encoding, binary mapping, one-hot
  encoding, and frequency encoding of categorical columns, against the IBM HR
  Attrition dataset.
- **`module_01.ipynb`** — conceptual/theory notes on AI and machine learning;
  no executable preprocessing code.

A pre-generated `ydata-profiling` HTML report (`output.html`) is also included
for `data.csv`, viewable directly in a browser with no setup.

## Key Features

**Exploratory data analysis**
- Missing-value detection and multiple imputation strategies (mean, median,
  mode, forward-fill, backward-fill), with visual inspection via `missingno`.
- Duplicate-row detection and removal.
- Outlier detection and removal using the IQR method, with before/after
  boxplots.
- Categorical binning with `pd.cut` and `pd.qcut`.
- Distribution and relationship visualization (histograms, bar charts,
  correlation heatmaps, `sns.pairplot`).
- Automated profiling report generation via `ydata-profiling`.

**Data preprocessing**
- Encoding-safe CSV loading with a UTF-8 → Latin-1 fallback.
- Fuzzy string matching (`fuzzywuzzy`) to consolidate inconsistent category
  labels (e.g. variant spellings of the same country name).
- Min-max scaling (`mlxtend.preprocessing.minmax_scaling`) and Box-Cox
  normalization (`scipy.stats.boxcox`) for skewed distributions.
- Ordinal encoding (`sklearn.preprocessing.OrdinalEncoder`), binary mapping
  (`Series.map`), one-hot encoding (`pandas.get_dummies`), and frequency
  encoding (`value_counts`).

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3 |
| Data handling | pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Missing-data visualization | [missingno](https://github.com/ResidentMario/missingno) |
| Automated profiling | [ydata-profiling](https://github.com/ydataai/ydata-profiling) |
| Statistical transforms | SciPy (`stats.boxcox`) |
| Fuzzy string matching | [fuzzywuzzy](https://github.com/seatgeek/fuzzywuzzy) (+ `python-Levenshtein` for speed) |
| Scaling utilities | [mlxtend](https://github.com/rasbt/mlxtend) |
| Encoding | scikit-learn (`OrdinalEncoder`), pandas (`get_dummies`) |
| Environment | Jupyter Notebook |

No API keys, external services, or databases are used.

## Project Architecture

```mermaid
flowchart TD
    subgraph EDA["Exploratory Data Analysis"]
        A[Raw CSV Dataset] --> B[Cleaning<br/>missing values, duplicates, outliers]
        B --> C[Visualization<br/>distributions, correlations]
        C --> D[Written Insights]
    end
    subgraph PREP["Preprocessing"]
        E[Raw / Inconsistent Data] --> F[Fuzzy-Match Categories]
        F --> G[Scale / Normalize<br/>min-max, Box-Cox]
        G --> H[Encode Categoricals<br/>ordinal, binary, one-hot, frequency]
    end
    A -.data.csv.-> I[ydata-profiling]
    I --> J[output.html]
    D --> H
    H --> K[Ready for Modeling]
```

The EDA notebooks explore and clean a dataset; the preprocessing notebooks pick
up from there and transform categorical/skewed columns into a model-ready
form. `EDA.ipynb` and `Label Encoding 6.2.ipynb` both use `data.csv` (IBM HR
Attrition) — the dataset is included once in this repository and used by both
stages.

## Project Structure

```
EDA-and-Preprocessing-Complete-Guide/
├── EDA.ipynb                          # Broad EDA technique reference (IBM HR + Auto MPG)
├── EDA and Visualization.ipynb        # Titanic case study (requires external CSV, see Usage)
├── DataCleaning 6.1.ipynb             # Fuzzy matching, scaling, Box-Cox normalization
├── Label Encoding 6.2.ipynb           # Ordinal / binary / one-hot / frequency encoding
├── module_01.ipynb                    # AI/ML theory notes (no executable code)
├── output.html                        # Pre-generated ydata-profiling report for data.csv
├── data.csv                           # IBM HR Analytics Employee Attrition (1,471 rows, 35 cols)
├── missing_values_data_auto_mpg.csv   # Auto MPG dataset with injected missing values
├── PIC.csv                            # University faculty records (used by DataCleaning 6.1)
├── requirements.txt                   # Python dependencies
├── LICENSE                            # MIT
├── binary.png, ordinal.png,           # Reference diagrams embedded in the
│   negative.png, positive.png,        #   preprocessing notebooks
│   no_skew.png, skewed.jpeg,          #
│   image.png                          #
└── Supervised/Unsupervised/           # General ML-type reference images,
    Reinforcement learning.png         #   unused by any notebook (see Limitations)
```

## Installation

```bash
git clone https://github.com/Engrziaullah/EDA-and-Preprocessing-Complete-Guide.git
cd EDA-and-Preprocessing-Complete-Guide
pip install -r requirements.txt
```

Requires Python 3.8+. No specific interpreter version is pinned.

## Configuration

No environment variables, API keys, or configuration files are required. Most
datasets are included in the repository — see Usage for the one exception.

## Usage

**View the pre-generated profiling report** — open `output.html` directly in a
browser, no setup required.

**Run the notebooks:**

```bash
jupyter notebook
```

- `EDA.ipynb`, `Label Encoding 6.2.ipynb`, and `DataCleaning 6.1.ipynb` all run
  as-is from the repo root — each reads a CSV that's already included
  (`data.csv`, `PIC.csv`).
- `EDA and Visualization.ipynb` requires `Titanic-Dataset.csv`, which is
  **not** included. Download it from
  [Kaggle's Titanic competition](https://www.kaggle.com/c/titanic/data) and
  place it in the repo root before running.
- `module_01.ipynb` is read-only reference material; there is nothing to run.

## How It Works

**EDA:** each notebook loads a CSV into a pandas DataFrame, then runs it
through a clean → explore → visualize sequence. Missing values are handled
with `fillna`/`dropna`; outliers are flagged and removed using the IQR method
(`Q1 - 1.5×IQR` to `Q3 + 1.5×IQR`); results are visualized with Seaborn.

**Preprocessing:** `DataCleaning 6.1.ipynb` loads data with an explicit
encoding fallback, uses `fuzzywuzzy.process` to merge near-duplicate category
strings, then demonstrates two normalization approaches — min-max scaling
(linear rescale to `[0, 1]`) and Box-Cox (a power transform that reduces
skew). `Label Encoding 6.2.ipynb` applies four different categorical-encoding
strategies to different columns of the same dataset, chosen to match each
column's structure: ordinal for ranked categories (`Education`), binary
mapping for two-valued columns (`Attrition`), one-hot for unordered categories
(`BusinessTravel`), and frequency encoding as a compact alternative
(`Department`).

## Results / Demo

The Titanic case study (`EDA and Visualization.ipynb`) concludes with these
findings, computed directly from the notebook's output:

- **Missing values:** `Age` and `Fare` were imputed with the median; `Cabin`
  had a large proportion missing; the few missing `Embarked` rows were
  dropped.
- **Outliers (IQR method):** one `Age` outlier (80 years) removed; `SibSp` and
  `Parch` outliers removed; `Fare`'s high-value outliers were left in place
  since removing them could distort fare-based insights.
- **Distributions:** most passengers were third class, aged 20–40, embarked
  from Southampton, and did not survive; `Fare` was right-skewed.
- **Correlations:** `Pclass` and `Fare` showed the strongest correlation;
  `Pclass` and `Survived` were also notably correlated.

The preprocessing notebooks are technique demonstrations rather than
insight-generating analyses, so there is no equivalent findings summary for
`DataCleaning 6.1.ipynb` or `Label Encoding 6.2.ipynb` — their value is the
demonstrated methodology.

## Future Improvements

- Add version pins to `requirements.txt` once a target environment is fixed.
- Consolidate `EDA.ipynb`'s individual technique demonstrations into a single
  narrative notebook with a findings summary, matching the structure of `EDA
  and Visualization.ipynb`.
- Execute the commented-out `LabelEncoder`/`OneHotEncoder`/target-encoding/
  feature-hashing sketches in `Label Encoding 6.2.ipynb` against real data
  instead of leaving them as placeholders.
- Bundle or auto-download `Titanic-Dataset.csv` (e.g. via the Kaggle API) so
  `EDA and Visualization.ipynb` runs without a manual download step.

## Limitations

- `EDA.ipynb` is an exploratory reference notebook, not a polished tutorial —
  it contains some dead-end cells and scratch content from the original
  learning process.
- `EDA and Visualization.ipynb` cannot run out of the box; it depends on an
  external file not included in this repository (see Usage).
- `output.html` is a static snapshot generated at one point in time — it does
  not update automatically if `data.csv` changes.
- `module_01.ipynb` contains no executable code; it's markdown-only
  theory notes, included for completeness rather than as a working notebook.
- `Label Encoding 6.2.ipynb` includes commented-out sketches for additional
  encoders (target encoding, feature hashing) that are not executed against
  real data in this notebook.
- `Supervised learning.png`, `Unsupervised learning.png`, and
  `Reinforcement learning.png` are general machine-learning reference images
  unrelated to this repository's EDA/preprocessing content; they are not used
  by any notebook.
- This repository was assembled by merging two previously separate repos.
  Their individual commit histories were not carried over — this repository's
  git history starts from the merge.

## Contributing

This is a personal reference/portfolio project and is not actively seeking
contributions. Issues and suggestions are still welcome via GitHub Issues.

## License

MIT — see [LICENSE](LICENSE).

## Author

**Zia Ullah** — [LinkedIn](https://www.linkedin.com/in/engr-ziaullah-7672ab260)
