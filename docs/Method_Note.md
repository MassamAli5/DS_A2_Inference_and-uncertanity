# DS-A2 — Statistical Derivation and Method Note

**Research topic:** Quantifying uncertainty in REY enrichment in Early Cambrian Kakul Garlaniyan phosphorites, northeastern Pakistan.

**Data source:** Ali et al. (2026), *Journal of Asian Earth Sciences*. DOI: 10.1016/j.jseaes.2025.106927.

## 1. Research Questions and Statistical Targets

This investigation uses published bulk-rock and in situ apatite geochemical measurements to quantify uncertainty in rare earth element and yttrium (ΣREY) enrichment.

Two complementary analyses are conducted.

**Study A — Bulk-rock REY enrichment**

Study A estimates the difference between mean bulk-rock ΣREY concentrations in the Upper Phosphorite Layer (UPL) and Lower Phosphorite Layer (LPL):

$$
\Delta_A = \mu_{\mathrm{UPL}}-\mu_{\mathrm{LPL}}
$$

The analysis uses 8 UPL and 10 LPL observations from Supplementary Table S1. The Middle Phosphorite Layer (MPL) provides additional stratigraphic context.

**Study B — In situ apatite REY enrichment**

Study B estimates the difference between parent-weighted mean ΣREY concentrations in pseudo-oolites and pellets, averaged equally across LPL, MPL, and UPL:

$$
\Delta_B=\frac{1}{3}\sum_{\ell}
(\mu_{\mathrm{pseudo},\ell}-\mu_{\mathrm{pellet},\ell})
$$

Supplementary Table S2 contains 103 analytical spots associated with 26 parent rock samples. Multiple spots from the same parent may be statistically dependent.

For both studies, the null hypothesis specifies a zero mean difference and the alternative specifies a nonzero difference. Two-sided inference uses a nominal significance level of 0.05.

A 100 ppm difference serves as a provisional practical-effect benchmark, with 50 and 150 ppm used as additional effect scenarios. These values are not established geological or economic cutoffs.

The investigation is retrospective and exploratory. Its hypotheses and analysis decisions were not prospectively preregistered.

## 2. Sampling Distribution — Study A

The sampling distribution of the difference between two means was investigated through Monte Carlo simulation.

The statistic is:

$$
\hat{\Delta}_A=\bar{X}_{\mathrm{UPL}}-\bar{X}_{\mathrm{LPL}}
$$

The simulation generated 10,000 hypothetical repeated experiments under independent normal sampling models. The group means and standard deviations were calibrated to the original observations, preserving sample sizes of 8 UPL and 10 LPL specimens.

Under independence, the model-based variance of the mean difference is:

$$
\operatorname{Var}(\hat{\Delta}_A)=
\frac{\sigma_{\mathrm{UPL}}^2}{n_{\mathrm{UPL}}}
+\frac{\sigma_{\mathrm{LPL}}^2}{n_{\mathrm{LPL}}}
$$

Replacing population standard deviations with sample estimates gives:

$$
\widehat{SE}(\hat{\Delta}_A)=
\sqrt{
\frac{s_{\mathrm{UPL}}^2}{n_{\mathrm{UPL}}}
+\frac{s_{\mathrm{LPL}}^2}{n_{\mathrm{LPL}}}
}
$$

The simulation produced a standard deviation of 75.57 ppm, compared with the theoretical plug-in standard error of 75.99 ppm. The close agreement verifies numerical consistency under the assumed model.

The normal simulation is a hypothetical sampling experiment, not additional geological data.

## 3. Confidence Intervals — Study A

### 3.1 Welch Confidence Interval

The Welch method was selected because the two groups have unequal sample sizes and different observed variances.

The approximate 95% confidence interval is:

$$
\hat{\Delta}_A \pm t_{0.975,\nu}\widehat{SE}(\hat{\Delta}_A)
$$

The Welch–Satterthwaite degrees of freedom are:

$$
\nu=
\frac{(a+b)^2}
{\frac{a^2}{n_{\mathrm{UPL}}-1}+
\frac{b^2}{n_{\mathrm{LPL}}-1}}
$$

where:

$$
a=\frac{s_{\mathrm{UPL}}^2}{n_{\mathrm{UPL}}},
\qquad
b=\frac{s_{\mathrm{LPL}}^2}{n_{\mathrm{LPL}}}
$$

The observed UPL minus LPL difference was **210.30 ppm**, with a 95% Welch interval of **48.44–372.16 ppm**.

The manual calculation was independently compared with SciPy's unequal-variance t-test confidence-interval implementation.

### 3.2 Nonparametric Bootstrap

A percentile bootstrap was also performed using 10,000 repetitions.

LPL and UPL observations were independently resampled with replacement within their respective groups, preserving the original sample sizes.

The 95% percentile interval was defined by the 2.5th and 97.5th percentiles of the bootstrap differences:

$$
CI_{\mathrm{bootstrap}}=
[Q_{0.025}(\hat{\Delta}^{*}),
Q_{0.975}(\hat{\Delta}^{*})]
$$

The resulting interval was **68.41–349.39 ppm**.

Both intervals exclude zero but overlap the provisional 100 ppm meaningful-effect benchmark.

### 3.3 Lithological Sensitivity

