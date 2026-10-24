# Chapter 3 — Statistical Experiments and Significance Testing

**Notebook:** [`Chapter_03_Statistical_Experiments_and_Significance_Testing.ipynb`](Chapter_03_Statistical_Experiments_and_Significance_Testing.ipynb)
<a href="https://colab.research.google.com/github/fxrdhan/Practical-Statistics-for-Data-Scientists/blob/main/Chapter_03_Statistical_Experiments_and_Significance_Testing/Chapter_03_Statistical_Experiments_and_Significance_Testing.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Summary

Chapter 3 asks whether a difference seen in an experiment is real or could have been produced by chance. It covers:

- the **A/B test**: random assignment, a predefined metric and a concurrent control;
- **hypothesis tests**: the null and the alternative hypothesis, one-way and two-way tests;
- **resampling**: the permutation test (random, exhaustive and bootstrap versions);
- **statistical significance and p-values**, alpha, and the two types of error;
- **$t$-tests** for two means;
- **multiple testing** and the inflation of false positives;
- **degrees of freedom**, including the dummy-variable trap;
- **ANOVA** and the $F$-statistic;
- the **chi-square test**: a resampling approach, the chi-square distribution, Fisher's exact test, and a data set of digit frequencies;
- the **multi-arm bandit** algorithm (epsilon-greedy and Thompson sampling);
- **power and sample size**.

The notebook reproduces the Python code of the chapter and adds a theory block for every section (potential outcomes and randomization inference, the pieces of a test, the exact Monte Carlo p-value, the hypergeometric distribution behind the conversion test, Welch's statistic, FWER and FDR procedures, the decomposition of the sum of squares, Pearson residuals, regret and Thompson sampling, the power of the $z$-test and Cohen's $h$) and experiments that test the statements the book makes in prose. The datasets are downloaded from the official repository when the notebook runs.

## Sections

| # | Section of the book | Book code | What the notebook adds |
|---|---|---|---|
| 1 | A/B testing | none | Randomization against self-selection, the false-positive rate of A/A tests, the cost of peeking at the results |
| 2 | Hypothesis tests | none | One- and two-sided p-values from one permutation distribution, a direction chosen after the data, the permutation test with unequal variances |
| 3 | Resampling | permutation test of the session times | An exact test, the Monte Carlo error of a permutation p-value, permutation against bootstrap, $t$ and rank tests, other statistics |
| 4 | Statistical significance and p-values | permutation test of the conversion rates, $\chi^2$ test | The exact p-value, type I and type II error by simulation, the distribution of p-values, what a significant result means, significance against importance |
| 5 | $t$-tests | two $t$-tests of the session times | Welch's statistic by hand, $t$ against rank tests, paired against independent, test against confidence interval |
| 6 | Multiple testing | none | The chance of a false positive among many tests, Bonferroni, Holm and Benjamini-Hochberg, many correlated metrics |
| 7 | Degrees of freedom | none | Why $n-1$, the degrees of freedom of the ANOVA table, the dummy-variable trap |
| 8 | ANOVA | permutation test of four pages, the $F$ table | The $F$ statistic by hand, three equivalent permutation statistics, pairwise comparisons, a two-way ANOVA, the $F$-test with unequal variances |
| 9 | Chi-square test | click rates (resampling and $\chi^2$), digit frequencies | The statistic by hand, exact p-values for the two resampling schemes, small expected counts, a goodness-of-fit test of the digits |
| 10 | Multi-arm bandit algorithm | none | Four allocation policies, the choice of epsilon, what adaptive sampling does to estimates and tests |
| 11 | Power and sample size | sample sizes for two conversion rates | The sample size by five methods and by simulation, power curves, the exaggeration of significant effects |

## Highlights from the notebook

