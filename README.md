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
| 02 | Data and Sampling Distributions | Done | [Chapter 2 notebook](Chapter_02_Data_and_Sampling_Distributions/Chapter_02_Data_and_Sampling_Distributions.ipynb) · [summary](Chapter_02_Data_and_Sampling_Distributions/README.md) |
| 03 | Statistical Experiments and Significance Testing | Done | [Chapter 3 notebook](Chapter_03_Statistical_Experiments_and_Significance_Testing/Chapter_03_Statistical_Experiments_and_Significance_Testing.ipynb) · [summary](Chapter_03_Statistical_Experiments_and_Significance_Testing/README.md) |
| 04 | Regression and Prediction | Done | [Chapter 4 notebook](Chapter_04_Regression_and_Prediction/Chapter_04_Regression_and_Prediction.ipynb) · [summary](Chapter_04_Regression_and_Prediction/README.md) |
| 05 | Classification | Done | [Chapter 5 notebook](Chapter_05_Classification/Chapter_05_Classification.ipynb) · [summary](Chapter_05_Classification/README.md) |
| 06 | Statistical Machine Learning | Planned | |
| 07 | Unsupervised Learning | Planned | |

---

## Chapter-by-chapter overview

### Chapter 1 — Exploratory Data Analysis
Look at the data before modelling it. The chapter covers the types of **structured data** and the rectangular table that holds them, the estimates of **location** (mean, trimmed mean, median, weighted versions) and of **variability** (standard deviation, IQR, MAD), the pictures of a **distribution** (percentiles, boxplot, frequency table, histogram, density plot), the summaries of **binary and categorical** data, **correlation** (matrix, heatmap, ellipse plot, scatterplot) and the tools for **two or more variables** (hexagonal binning, contour plots, contingency tables, violin plots, conditioning with facets).
*Key tools:* `pandas`, `scipy.stats.trim_mean`, `statsmodels.robust`, `wquantiles`, `seaborn`, `Matplotlib`.

### Chapter 2 — Data and Sampling Distributions
How far can a sample be trusted? The chapter covers **random sampling and sample bias**, **selection bias** and regression to the mean, the **sampling distribution of a statistic** (central limit theorem, standard error), the **bootstrap**, **confidence intervals**, and the distributions used as models: the **normal** distribution with QQ-plots, **long-tailed** distributions, Student's **t**, the **binomial**, the **chi-square**, the **F**, and the **Poisson** family with the exponential and the Weibull distribution.
*Key tools:* `scipy.stats`, `sklearn.utils.resample`, `scipy.stats.bootstrap`, `pandas`, `Matplotlib`.

### Chapter 3 — Statistical Experiments and Significance Testing
Is a difference real, or could chance have produced it? The chapter covers the **A/B test** and random assignment, **hypothesis tests**, **resampling** with the permutation test, **statistical significance and p-values** with the two types of error, the **t-test**, **multiple testing**, **degrees of freedom**, **ANOVA** and the F-statistic, the **chi-square test** and Fisher's exact test, the **multi-arm bandit** algorithm, and **power and sample size**.
*Key tools:* `scipy.stats`, `statsmodels` (ANOVA tables, power analysis, multiple-testing corrections), `pandas`, `Matplotlib`.

### Chapter 4 — Regression and Prediction
Modelling an outcome from predictors. The chapter covers **simple** and **multiple linear regression** (least squares, the King County house prices, assessing a model, cross-validation, stepwise selection, weighted regression), **prediction** with confidence and prediction intervals and the dangers of extrapolation, **factor variables** (dummy variables, many levels), the **interpretation** of the coefficients (correlated predictors, confounding, interactions), **regression diagnostics** (outliers, influential values, heteroskedasticity, partial residual plots), **polynomial and spline regression** with generalized additive models, and the lasso as additional material of the official repository.
*Key tools:* `scikit-learn`, `statsmodels`, `pygam`, `dmba`, `seaborn`, `Matplotlib`.

### Chapter 5 — Classification
Predicting a category through the probability of each class. The chapter covers **naive Bayes**, **discriminant analysis**, **logistic regression** (the logit, the GLM, odds ratios, assessing the model), the **evaluation** of classifiers (confusion matrix, precision, recall, specificity, ROC curve, AUC, lift) and **strategies for imbalanced data** (undersampling, oversampling and weighting, SMOTE and ADASYN, cost-based classification, comparing the decision boundaries of different classifiers).
*Key tools:* `scikit-learn`, `statsmodels`, `imbalanced-learn`, `pygam`, `dmba`.

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