Because LPL includes several lithologies whereas UPL comprises phosphorite samples, a restricted phosphorite-only comparison was conducted.

The original difference of 210.30 ppm decreased to **16.54 ppm** after restriction, with a 95% Welch interval of **−181.84–214.92 ppm**.

This sensitivity indicates that the original bulk-rock comparison depends strongly on lithological composition. The restricted analysis changes the represented sample population and does not isolate the causal influence of stratigraphic position.

## 4. Study B — Parent-Cluster Bootstrap

In situ analytical spots were first summarized within each parent rock and grain-type combination.

Parent-level means were then averaged within each grain type and stratigraphic layer. The three layer-specific contrasts were given equal weight.

The observed overall pseudo-oolite minus pellet difference was **169.15 ppm**.

A layer-stratified cluster bootstrap was performed using 10,000 resampling attempts.

Within each layer, entire parent rocks were sampled with replacement, preserving the available grain-type measurements associated with each sampled parent.

Twenty-three bootstrap repetitions lacked complete grain-type representation and were recorded as incomplete.

The 9,977 complete repetitions produced a bootstrap standard error of **40.55 ppm** and a conditional 95% percentile interval of **87.55–247.97 ppm**.

The interval excludes zero but overlaps the provisional 100 ppm benchmark.

The procedure accounts for the parent-rock grouping in its resampling design but does not verify independence between different parent samples or geological representativeness. Excluding incomplete repetitions may affect interval coverage.

A supplementary paired-parent sensitivity analysis used the 13 parent samples containing both grain types. Its equal-layer-weighted mean difference was **170.88 ppm**, although substantial LPL variability remained.

## 5. Statistical Power Analysis

Study A statistical power was investigated using Monte Carlo simulations and a two-sided Welch t-test at a significance level of 0.05.

The simulation design included:

- Independent sample sizes of 5, 10, 20, and 40 specimens per group.
- True mean differences of 0, 50, 100, 150, and 200 ppm.
- Noise multipliers of 0.5, 1.0, and 1.5 relative to the observed group standard deviations.
- 2,000 simulation repetitions per scenario.

This produced 60 scenarios comprising 120,000 simulated hypothesis tests.

For nonzero effects, power was estimated as:

$$
\widehat{\mathrm{Power}}=
\frac{\text{Number of rejected null hypotheses}}
{\text{Number of simulated experiments}}
$$

When the true effect was zero, the rejection proportion estimated the Type I error rate.

An illustrative scenario with 10 independent specimens per group, a true effect of 100 ppm, and baseline noise yielded approximately **25.1% power**.

The simulations indicate that power generally increases with sample size and effect magnitude and decreases with increasing within-group variability.

These are hypothetical design calculations rather than new geological experiments.

## 6. Assumption-Violating Counterexample

A synthetic experiment investigated the consequences of ignoring dependence among analytical spots within parent rocks.

Each synthetic dataset contained 20 independent parent rocks, with four pseudo-oolite and four pellet analytical spots per parent. The true grain-type difference was zero.

Shared parent effects with a standard deviation of 100 ppm and independent spot-level effects with a standard deviation of 50 ppm introduced positive within-parent dependence.

Two methods were compared:

1. A naive unpaired Welch analysis treating 160 analytical spots as independent.
2. A parent-aware paired analysis using grain-type differences within the 20 parent rocks.

Across 2,000 independent synthetic experiments, the naive approach produced a false-positive rate of **0.05%** and interval coverage of **99.95%**.

The parent-aware procedure produced a false-positive rate of **5.35%** and interval coverage of **94.65%**.

The methods disagreed on statistical significance in approximately **5.3%** of experiments.

In this balanced paired design, ignoring parent dependence produced overly conservative inference. Shared parent variation cancelled when within-parent grain-type differences were analyzed.

The direction of miscalibration depends on the sampling design and correlation structure; independence violations do not invariably inflate false-positive rates.

## 7. Assumptions, Limitations, and Reproducibility

The principal limitations are nonrandom geological sampling, small sample sizes, heterogeneous lithology, possible stratigraphic dependence, repeated in situ measurements, and retrospective analysis choices.

Normality diagnostics provide limited assurance with small samples. Neither Welch inference nor bootstrap resampling automatically corrects geological selection bias.

All synthetic observations were generated exclusively for statistical demonstrations and are not presented as collected geological data.

The notebook uses fixed random seeds, retains the original supplementary Excel source, records software dependencies, and preserves numerical simulation results in CSV files.

The manual Welch interval was checked against SciPy. CSV outputs were independently reloaded and checked against the in-memory results, and the notebook was executed from a restarted kernel.

These checks verify aspects of implementation and reproducibility but do not establish that every statistical or geological modeling assumption is correct.

## 8. Methodological Conclusion

The investigation demonstrates that uncertainty quantification can materially change how geochemical differences are interpreted.

Study A shows an initially positive bulk-rock REY difference that is strongly sensitive to lithological composition. Study B indicates a positive grain-type-associated REY contrast under a parent-aware resampling framework.

The counterexample demonstrates that ignoring the geological measurement hierarchy can distort inference, even when a computational procedure produces apparently valid confidence intervals and p-values.

These results support cautious, assumption-aware interpretation rather than claims of causation or unrestricted generalization.