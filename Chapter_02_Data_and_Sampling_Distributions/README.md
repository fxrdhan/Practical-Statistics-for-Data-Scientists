# Chapter 2 — Data and Sampling Distributions

**Notebook:** [`Chapter_02_Data_and_Sampling_Distributions.ipynb`](Chapter_02_Data_and_Sampling_Distributions.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_02_Data_and_Sampling_Distributions/Chapter_02_Data_and_Sampling_Distributions.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 2 asks how far a sample can be trusted. It covers:

- **random sampling and sample bias**: samples and populations, simple random and stratified sampling, bias against random error, and why size does not repair quality;
- **selection bias**: data snooping, the vast search effect and regression to the mean;
- the **sampling distribution of a statistic**: the central limit theorem and the standard error;
- the **bootstrap**: estimating a sampling distribution by resampling;
- **confidence intervals**, from the bootstrap and from formulas;
- the **normal distribution** and QQ-plots, and **long-tailed distributions**;
- Student's **$t$-distribution**, the **binomial**, **chi-square** and **$F$** distributions;
- the **Poisson** distribution and its relatives, the exponential and the Weibull distribution.

The notebook reproduces the Python code of the chapter and adds a theory block for every section (stratified-sampling variance, Meng's identity for the error of a mean, the plug-in principle of the bootstrap, coverage of an interval, the construction of a QQ-plot, tails and kurtosis, the $t$, chi-square and $F$ distributions and the relations between them, binomial intervals, the Poisson process, the Weibull hazard) and experiments that test the statements the book makes in prose. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code | What the notebook adds |
|---|---|---|---|
| 1 | Random sampling and sample bias | a population and a sample (figure) | Stratified against simple random sampling, a biased sample whose error does not shrink with its size, the identity that splits the error of a mean into quality and quantity |
| 2 | Selection bias | none | Regression to the mean, the vast search effect and holdout data, a selection that creates a correlation |
| 3 | Sampling distribution of a statistic | means of 5 and of 20 incomes | The $1/\sqrt{n}$ law, the central limit theorem step by step, the finite-population correction, the sampling distribution of six statistics |
| 4 | The bootstrap | the bootstrap of a median | The bootstrap by hand and with two libraries, the Monte Carlo error, the bootstrap against the true sampling distribution, a failure for the maximum |
| 5 | Confidence intervals | 90% and 95% bootstrap intervals | Actual coverage of three intervals, width against $n$ and level, what "90%" means, percentile, basic and BCa intervals |
| 6 | Normal distribution | a QQ-plot of normal data | The 68-95-99.7 rule, a QQ-plot built by hand, a gallery of QQ-plots |
| 7 | Long-tailed distributions | a QQ-plot of the stock NFLX | What the book's code computes from that column, tails of daily price changes, a mean that does not converge, kurtosis of 511 stocks |
| 8 | Student's $t$-distribution | none | Quantiles against the normal, why the standardized mean has heavy tails, coverage of $z$ and $t$ intervals |
| 9 | Binomial distribution | two probabilities | The distribution by hand, the normal approximation, exact coverage of Wald, Wilson and Clopper-Pearson intervals |
| 10 | Chi-square distribution | none | Sums of squared normal variables, the sample variance, a goodness-of-fit test of a die, small expected counts |
| 11 | $F$-distribution | none | A ratio of variances, $F = t^2$, the fragility of the variance-ratio test, the $F$ statistic of an ANOVA |
| 12 | Poisson and related distributions | Poisson, exponential and Weibull samples | The Poisson process, overdispersion, estimating a failure rate, the Weibull hazard and its estimation |

## Highlights from the notebook

- **Quantity does not repair quality.** A sample whose chance of inclusion rises with income has an error of 14,600 to 15,700 dollars (21% to 23% of the mean) for every size from 50 to 5,000, while the error of a random sample falls from 4,695 to 435. A random sample of 50 incomes is more accurate than a biased sample of 20,000. Meng's identity (error = data defect correlation $\times \sqrt{(N-n)/n} \times \sigma$) holds exactly.
- **Selection manufactures findings.** The best of 1,000 useless predictors has $|r| = 0.52$ on average and 0.13 on new data; players selected for an extreme first score keep only a share of it equal to the reliability; selecting on the sum of two independent scores makes them correlated ($r = -0.71$ among the top 10%).
- **The standard error.** It falls as $n^{-0.501}$ for the loan incomes. The distribution of the mean is nearly normal at $n = 20$ in the centre, but the tails of the standardized mean are still 1.8% and 3.2% (nominal 2.5% each) at $n = 20$ and 2.3% and 2.8% at $n = 500$.
- **The bootstrap.** 1,000 resamples give a standard error accurate to about 2%. For the median of 100 incomes the bootstrap estimates average 1.5% above the true standard error, but a single one has a spread of 22%. For the maximum of a sample it fails: 63.4% of the resamples have the sample maximum.
- **Intervals.** For 90% nominal intervals of a skewed population, the coverage at $n = 20$ is 85.9% for the percentile bootstrap, 88.3% for the $t$ interval; at $n = 10$ the bootstrap covers only 82.1%.
- **The column NFLX.** The data file holds daily price changes (1,613 positive, 1,671 negative, 2,363 zero), not prices; the book's code takes logarithms of the positive changes and differences them, which does not give returns. Across 511 stocks, 91% have an excess kurtosis above 1, and days beyond four standard deviations are on average 47 times as frequent as a normal model says.
- **The $t$ and the other distributions.** With $n = 5$ the 95% interval with the normal multiplier covers 87.8%, the $t$ interval 94.9%. The Wald interval for a proportion covers 45% for $p = 0.02$, $n = 30$. The variance interval of the chi-square distribution covers 76.6% for exponential data, and the $F$ test of two variances falsely rejects 16% to 27% of equal-variance experiments for heavy-tailed or skewed data (Brown-Forsythe: 3% to 5%).
- **Events and lifetimes.** Exponential gaps give Poisson counts (chi-square against Poisson(2): p = 0.70); counts with a varying rate have an index of dispersion of 2 and 3.8 times the chance of six or more events; the estimate $1/\bar x$ of a failure rate is 24% too high for $n = 5$ and the percentile bootstrap covers 78%.

## Notes on the book vs. the current library

- The official code ran unchanged on the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell) and seeds: the official script seeds only the first figure and the confidence-interval cells, and the notebook adds a seed (marked `NOT IN THE BOOK`) to the cells that draw random numbers without one.
- The column `NFLX` of the data file holds price changes, so the series that the book's code builds from it is not a series of returns (extra 7(a) shows what it is). The notebook reproduces the code as it is and does not correct it.
- The second confidence-interval cell draws two histograms and displays one figure with both intervals.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
