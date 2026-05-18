# Class 07 — Meta-Analysis and Publication Bias

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

*Based on lecture slides by Armin Schwartzman, DSC 215 — Spring 2026*

---

## 📖 Theory Summary

### The Core Problem

When multiple independent research groups study the same phenomenon, their estimates disagree — due to sampling variability, different sample sizes, and different methodologies. How should we combine them into a single, principled estimate? And what happens when the studies we observe are not a representative sample of all studies that were run?

---

## 📐 Meta-Analysis: Combining Several Studies

### Setup

Suppose $J$ studies are conducted by different research groups, each trying to estimate an effect $\mu$. Study $j$ collects data with sample size $n_j$ and produces an estimate $\hat{\mu}_j$ with standard error $\hat{\sigma}_j / \sqrt{n_j}$.

### Why Not Just Average?

A simple average treats all studies equally:

$$\hat{\mu} = \frac{1}{J} \sum_{j=1}^{J} \hat{\mu}_j$$

This is wrong. A study with $n = 10$ should not carry the same weight as a study with $n = 10{,}000$.

### The Correct Approach: Weighted Average

Larger studies give more accurate estimates, so the pooled estimate should weight each study inversely proportional to its variance:

$$\hat{\mu} = \frac{\displaystyle\sum_{j=1}^{J} \hat{\mu}_j \cdot n_j/\hat{\sigma}_j^2}{\displaystyle\sum_{j=1}^{J} n_j/\hat{\sigma}_j^2}$$

This is the **inverse-variance weighted** estimator. It is the minimum-variance unbiased linear combination of the study estimates — the BLUE (Best Linear Unbiased Estimator) under the model below.

---

## 🔬 A Simple Model

Assume sample sizes are large enough for the CLT to apply, so estimates are approximately normal:

$$\hat{\mu}_j \sim N\!\left(\mu,\, \frac{\sigma_j^2}{n_j}\right), \qquad j = 1, \ldots, J$$

For simplicity, assume $\sigma_j = 1$ for all $j$:

$$\hat{\mu}_j \sim N\!\left(\mu,\, \frac{1}{n_j}\right), \qquad j = 1, \ldots, J$$

For the distribution of sample sizes, assume an **exponential model**:

$$n \sim \text{Exp}(\lambda) \qquad \Leftrightarrow \qquad \log\!\left(\frac{n}{\lambda}\right) \sim \text{Unif}(0, 1)$$

This means sample sizes are log-uniformly distributed — spanning several orders of magnitude, which is realistic for a literature of independent studies.

---

## 📊 The Funnel Plot

The **funnel plot** is the standard visualization for a set of studies in a meta-analysis. It graphs:

- **Horizontal axis:** effect estimate $\hat{\mu}_j$
- **Vertical axis:** sample size $n_j$ (larger samples → top of plot)

### Funnel Boundary Lines

The boundary lines are placed at 2 standard errors away from the true $\mu$:

$$b = \mu \pm \frac{2}{\sqrt{n}}$$

Inverting to express $n$ as a function of the boundary location $b$:

$$n = \left(\frac{2}{|b - \mu|}\right)^2$$

Taking the log (since $n$ is log-uniformly distributed under the model):

$$n = 2 \log\!\left(\frac{2}{|b - \mu|}\right)$$

This gives the characteristic **funnel shape**: studies scatter within a wide band at the bottom (small $n$, high variability) and converge tightly near the true effect at the top (large $n$, low variability).

### Interpreting the Funnel Plot

| Pattern | Interpretation |
|---------|---------------|
| Symmetric funnel | No evidence of publication bias |
| Asymmetric (missing lower-left) | Small studies with null/small effects suppressed — publication bias |
| Missing lower-right | Unlikely; would suggest negative publication bias |
| Outliers far outside funnel | Possible heterogeneity or errors |

---

## 🔧 Publication Bias in the Funnel Plot

Under **publication bias**, small studies with small or null effects are never published. In the funnel plot, this removes the lower-left region of the scatter — creating a visually asymmetric funnel.

Consequence: the apparent weighted average across published studies is pulled away from the true $\mu$ toward larger effect sizes. The literature overestimates the true effect.

**Egger's test** formally tests for funnel plot asymmetry by regressing the standardized effect size on precision.

---

## 📋 Corollaries

| Condition | Effect on Meta-Analysis |
|-----------|------------------------|
| All studies published (no bias) | Weighted average converges to true $\mu$ |
| Small studies with null results suppressed | Pooled estimate inflated |
| Heterogeneous true effects across studies | Random-effects meta-analysis needed |
| Only large studies available | Precise estimate but limited generalizability |

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Why simple averaging fails — variance of the unweighted vs. weighted estimator
2. The inverse-variance weighted estimator — derivation and simulation
3. The simple model — exponential sample sizes, normal estimates
4. The funnel plot — deriving the boundary lines from the model
5. Publication bias in the funnel plot — simulated vs. unbiased literature
6. Egger's test — formal test of funnel plot asymmetry
7. Summary table

---

## 📚 References

- Schwartzman, A. (2026). *DSC 215 Lecture Slides: Meta-Analysis and Publication Bias.* UCSD.
- Egger, M., Davey Smith, G., Schneider, M., & Minder, C. (1997). *Bias in meta-analysis detected by a simple, graphical test.* BMJ 315: 629–634.
- Borenstein, M., Hedges, L.V., Higgins, J.P.T., & Rothstein, H.R. (2009). *Introduction to Meta-Analysis.* Wiley.
