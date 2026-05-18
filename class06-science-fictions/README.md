# Class 06 — Bias, Multiple Testing & P-Hacking

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

*Based on Ritchie (2020), Science Fictions: Chapter 4*

---

## 📖 Theory Summary

### The Core Problem

Science has two distinct failure modes covered in this class:

> **Part 1 (Bias):** Structural forces — publication pressure, confirmation bias, underpowered studies — cause the literature to systematically overstate effects even without any deliberate fraud.

> **Part 2 (Multiple Testing & P-Hacking):** Deliberate or accidental misuse of significance testing inflates false positive rates far beyond the nominal α = 0.05.

Both failure modes produce the same outcome: published findings that don't replicate.

---

## 📐 Part 1 — Bias

### Sample Size and the Standard Error

The **Scottish height example** anchors the discussion: testing whether Scottish men are taller than Scottish women. The standard error of the difference in means is:

$$\text{SE} = \sigma\sqrt{\frac{2}{n}}$$

As $n$ grows, SE shrinks as $1/\sqrt{n}$ — making even a tiny true difference detectable. The **sample-size conflict**: cost grows linearly with $n$, but precision improves much more slowly. To halve the SE you need 4× more data.

| n | SE (cm) | p-value |
|---|---------|---------|
| 10 | 3.13 | 0.0001 |
| 100 | 0.99 | < 0.0001 |
| 1000 | 0.31 | < 0.0001 |

### Publication Bias

**Publication bias**: journals prefer significant positive findings. Studies with null or small effects stay in the file drawer. Consequence: the published literature systematically overestimates true effect sizes.

The **funnel plot** diagnoses this: plot each study's effect size against its standard error. Under no bias, studies scatter symmetrically in a funnel shape. Asymmetry — missing studies in the lower-left — is the signature of publication bias.

### Confirmation Bias

**Confirmation bias** is the tendency to obtain results consistent with prior expectations. Occurs when:
- Financial incentives push for a positive result (prove the drug works)
- Ego incentives push for a positive result (prove my idea is correct)
- Analytic flexibility (researcher degrees of freedom) allows many paths to p < 0.05

Key statistical fact: under H₀, p-values are **Uniform(0,1)**. Exactly 5% fall below 0.05 by chance. A researcher who keeps reanalyzing until p < 0.05 exploits this directly.

### Meta-Analysis

**Definition:** A statistical technique combining results from multiple independent studies addressing the same research question.

**Why it works:**
- **Increased power**: pooling $k$ studies of $n$ is roughly equivalent to one study of $k \times n$
- **Generalizability**: consistency across labs and populations increases confidence
- **Signal in noise**: meta-analysis resolves contradictory individual studies

**Standard method:** inverse-variance weighted pooled estimate. Each study gets weight $w_i = 1/\text{SE}_i^2$ — larger, more precise studies count more.

$$\hat{\mu}_{\text{pooled}} = \frac{\sum w_i \hat{\mu}_i}{\sum w_i}, \qquad \text{SE}_{\text{pooled}} = \frac{1}{\sqrt{\sum w_i}}$$

---

## 🔬 Part 2 — Multiple Testing & P-Hacking

### The Multiple Testing Problem

When $m$ independent hypotheses are each tested at level $\alpha$, the **Family-Wise Error Rate (FWER)** — probability of at least one false positive — grows rapidly:

$$\text{FWER} = 1 - (1-\alpha)^m$$

The expected number of false positives is $m \times \alpha$. This is the **jelly bean problem** from the slides: test 20 jelly bean colors for acne at α = 0.05, and you expect exactly 1 false positive even if none cause acne.

| m (tests) | FWER | Expected false positives |
|-----------|------|-------------------------|
| 1 | 5% | 0.05 |
| 10 | 40% | 0.5 |
| 20 | 64% | 1.0 |
| 100 | 99% | 5.0 |

### P-Hacking

**P-hacking:** manipulating analysis choices until p < 0.05 is achieved.

Common tactics:
- **Selective reporting** — only report outcomes that are significant
- **Optional stopping** — continue data collection until significance is reached
- **Outlier removal** — selectively remove data points that hurt the p-value
- **Covariate adjustment** — add or remove covariates until p < 0.05
- **Data dredging** — search large datasets for any significant correlation

P-hacking can be unintentional (researcher degrees of freedom) or constitute outright fraud.

### P-HARKing

**P-HARKing = Hypothesizing After the Results are Known.**

