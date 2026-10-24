# Chapter 5 — Classification

**Notebook:** [`Chapter_05_Classification.ipynb`](Chapter_05_Classification.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_05_Classification/Chapter_05_Classification.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 5 predicts a category, usually through the probability of each class. It covers:

- **naive Bayes**: why exact Bayesian classification is impractical, the naive solution, numeric predictors;
- **discriminant analysis**: the covariance matrix, Fisher's linear discriminant;
- **logistic regression**: the logit and the logistic response function, the GLM, predicted values, odds ratios, assessing the model;
- **evaluating classification models**: the confusion matrix, the rare class problem, precision, recall and specificity, the ROC curve, the AUC, lift;
- **strategies for imbalanced data**: undersampling, oversampling and weighting, data generation (SMOTE, ADASYN), cost-based classification, exploring the predictions.

The notebook has, for every section, a summary in my own words, the theory behind it (Bayes' rule and the naive assumption, the discriminant function, the likelihood of the logistic model and iteratively reweighted least squares, the measures of the confusion matrix and the meaning of the AUC, weights, SMOTE and the cost-based cutoff), the official Python code executed, and a short analysis of its outputs. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code |
|---|---|---|
| 1 | Naive Bayes | `MultinomialNB` on the loan data with three categorical predictors |
| 2 | Discriminant analysis | `LinearDiscriminantAnalysis` of 3,000 loans and its decision line |
| 3 | Logistic regression | the logit, scikit-learn and `statsmodels` fits, odds, a spline model, a partial residual plot |
| 4 | Evaluating classification models | confusion matrix, precision, recall, specificity, ROC curve, AUC |
| 5 | Strategies for imbalanced data | the rare class problem, weighting, SMOTE, ADASYN, four classifiers compared |

## Highlights from the notebook

- **Naive Bayes** gives a probability of default of 0.654 for the loan in row 146 of the data.
- **Logistic regression** on the 45,342 balanced loans: a small-business loan has about 3.4 times the odds of default of a credit-card loan, a longer employment about 0.70 times; the coefficients of scikit-learn are those of the second class (`paid off`) and have the opposite sign to those of a model of default.
- **Evaluation.** Accuracy 0.6365, precision 0.638, recall 0.632, specificity 0.641 and an AUC of 0.692: a moderate separation of the classes.
- **The rare class.** In the full training set (119,987 loans, 18.9% in default) the logistic regression predicts only 1.0% of the loans as defaults; with weights it predicts 61.1%, after SMOTE 29.2% and after ADASYN 27.5%.
- **Decision boundaries.** The decision tree has a step-like boundary, whereas the linear discriminant analysis, the logistic regression and the generalized additive model have nearly the same smooth one.

## Notes on the book vs. the current library

- The official code ran with the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell), one change marked `# CHANGED` (`gridsearch(..., progress=False)` to avoid a progress bar with the elapsed time) and the seeds added (marked `NOT IN THE BOOK`) before SMOTE and ADASYN, which the script leaves random.
- scikit-learn 1.8 and later deprecate the argument `penalty` that the code passes to `LogisticRegression`; the code still works and the warning is silenced in the setup cell.
- Importing `dmba` selects the non-interactive `Agg` backend of Matplotlib when it finds no display, so the notebook has one extra cell (`%matplotlib inline`, not in the book) that shows the figures again.
- `imbalanced-learn`, `pygam` and `dmba` are not part of a standard Python installation; the setup cell installs them when they are missing (for example in Google Colab).
- The script prints through `print(..., print(...))` in several places, which shows the number first and then a line ending in `None`; the cell under the heading *undersampling* shows the rare class problem and does not undersample.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
