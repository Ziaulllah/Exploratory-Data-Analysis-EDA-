# 🧹 EDA and Preprocessing Complete Guide

A structured, hands-on walkthrough of exploratory data analysis and data
preprocessing — from raw, messy CSVs to model-ready features — built as a
personal study reference and portfolio artifact.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![Status](https://img.shields.io/badge/status-active%20learning%20log-informational)

## 📖 Table of Contents

- [🔍 Overview](#-overview)
- [📚 Notebooks](#-notebooks)
- [🛠️ Tech Stack](#️-tech-stack)
- [⚙️ Getting Started](#️-getting-started)
- [🔗 Related Work](#-related-work)
- [📄 Scope & License](#-scope--license)

## 🔍 Overview

This repository is a study log covering the two stages that come before model
training: exploratory data analysis (understanding a dataset — its
distributions, missing values, outliers, and relationships) and preprocessing
(cleaning inconsistent values, scaling, normalizing, and encoding
categoricals). It's a learning collection rather than a packaged library —
expect notebook-style code (exploratory cells, inline notes) rather than a
production module.

It was formed by merging two previously separate repositories —
`EDA-Complete-Guide` and `Data-preprocessing-` — into one guide, since both
covered adjacent stages of the same workflow and, in one case, the exact same
dataset. Everything is organized into `notebooks/`, `data/`, `assets/`, and
`reports/` so each notebook's relative file references stay short and
consistent.

It's the data-analysis counterpart to
[`NLP-Complete-Guide`](https://github.com/Engrziaullah/NLP-Complete-Guide) and
[`Deep-Learning-Complete-Guide`](https://github.com/Engrziaullah/Deep-Learning-Complete-Guide),
companion repos in the same "complete guide" series.

## 📚 Notebooks

5 Jupyter notebooks, organized by topic:

**Exploratory Data Analysis**

| Notebook | Covers |
|---|---|
| [`eda-techniques-reference.ipynb`](<notebooks/eda-techniques-reference.ipynb>) | Broad technique reference: typing, binning (`qcut`/`cut`), groupby aggregation, mixed-type handling, missing-value imputation, datetime formatting, correlation analysis — on the IBM HR Attrition and Auto MPG datasets |
| [`titanic-eda-and-visualization.ipynb`](<notebooks/titanic-eda-and-visualization.ipynb>) | Focused case study: load, clean, detect/remove outliers (IQR method), visualize, and conclude with a written key-findings summary |

**Data Preprocessing**

| Notebook | Covers |
|---|---|
| [`data-cleaning-and-normalization.ipynb`](<notebooks/data-cleaning-and-normalization.ipynb>) | Encoding-safe CSV loading, fuzzy-matching inconsistent category labels, min-max scaling, Box-Cox normalization |
| [`categorical-encoding.ipynb`](<notebooks/categorical-encoding.ipynb>) | Ordinal encoding, binary mapping, one-hot encoding, and frequency encoding |

**Reference**

| Notebook | Covers |
|---|---|
| [`ai-ml-theory-notes.ipynb`](<notebooks/ai-ml-theory-notes.ipynb>) | Conceptual AI/ML notes — markdown only, no executable code |

A pre-generated `ydata-profiling` HTML report is included at
[`reports/data-profile-report.html`](<reports/data-profile-report.html>) for
`data/data.csv` — open it directly in a browser, no setup required.

> **Note:** `eda-techniques-reference.ipynb` and `categorical-encoding.ipynb`
> both use `data/data.csv` (IBM HR Attrition) — one dataset, shared across the
> EDA and preprocessing stages. `titanic-eda-and-visualization.ipynb` expects
> `data/Titanic-Dataset.csv`, which is **not** included (see Getting Started).
> `assets/skewed.jpeg` isn't referenced by any notebook — kept for reference,
> not currently used. `ai-ml-theory-notes.ipynb` has no runnable cells by
> design; it's markdown notes, not a demo.

## 🛠️ Tech Stack

Reconstructed from the actual imports used across the notebooks:

| Category | Tools |
|---|---|
| Data handling | pandas, NumPy |
| Visualization | Matplotlib, seaborn |
| Missing-data visualization | [missingno](https://github.com/ResidentMario/missingno) |
| Automated profiling | [ydata-profiling](https://github.com/ydataai/ydata-profiling) |
| Statistical transforms | SciPy (`stats.boxcox`) |
| Fuzzy string matching | [fuzzywuzzy](https://github.com/seatgeek/fuzzywuzzy) (+ `python-Levenshtein`) |
| Scaling utilities | [mlxtend](https://github.com/rasbt/mlxtend) |
| Encoding | scikit-learn (`OrdinalEncoder`), pandas (`get_dummies`) |

## ⚙️ Getting Started

```bash
git clone https://github.com/Engrziaullah/EDA-and-Preprocessing-Complete-Guide.git
cd EDA-and-Preprocessing-Complete-Guide
pip install -r requirements.txt
jupyter notebook
```

Then open whichever notebook covers the topic you're interested in, from the
`notebooks/` folder. Launch Jupyter from the repository root so each
notebook's relative paths (`../data/...`, `../assets/...`) resolve correctly.

`eda-techniques-reference.ipynb`, `categorical-encoding.ipynb`, and
`data-cleaning-and-normalization.ipynb` all run as-is — their datasets are
already in `data/`. `titanic-eda-and-visualization.ipynb` needs one more file:
download the Titanic dataset from
[Kaggle's Titanic competition](https://www.kaggle.com/c/titanic/data) and
save it as `data/Titanic-Dataset.csv` first.

## 🔗 Related Work

- [`NLP-Complete-Guide`](https://github.com/Engrziaullah/NLP-Complete-Guide) — the NLP counterpart to this repo, same series.
- [`Deep-Learning-Complete-Guide`](https://github.com/Engrziaullah/Deep-Learning-Complete-Guide) — the deep-learning counterpart, same series.

## 📄 Scope & License

A personal reference collection, not a tutorial series with guaranteed
correctness or a maintained API. Content ranges from short technique
demonstrations to a full worked case study (Titanic) — treat it as study
material rather than a dependency to build on. MIT-licensed — see
[LICENSE](LICENSE). Shared for educational and portfolio purposes.
