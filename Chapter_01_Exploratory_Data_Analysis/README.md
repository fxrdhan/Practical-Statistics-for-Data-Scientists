# Chapter 1 — Exploratory Data Analysis

**Notebook:** [`Chapter_01_Exploratory_Data_Analysis.ipynb`](Chapter_01_Exploratory_Data_Analysis.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_01_Exploratory_Data_Analysis/Chapter_01_Exploratory_Data_Analysis.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 1 is about looking at the data before modelling it. It covers:

- **structured data**: numeric (continuous, discrete) and categorical (binary, ordinal) variables, and the rectangular table, with its rows, columns and index, that holds them;
- **estimates of location**: the mean, the trimmed mean, the median, and the weighted mean and weighted median;
- **estimates of variability**: the standard deviation, the interquartile range and the median absolute deviation;
- **the distribution of the data**: percentiles, the boxplot, the frequency table, the histogram and the density plot;
- **binary and categorical data**: proportions, the mode, the expected value and the bar chart;
- **correlation**: the correlation matrix, the heatmap, the ellipse plot and the scatterplot;
- **two or more variables**: hexagonal binning and contour plots, contingency tables, boxplots and violin plots, and conditioning on a third variable with facets.

The notebook reproduces the Python code of every section that has code, and adds a theory block (Stevens' scales, tidy data, robustness and the breakdown point, the nine definitions of a percentile, histogram and kernel-density theory, Fisher's transformation, the chi-square test and Cramér's $V$) and experiments that test the statements the book makes in prose. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code | What the notebook adds |
|---|---|---|---|
| 1 | Elements of structured data | none | A statistical type for the main variables of the datasets, the ZIP code that is a number but a name, the `category` dtype |
| 2 | Rectangular data | none | Shape, index and missing values of every table, wide and long layouts |
| 3 | Estimates of location | mean, trimmed mean, median, weighted mean and median | The mean and the median as minimizers of two losses, breakdown under gross outliers, the trimming proportion, a weighted median by hand, efficiency against robustness |
| 4 | Estimates of variability | standard deviation, IQR, MAD | The $n-1$ divisor by simulation, the scale constants 1.349 and 0.6745, breakdown of the three scale estimates, Chebyshev's inequality |
| 5 | Exploring the data distribution | percentiles, boxplot, frequency table, histogram, density | The nine percentile definitions, a boxplot by hand, rules for the number of bins, the bandwidth of a density estimate, equal-width against equal-count bins |
| 6 | Exploring binary and categorical data | frequency table, bar chart | Entropy and expected value of a categorical variable, a Pareto chart, an ordinal axis |
| 7 | Correlation | correlation matrix, heatmap, ellipse plot, scatterplot | Pearson by hand, Spearman and Kendall, one outlier, Anscombe's quartet, a confidence interval, spurious correlation of random walks |
| 8 | Exploring two or more variables | hexbin, contour plot, contingency tables, boxplot, violin plot, facets | Overplotting in numbers, a chi-square test with Cramér's $V$, the numbers behind boxplot and violin, pooled against group-wise slopes |

## Highlights from the notebook

- **Types are about meaning.** `ZipCode` is stored as a float and has a mean (98,309.35) that is not the code of any place; 6 of its 467,900 values cannot be five-digit ZIP codes (0, 98, 9800, 9804, 9806501, 98157059) and 8 more lie outside the range of the county, which a numeric column cannot reject. The `category` dtype cuts the memory of the loan grade from 22.5 MB to 0.45 MB.
- **Robustness has a price list.** Replacing one of the 50 state populations by $10^{12}$ destroys the mean, five do not destroy the 10% trimmed mean, and 24 do not destroy the median; the standard deviation breaks with one outlier, the IQR survives 12 and the MAD 24. On normal data the median has a standard deviation 24% larger than the mean's and the 10% trimmed mean only 2.5% larger; with 5% contamination the trimmed mean has less than half the variability of the mean.
- **Small samples depend on conventions.** The nine definitions of a percentile give a 95th percentile of the 50 murder rates between 6.5 and 7.5, because the upper tail has a gap (6.6, then 8.6 and 10.3). The rules for the number of bins give 6 to 14 bins for the 50 populations.
- **The boxplot flags candidates, not errors.** It marks 4 of 50 states (8%) against 0.7% for a normal sample; for the daily delays of the airlines it flags 1.6% to 4.8% of the days because the data are right-skewed.
- **Correlation needs a picture and a caveat.** Pearson's $r$ of AT&T and Verizon is 0.678 (95% interval 0.637 to 0.714); one added wrong day out of 755 turns it into $-0.103$ while Spearman and Kendall do not move. Four Anscombe data sets share $r = 0.816$ and look nothing alike, and independent random walks have $|r| > 0.5$ in 39% of the pairs while their changes never do.
- **Large tables make everything significant.** For the 450,961 loans the chi-square test of grade against status gives a p-value that underflows to 0, yet Cramér's $V$ is 0.084, and thinning the data to every 100th loan leaves $V$ unchanged (0.081) while $\chi^2$ falls from 9,594 to 88.
- **Condition before you pool.** In four ZIP codes the slope of assessed value on area ranges from 78 to 142 dollars per square foot, and the pooled correlation (0.47) is lower than the correlation inside each ZIP code (0.65 to 0.74).

## Notes on the book vs. the current library

- The official code ran unchanged on the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell).
- The contour plot of the book draws an unseeded random sample of 10,000 houses, so its lines change a little from run to run; the notebook sets a seed (marked `NOT IN THE BOOK`).
- The installed `pandas` has a dedicated `str` dtype for text and keeps missing cells in `DataFrame.stack()`; the extras that depend on this are written for it.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