- **Randomization removes the bias.** An observational comparison of a feature with true effect 1 averages 3.12, because the users who adopt it are more engaged; the randomized experiment averages 1.00.
- **Using a test as designed.** A/A tests reject at the nominal rates (1.0%, 5.1% and 10.0% at the 1%, 5% and 10% levels). Looking at an A/A experiment 20 times and stopping at the first significant result gives 24.6% false positives instead of 5%; choosing the direction of a one-sided test after seeing the data gives 10.1%.
- **Permutation tests.** The session-time difference of 35.67 seconds has a p-value of 0.121 in the script's 1,000 permutations and about 0.135 with many more (the standard error of a Monte Carlo p-value is $\sqrt{p(1-p)/R}$, 0.011 for 1,000 permutations). Five methods give 0.114 to 0.141. With unequal variances and unequal group sizes the permutation test of equal means rejects 26% of true nulls when the small group is the noisy one (0.15% in the opposite arrangement), Welch's test 5% in both.
- **p-values.** The conversion test has an exact p-value of 0.3499 (Fisher's exact test, the hypergeometric tail; the book's chi-square value is 0.3498). The experiment would detect the observed difference in only 11% of repetitions. If one tested hypothesis in ten is true and the power is 0.8, about 35% of the significant results are false. A difference of 0.01 standard deviations has $p = 1.5 \times 10^{-12}$ with a million observations per group.
- **$t$-tests.** Welch's test by hand equals `scipy` and `statsmodels` ($t = -1.098$, 27.7 degrees of freedom). In the simulation with 15 observations per group the Mann-Whitney test had more power for heavy-tailed and lognormal data (and 3.6 points less for normal data); a paired design analysed as two groups has a power of 0.4% against 67.6%.
- **Multiple testing.** Twenty true nulls give a 64% chance of a false positive. With 100 real effects among 1,000 tests Bonferroni and Holm find 15% of them, Benjamini-Hochberg 50% with a false discovery proportion of 4.5%.
- **ANOVA.** The four pages have $F = 2.74$, $p = 0.078$; the permutation tests with three equivalent statistics give 0.081. The last lines of the book's cell print half of $F$ and of the p-value (1.37 and 0.039), which is not the test. The pair of pages 2 and 4 has $p = 0.0067$ with Welch and Bonferroni and 0.053 with Tukey's HSD. The classical $F$-test rejects 37.9% of true nulls when the smallest of three groups is the noisiest.
- **Chi-square.** The click table has $\chi^2 = 1.67$ with $p = 0.435$; the exact values are 0.482 and 0.486 under the two resampling schemes. With only 3 clicks in the table the nominal 5% test rejects 11.1% of true nulls. The digit frequencies have $\chi^2 = 174.4$ against a uniform model.
- **Bandits.** Thompson sampling has a regret of 24.9 against 166.7 for a fixed split (explore-then-greedy 26.2, epsilon-greedy 43.1), but the observed rate of the worse version is 13% too low, and a naive $z$-test rejects 9.4% of true nulls.
- **Power.** 116,603 visitors per group are needed to detect a rise from 1.1% to 1.21%, 5,489 for 1.1% to 1.65%; the sample size scales as $1/\text{effect}^2$. At a power of 9% the significant estimates exaggerate the true effect 3.8 times.

## Notes on the book vs. the current library

- The official code ran with the versions printed by the setup cell, apart from the path of the data (it comes from the setup cell), the seeds (cells that draw random numbers without a seed start with a seeding line marked `NOT IN THE BOOK`) and one change marked `# CHANGED`: `four_sessions.groupby('Page').mean().var()[0]` raises a `KeyError` in recent pandas and is replaced by `.var().iloc[0]`.
- The script's `random.seed(1)` before the ANOVA permutations has no effect, because `perm_test` uses NumPy's random generator; the notebook seeds NumPy.
- The last lines of the ANOVA cell print the $F$-statistic and the p-value of `f_oneway` divided by 2 (1.3699 and 0.0388), whereas the ANOVA table above them gives $F = 2.7398$ and $p = 0.0776$. The notebook reproduces the code and points this out.
- In the conversion test the observed difference is price A minus price B, while `perm_fun(conversion, 23739, 22588)` returns the second group minus the first; the permutation distribution is almost symmetric, so the p-value is hardly affected.
- The script's comment says that SciPy has Fisher's exact test only for $2 \times 2$ tables; the SciPy version used here also accepts the $2 \times 3$ click table but returns slightly different p-values from call to call, so the notebook uses it for the conversions only and enumerates the click table by hand.
- The code and data of the official repository are under the GNU General Public License v3; the data are downloaded when the notebook runs and are not part of this repository.
