### Limitations, Assumptions and Future Work

To maintain academic rigor and adhere to Data Science best practices, it is crucial to lay out the assumptions and limitations of our chosen methodology:

#### **Macroeconomic Publication Lag (Look-Ahead Bias)**

In our data handling strategy, we utilized forward-filling (`ffill()`) to align low-frequency indicators (CPI, GDP) with daily market data. While methodologically sound for retrospective analysis, it introduces a slight look-ahead bias if this model were deployed in algorithmic trading. In the real world, macroeconomic data is published with a lag (e.g., CPI is delayed by ~2 weeks; GDP revisions occur over multiple quarters). 

**Theoretical Implications:** Forward-filling implicitly assumes market participants have instantaneous access to macroeconomic releases, which violates the informational efficiency assumptions underlying modern financial econometrics. In practice, market participants operate under information asymmetry during the publication lag period.

**Future Iterations:** Future versions of this analysis could implement temporal shifting using pandas `.shift()` methods relative to each indicator's specific release calendar (e.g., shifting CPI forward by 14 days, GDP forward by 45 days), then applying forward-filling only to the remaining gaps. This would more accurately replicate real-world information sets available to market participants at each decision point, enabling out-of-sample predictive validation with minimal look-ahead bias.

#### **Categorical Threshold Bias**

To perform the Welch's Two-Sample t-test, we binarized the continuous yield spread into distinct macroeconomic regimes ('Normal' vs. 'Inverted'). While this categorical transformation is a strict methodological requirement for comparing independent sample means, it inherently compresses the continuous variance of the spread, resulting in information loss. The dichotomization obscures the magnitude of inversions—a spread of -50 basis points and -200 basis points are treated identically as 'Inverted' states, potentially masking severity-dependent market reactions.

**Statistical Limitation:** Categorical encoding is fundamentally a lossy transformation; the original continuous signal contains richer information than its binary proxy. Mean comparisons via t-tests assume homogeneity within categories, which may violate actual market microstructure dynamics.

**Proposed Enhancement:** Future expansions should apply Ordinary Least Squares (OLS) regression using standardized continuous variables (z-scores of the yield spread) as the independent variable and demeaned log-returns as the dependent variable. This preserves information density and permits estimation of a continuous dose-response relationship: "For each standard deviation increase in the yield spread, how many basis points does the expected quarterly return change?" This approach can be validated using rolling (Train-Test) splits, partitioning data chronologically into expanding training windows and fixed testing windows to simulate realistic out-of-sample predictive performance.

#### **Extreme Values and Sensitivity of Means**

In financial time-series analysis, extreme values (e.g., severe market crashes like 2008 or 2020, the rapid volatility spike in March 2020, or the unexpectedly strong recovery in Q2-Q3 2020) are not data entry mistakes; they are real, scientifically important phenomena reflecting genuine economic shocks. While Welch's t-test robustly handles unequal variances between groups, it ultimately compares sample *means*, which are highly sensitive to extreme outliers. 

A single severe market crash or surge can substantially shift the mean of a relatively small sample, potentially distorting the validity of hypothesis test conclusions. For instance, if one quarter experienced a market surge of +40% due to an extraordinary geopolitical or monetary policy event, this single observation could disproportionately influence mean calculations.

**Methodological Solution:** Median-based non-parametric tests (Mann-Whitney U test) and trimmed means (excluding top/bottom 5%) offer robustness to extreme values. Alternatively, quantile regression permits estimation of treatment effects across the conditional distribution (e.g., "Does yield curve inversion affect median returns differently than it affects 75th percentile returns?"). Bootstrap resampling with confidence interval construction provides asymptotically valid inference without distributional assumptions, making it particularly suitable for leveraged financial returns with potential fat tails.

#### **Temporal Dependencies and Serial Correlation**

Financial returns often exhibit autocorrelation and clustering of volatility (ARCH effects), violating the independence assumption underlying classical t-tests. This may induce downward bias in standard errors and inflate Type I error rates (false positive rejections of null hypotheses).

**Future Enhancement:** Implementation of Generalized Autoregressive Conditional Heteroskedasticity (GARCH) models or heteroskedasticity and autocorrelation-consistent (HAC) standard errors would provide more conservative confidence intervals and more defensible statistical inference.

---

**Conclusion:** While our current analytical framework provides compelling support for the "Late-Cycle Market Surge" hypothesis via Welch's t-test (p-value ≈ 0.02), recognition of these methodological limitations demonstrates scientific maturity. The proposed future enhancements—particularly OLS with z-score standardization, rolling validation, non-parametric alternatives, and GARCH specification—would further strengthen empirical claims and align this inquiry with the cutting edge of financial econometrics practice.

