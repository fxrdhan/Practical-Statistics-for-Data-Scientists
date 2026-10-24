# Chapter 6 — Statistical Machine Learning

**Notebook:** [`Chapter_06_Statistical_Machine_Learning.ipynb`](Chapter_06_Statistical_Machine_Learning.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_06_Statistical_Machine_Learning/Chapter_06_Statistical_Machine_Learning.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 6 presents the data-driven methods of machine learning, which make few assumptions about the data and predict well, at the price of being harder to interpret. It covers:

- **K-nearest neighbors**: classifying a loan by a vote of the most similar loans, distance metrics, the standardization of the predictors, and the use of a KNN probability as a new feature;
- **tree models**: recursive partitioning, the Gini impurity and the entropy, and how a tree is stopped from growing;
- **bagging and the random forest**: bootstrap samples, a random subset of the predictors at each split, the out-of-bag estimate, and two measures of variable importance (the accuracy decrease and the Gini decrease);
- **boosting**: XGBoost, regularization against overfitting, and the choice of the hyperparameters by cross-validation.

The notebook has, for every section, a summary in my own words, the theory behind it (the KNN classifier and the curse of dimensionality, the split criterion and cost-complexity pruning, the variance of an average of correlated trees and the out-of-bag estimate, gradient boosting and the objective of XGBoost, cross-validation), the official Python code executed, and a short analysis of its outputs. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code |
|---|---|---|
| 1 | K-nearest neighbors | a small example (K = 20), standardization, KNN as a feature engine |
| 2 | Tree models | a decision tree for the loan data (`dmba`, Graphviz), the partition of the plane, impurity measures |
| 3 | Bagging and the random forest | a random forest, the out-of-bag accuracy against the number of trees, variable importance |
| 4 | Boosting | XGBoost, regularization (with and without a penalty), cross-validation of the learning rate and the depth |

## Highlights from the notebook

- **KNN.** With K = 20, 9 of the 20 neighbours of the first loan are in default, so the probability of default is 0.45. Without standardization the five nearest neighbours of a loan all have the same revolving balance (within 3 dollars) and differ a lot in the other variables.
- **Tree.** A tree with two predictors has 6 leaves and classifies 61.1% of the 3,000 training loans correctly; its first split is a borrower score of 0.575.
- **Random forest.** The out-of-bag accuracy on the two predictors is about 61% for any number of trees from 20 to 505. By permutation the most important predictors are the borrower score (0.076), the grade (0.042) and the term (0.031), while the Gini decrease favours numeric variables with many values.
- **XGBoost.** The model without penalty has a training error of 0.106 and a validation error of 0.361; with the penalty and a smaller learning rate the validation error is 0.333. The validation error of the unpenalized model is lowest (0.339) after 23 trees and then rises.
- **Cross-validation.** Of 9 combinations of the learning rate and the depth, the lowest average error (0.3276) is for a learning rate of 0.1 and a depth of 3, at the edge of the grid.

## Notes on the book vs. the current library

- The official code ran with the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell), with no change to the code itself. The notebook adds the seeds that the script lacks (`np.random.seed(...)  # NOT IN THE BOOK`).
- `dmba` is not part of a standard Python installation, and `plotDecisionTree` needs the program Graphviz (`dot`); the setup cell installs `dmba` when it is missing, Graphviz is present in Google Colab and otherwise has to be installed with the package manager of the system. Importing `dmba` selects the non-interactive `Agg` backend of Matplotlib when it finds no display, so the notebook has one extra cell (`%matplotlib inline`, not in the book) that shows the figures again.
- The script converts `outcome` to a categorical variable with the order *paid off*, *default*, but `scikit-learn` uses the classes in alphabetical order, so the first column of `predict_proba` is the probability of *default*; the KNN cell overwrites the column `borrower_score` of the data with it, which runs in the opposite direction to the original column. The XGBoost cell calls `predict_proba(X)[:, 0]` `prob_default`, but with the outcome coded 1 for default this column is the probability of *paid off*.
- The loop of the regularization example uses `iteration_range = [1, ntree_limit + 1]`, which leaves out the first boosting round; the code is reproduced as it is.
- The notebook takes about eight minutes to run on four cores (98 forests of the out-of-bag loop and 45 XGBoost models of the cross-validation). The numbers of the random parts depend on the seeds, and `xgboost` can give slightly different numbers on another machine.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