The researcher:
1. Collects data and finds a surprising pattern
2. Formulates a hypothesis that "predicts" that pattern
3. Presents it as if the hypothesis was pre-specified

This is always fraud because:
- Data is used twice — once to discover, once to confirm — invalidating the test
- It misrepresents the scientific process to readers and reviewers
- It is mathematically equivalent to overfitting in machine learning

| | P-Hacking | P-HARKing |
|--|-----------|-----------|
| What is manipulated? | The data or analysis | The hypothesis |
| Intent | Get p < 0.05 | Make result look confirmatory |
| Always fraudulent? | Not always | Yes |

### Multiple Testing Corrections

Two standard approaches:

| Method | Rule | Controls |
|--------|------|---------|
| **Bonferroni** | Reject if $p_i < \alpha / m$ | FWER — at most one false positive on average |
| **Benjamini-Hochberg (BH)** | Reject if $p_{(i)} \leq \frac{i}{m}\alpha$ | FDR — controlled proportion of false positives among rejections |

Bonferroni is conservative but guarantees strong FWER control. BH is more powerful when many tests are run and some true effects exist.

---

## 🔎 Detecting Fabricated Data

### Statistical Red Flags

| Test | What genuine data shows | Red flag |
|------|------------------------|---------|
| **Variance** | Natural variability | Suspiciously low variance, too-round numbers |
| **Last digits** | Uniformly distributed (0–9) | Excess zeros (rounding) |
| **First digits** | Follow Benford's Law | Deviates from log distribution |
| **Metadata** | Consistent timestamps, raw data available | Inconsistencies, data unavailable |
| **Publication pattern** | Mixed journals | Many papers in low-quality journals |

### Benford's Law

In many naturally occurring datasets spanning several orders of magnitude, the leading digit $d$ follows:

$$P(d) = \log_{10}\!\left(1 + \frac{1}{d}\right), \quad d \in \{1, \ldots, 9\}$$

Digit 1 appears ~30% of the time; digit 9 only ~5%. This is **scale-invariant** — it holds regardless of units (meters, feet, dollars, yen).

**Applies to:** country populations, stock prices, river lengths, physical constants, financial transactions.

**Does NOT apply to:** Gaussian data, data confined to a narrow range.

**Historical use:**
- Proposed by Hal Varian for fraud detection
- Applied (correctly) to the **2009 Iranian elections**
- Misapplied to **2020 US elections** — precinct vote counts are in a narrow range and do not follow Benford's Law

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Sample size and SE — the Scottish height example with sampling distributions
2. Publication bias — simulated funnel plots, biased vs. unbiased
3. Confirmation bias — p-value distribution under H₀
4. Meta-analysis — forest plot with inverse-variance weighting
5. Family-Wise Error Rate — FWER formula and the jelly bean scenario
6. P-hacking via data dredging — 30 independent predictors, all false positives
7. Multiple testing corrections — Bonferroni and BH side by side
8. Benford's Law — real vs. fabricated first-digit distributions with chi-squared tests
9. Last-digit analysis — detecting rounding and fabrication
10. Summary corollaries table

---

## 📋 Corollaries — When Are Findings Least Trustworthy?

| Condition | Why It Matters |
|-----------|---------------|
| Small sample size | Low power — misses real effects; inflates effect estimates of what is found |
| Many tests, no correction | FWER explodes — one significant result proves nothing |
| Exploratory analysis presented as confirmatory | P-HARKing — invalidates the test |
| Financial or ego incentives | Raises bias; pushes toward positive results |
| "Hot" or fashionable field | High researcher degrees of freedom; many unregistered analyses |
| Low-quality journals | Less rigorous review; higher tolerance for p-just-below-0.05 |

---

## 📚 References

- Ritchie, S. (2020). *Science Fictions: How Fraud, Bias, Negligence, and Hype Undermine the Search for Truth.* Metropolitan Books. Chapter 4.
- Simmons, J.P., Nelson, L.D., & Simonsohn, U. (2011). *False-positive psychology: Undisclosed flexibility in data collection and analysis allows presenting anything as significant.* Psychological Science 22(11): 1359–1366.
- Varian, H.R. (1972). *Benford's Law.* The American Statistician 26(3): 65–66.
- Benjamini, Y. & Hochberg, Y. (1995). *Controlling the false discovery rate: a practical and powerful approach to multiple testing.* Journal of the Royal Statistical Society B 57(1): 289–300.
