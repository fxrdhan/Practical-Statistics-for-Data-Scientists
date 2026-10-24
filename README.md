# Practical-Statistics-for-Data-Scientists

**Code reproduction and theoretical deep-dive of _Practical Statistics for Data Scientists_, 2nd edition**

This repository reproduces, chapter by chapter, the code of **_Practical Statistics for Data Scientists: 50+ Essential Concepts Using R and Python_** by **Peter Bruce, Andrew Bruce and Peter Gedeck** (O'Reilly Media, 2020). Each chapter has its own Jupyter notebook that:

1. **summarizes** every section of the chapter in the author's own words,
2. **explains the theory** behind the concepts (definitions, math, and the reasons a method behaves as it does),
3. **reproduces** the book's Python code, runs it on current library versions and analyzes every output, and
4. adds **extra experiments**, written for this repository, that turn statements the book makes in prose into runnable code (simulations, proofs by numbers, alternative methods).

The code of the book is taken from its official repository, `gedeck/practical-statistics-for-data-scientists`; everything else (summaries, theory, analyses, extra experiments) was written for this repository.

---

## Chapters

| # | Chapter | Status | Notebook |
|---|---|---|---|
| 01 | Exploratory Data Analysis | Done | [Chapter 1 notebook](Chapter_01_Exploratory_Data_Analysis/Chapter_01_Exploratory_Data_Analysis.ipynb) · [summary](Chapter_01_Exploratory_Data_Analysis/README.md) |
| 02 | Data and Sampling Distributions | Planned | |
| 03 | Statistical Experiments and Significance Testing | Planned | |
| 04 | Regression and Prediction | Planned | |
| 05 | Classification | Planned | |
| 06 | Statistical Machine Learning | Planned | |
| 07 | Unsupervised Learning | Planned | |

---

## Chapter-by-chapter overview

### Chapter 1 — Exploratory Data Analysis
Look at the data before modelling it. The chapter covers the types of **structured data** and the rectangular table that holds them, the estimates of **location** (mean, trimmed mean, median, weighted versions) and of **variability** (standard deviation, IQR, MAD), the pictures of a **distribution** (percentiles, boxplot, frequency table, histogram, density plot), the summaries of **binary and categorical** data, **correlation** (matrix, heatmap, ellipse plot, scatterplot) and the tools for **two or more variables** (hexagonal binning, contour plots, contingency tables, violin plots, conditioning with facets).
*Key tools:* `pandas`, `scipy.stats.trim_mean`, `statsmodels.robust`, `wquantiles`, `seaborn`, `Matplotlib`.

---

## How to run

```bash
python -m venv .venv
source .venv/bin/activate            # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

Every notebook starts with a setup cell that prints the versions of the libraries and **downloads the datasets it needs** from the official repository into a folder called `data` next to the notebook (the only use of the network). Each notebook also has an *Open in Colab* badge; in Colab the setup cell installs the one library that Colab does not ship.

## How the notebooks are organized

Every chapter notebook has the same structure, section by section: **Summary**, **Theory**, **Book code** with an **output analysis**, and **Extra experiments** with an analysis of each. A decision guide, a chapter summary with key takeaways, notes on the differences between the book's code and current library versions, and references close the notebook.

Every code cell starts with a label: `# BOOK CODE` marks code from the official repository, reproduced as it is (a change needed to run it is marked in the cell), and `# EXTRA` marks code written for this repository. The first code cell, `# SETUP`, is not part of the book.

## Data and license

The code and the datasets of the book are in the official repository, which is under the **GNU General Public License v3**. This repository does not redistribute the datasets (the folder `data` is ignored by git); the notebooks download them when they run. The book itself is not included and is not quoted.
