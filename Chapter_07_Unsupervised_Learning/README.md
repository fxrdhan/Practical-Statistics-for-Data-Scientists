# Chapter 7 — Unsupervised Learning

**Notebook:** [`Chapter_07_Unsupervised_Learning.ipynb`](Chapter_07_Unsupervised_Learning.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_07_Unsupervised_Learning/Chapter_07_Unsupervised_Learning.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 7 looks for structure in the predictors alone, with no outcome to predict. It covers:

- **principal components analysis**: the principal components and their loadings, the screeplot, and the correspondence analysis of a table of counts;
- **K-means clustering**: the algorithm, the interpretation of the clusters and the choice of the number of clusters with the elbow plot;
- **hierarchical clustering**: the agglomerative algorithm, the dendrogram and four measures of dissimilarity (single, average, complete and Ward linkage);
- **model-based clustering**: the multivariate normal distribution, mixtures of normals fitted by the EM algorithm and the choice of the model with the BIC;
- **scaling and categorical variables**: standardization, dominant variables, Gower's distance and the problems of clustering mixed data.

The notebook has, for every section, a summary in my own words, the theory behind it (the eigenproblem of the covariance matrix, the inertia of a correspondence analysis, the K-means objective and Lloyd's algorithm, the linkage formulas and Ward's criterion, the EM algorithm and the BIC, Gower's distance), the official Python code executed, and a short analysis of its outputs. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code |
|---|---|---|
| 1 | Principal components analysis | two stocks, sixteen stocks (screeplot, loadings), correspondence analysis of household tasks (`prince`) |
| 2 | K-means clustering | two stocks, sixteen stocks (cluster sizes, centres), the elbow plot |
| 3 | Hierarchical clustering | eighteen stocks (dendrogram, clusters), four measures of dissimilarity |
| 4 | Model-based clustering | the bivariate normal distribution, a mixture of two normals, BIC for 1 to 8 components and four covariance types |
| 5 | Scaling and categorical variables | scaling the loan data, dominant variables in a PCA, five loans for Gower's distance, mixed data |

## Highlights from the notebook

- **PCA of two stocks.** The daily price changes of `XOM` and `CVX` have a correlation of 0.79; the first principal component (loadings 0.665 and 0.747) carries 89.6% of their variance.
- **PCA of sixteen stocks.** The first component, with positive loadings for all stocks, carries 44.5% of the variance and the first five 80.9%; the second contrasts the energy stocks with Apple and the retail stocks.
- **Correspondence analysis.** Two dimensions carry 88.6% of the inertia of the table of household tasks; laundry and meals lie near the wife, repairs and driving near the husband, holidays and finances near *jointly*.
- **K-means.** Sixteen stocks divided into five clusters of days: strong rises (130 days), strong falls (152), mild rises (322) and two contrasting clusters (energy against Apple and retail). The elbow plot has no sharp elbow.
- **Hierarchical clustering.** The 18 stocks form the four energy stocks, a group of 12 stocks, and `AMZN` and `GOOGL` alone. With four clusters, single linkage puts 1,127 of 1,131 days in one cluster, Ward's method gives clusters of 464, 290, 254 and 123 days.
- **Mixtures of normals.** The lowest BIC of the 32 models (4,589.8) is for two components with their own covariance matrices: a narrow cloud (916 days) and a wide one (215 days).
- **Scaling.** Without scaling, K-means divides the defaulted loans by income (one cluster of 88 loans with an average income of about 410,000 dollars); with standardized variables the clusters differ in the debt-to-income ratio, the utilization and the loan amount.
- **Dominant variables and mixed data.** `GOOGL` and `AMZN` take the first two principal components of unstandardized data (loadings 0.857 and 0.874); with dummy variables, K-means on mixed data finds the three types of home ownership.

## Notes on the book vs. the current library

- The official code ran with the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell), with no change to the code itself. The notebook adds the seeds that the script lacks (`np.random.seed(...)  # NOT IN THE BOOK`) and eight short cells that print numbers the book code only draws (also marked `# NOT IN THE BOOK`).
- `prince` (correspondence analysis) and `adjustText` (labels of the plot) are not part of a standard Python installation; the setup cell installs them when they are missing (a fresh environment, or Google Colab, may not have them). The code ran with `prince` 0.22.2 and `adjustText` 1.4.0.
- With `n_init='auto'`, `KMeans` runs the algorithm once with its default initialization, not ten times as the comment of the script says; `GaussianMixture` has `warm_start=True` in the script, which has no effect because each model is fitted only once; in `scikit-learn` a lower BIC is better.
- Gower's distance is still not available in the installed `scikit-learn` and `SciPy`, so the section has no Python code for it (as in the official repository).
- The file `sp500_data.csv.gz` has no description of its units; the values behave like daily changes of the stock prices, not like percentage returns, which is why `GOOGL` and `AMZN` dominate the unscaled analyses.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
