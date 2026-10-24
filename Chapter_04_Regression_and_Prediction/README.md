# Chapter 4 — Regression and Prediction

**Notebook:** [`Chapter_04_Regression_and_Prediction.ipynb`](Chapter_04_Regression_and_Prediction.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_04_Regression_and_Prediction/Chapter_04_Regression_and_Prediction.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 4 models an outcome as a function of predictors, to predict it and to explain it. It covers:

- **simple linear regression**: the regression equation, fitted values and residuals, least squares, prediction against explanation;
- **multiple linear regression** on the King County house prices: assessing the model, cross-validation, model selection and stepwise regression, weighted regression;
- **prediction using regression**: the dangers of extrapolation, confidence and prediction intervals;
- **factor variables**: dummy variables, factors with many levels, ordered factors;
- **interpreting the regression equation**: correlated predictors, multicollinearity, confounding variables, interactions and main effects;
- **regression diagnostics**: outliers, influential values, heteroskedasticity, non-normality and correlated errors, partial residual plots;
- **polynomial and spline regression** and generalized additive models;
- the additional material of the official repository (not in the book): regularization with the lasso.

The notebook has, for every section, a summary in my own words, the theory behind it ($\hat\beta = (X^\top X)^{-1}X^\top y$, $R^2$ and the $F$ test, information criteria, the hat matrix, Cook's distance, the variance inflation factor, B-splines and penalized splines, the lasso criterion), the official Python code executed, and a short analysis of its outputs. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code |
|---|---|---|
| 1 | Simple linear regression | lung disease data: scikit-learn fit, fitted values and residuals |
| 2 | Multiple linear regression | house prices: scikit-learn and `statsmodels` fits, full model, stepwise selection with `dmba`, weighted regression |
| 3 | Prediction using regression | none (summary and theory of the intervals) |
| 4 | Factor variables in regression | dummy variables, zip codes grouped into five zip groups |
| 5 | Interpreting the regression equation | correlated predictors, confounding with the zip group, interactions |
| 6 | Regression diagnostics | outliers, influential values, heteroskedasticity, partial residual plots |
| 7 | Polynomial and spline regression | polynomial, cubic spline, generalized additive model (`pygam`) |
| 8 | Additional material (official repository, not in the book) | the lasso path and cross-validation |

## Highlights from the notebook

- **Simple regression.** The lung capacity (PEFR) of 122 workers falls by 4.185 units per year of exposure (intercept 424.6); the residuals are large, so the line explains only part of the variation.
- **House prices.** The model with five predictors has an R-squared of 0.5406 and an RMSE of 261,220 dollars on the data it was fitted to; the full model has 0.595, and the stepwise search with the AIC keeps eight of the twelve columns.
- **Coefficients depend on the model.** The bedrooms have a coefficient of -51,947 with the living area in the model and +27,151 without it; the single-family indicator goes from -84,678 to +19,324 when the zip group is added.
- **Interactions.** With the interaction of the living area and the zip group, a square foot is worth 114.8 dollars in the cheapest group and 341.4 in the most expensive one (R-squared 0.682).
- **Diagnostics.** In the zip code 98105 one sale (record 24333) has a studentized residual of -4.33: it sold for 119,748 dollars, the model predicts about 877,500. Dropping 6 of the 313 sales with the largest Cook's distance changes most coefficients by 10% to 15% and flips the sign of the bathrooms. The residuals are heteroskedastic and heavy-tailed.
- **Nonlinearity.** A quadratic term, a cubic spline and a GAM improve the fit of the living area (AIC 8,464 for the linear model, 8,450, 8,445 and 8,443 for the three).
- **Lasso.** On unstandardized predictors the cross-validated lasso keeps four coefficients (living area, lot size, finished basement, year of renovation) and sets the grade to zero.

## Notes on the book vs. the current library

- The official code ran with the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell) and three changes marked `# CHANGED`: `model.params[0]` and `result_poly.params[2]` raise a `KeyError` in recent `pandas` and are replaced by `.iloc[0]` and `.iloc[2]`; `gam.gridsearch(X, y)` is called with `progress=False` to avoid a progress bar with the elapsed time.
- Importing `dmba` selects the non-interactive `Agg` backend of Matplotlib when it finds no display, so the notebook has one extra cell (`%matplotlib inline`, not in the book) that shows the figures again.
- `pygam` and `dmba` are not part of a standard Python installation; the setup cell installs them when they are missing (a fresh environment, or Google Colab, may not have them).
- The summaries of `statsmodels` print the date and the time of the run, and `pygam` warns that the p-values of its summary are unreliable.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
