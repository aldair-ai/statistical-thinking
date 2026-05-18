# Class 04 — P-values and Confidence Intervals

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

---

## 📖 Theory Summary

### What Is a P-value?

The **p-value** is the probability, under the null hypothesis $H_0$, of observing a test statistic at least as extreme as the one actually observed:

$$p\text{-value} = P_{H_0}[|Z| \geq z_\text{obs}]$$

It is a **tail probability** under $H_0$ — nothing more. It says nothing about the probability that $H_0$ is true.

---

## 📐 From Maximum Likelihood to Testing

The slides derive the p-value by contrasting two related concepts:

### Maximum Likelihood
Uses the **probability density** at the observed value. Picks the model $\theta$ that makes the data most probable:

$$\hat{\theta} = \arg\max_\theta \phi(z - \theta)$$

For $Z \sim N(\theta, 1)$ with $z = 1.5$:

| Model | Density $\phi(z-\theta)$ |
|-------|--------------------------|
| $\theta = -1$ | 0.02 |
| $\theta = 0$ | 0.13 |
| $\theta = 1$ | 0.35 ← MLE |

### Hypothesis Testing
Uses the **tail probability** under each model. Rejects models that make the observed value look too extreme:

| Model | $P_\theta[Z \geq 1.5]$ |
|-------|------------------------|
| $\theta = -1$ | 0.01 ← rejected |
| $\theta = 0$ | 0.07 |
| $\theta = 1$ | 0.31 |

### The P-value (Composite Null)
When $H_A: \theta \neq 0$ (composite — $\theta$ unspecified), we can only evaluate under $H_0$:

$$p = P_{\theta=0}[|Z| \geq 1.5] = 2(1 - \Phi(1.5)) = 0.13$$

**Key distinction:** MLE picks the *best* model; testing *rejects* the *worst* ones.

---

## ⚠️ Common Misinterpretations

### Misinterpretation #1 — "P-value = P(H₀ is true)"
**Wrong.** This would require a **Bayesian prior** $\pi_0 = P[H_0]$. The correct Bayesian statement is:

$$P[H_0 \mid |Z| \geq z] = \frac{\pi_0 \cdot p\text{-value}}{P[|Z| \geq z]}$$

This is the **false discovery rate** — identical to what Ioannidis (Class 09) analyzed. The p-value alone doesn't tell you this.

### Misinterpretation #4 — "p > 0.05 means H₀ is true"
**Wrong in composite tests.** A non-significant result just means the data are consistent with $H_0$. But they're also consistent with many nearby alternatives. For $z = 1.5$:

$$P_{\theta=-0.1}[|Z| \geq 1.5] = 0.11, \quad P_{\theta=0}[|Z| \geq 1.5] = 0.13, \quad P_{\theta=0.1}[|Z| \geq 1.5] = 0.16$$

All three models are compatible with the data — failing to reject $\theta=0$ doesn't mean $\theta=0$.

### Misinterpretation #7 — "Significant = important"
**Wrong.** With large $n$, even a trivially small effect becomes significant. For a test of proportions:

$$\theta = \frac{\sqrt{n}(p_1 - p_2)}{\sqrt{p_1(1-p_1) + p_2(1-p_2)}}$$

As $n \to \infty$, $\theta \to \infty$ for any fixed $p_1 \neq p_2$, no matter how tiny the difference. Statistical significance is mostly a function of sample size; practical importance must be evaluated separately using **effect sizes**.

### Misinterpretation #13 — "Statistical significance is a property of the phenomenon"
**Wrong.** Significance is a property of the test, the data, and the sample size — not of reality. Writing "X is a statistically significant predictor" is bad practice. Writing "X is an important predictor" is better — it separates the statistical machinery from the substantive question.

---

## 📏 Confidence Intervals

### Definition and Duality with P-values

For $Z \sim N(\theta, 1)$ with MLE $\hat{\theta} = z$, a $1-\alpha$ CI is:

$$\text{CI} = [\hat{\theta} - z_\alpha, \hat{\theta} + z_\alpha]$$

**Duality:** The CI excludes $\theta_0$ iff the p-value for $H_0: \theta = \theta_0$ is less than $\alpha$.

### Misinterpretation #19 — "A 95% CI has a 95% chance of containing θ"
**Wrong.** Once computed, the interval either contains $\theta$ or it doesn't — probability is 0 or 1. The 95% refers to the **procedure**: if repeated many times, 95% of such intervals will contain the true value. $\theta$ is fixed; the interval is random.

### Misinterpretation #20 — "Values outside the CI are excluded"
**Wrong.** A CI is not a hard boundary. Values just outside have p-values slightly above $\alpha$ — they are marginally consistent with the data, not definitively excluded.

### Misinterpretation #21 — "Overlapping CIs means no significant difference"
**Wrong.** The CI for a *difference* $\theta_1 - \theta_2$ is not the same as comparing two individual CIs. For independent estimates, the CI for the difference is $1/\sqrt{2} \approx 0.7$ times the sum of the two individual CI lengths — meaning two CIs can overlap substantially while the difference is still significant.

---

## 🤔 P-values vs. Confidence Intervals

Greenland (2016) argues CIs are preferable:

| Aspect | P-value | Confidence Interval |
|--------|---------|---------------------|
| Dichotomous decision | Tempts binary think | Encourages quantification |
| Effect size | Not shown | Shown explicitly |
| Uncertainty | Not shown | Shown as interval width |
| Sample size effect | Becomes extreme | Shows increasing precision |
| Multiple testing | Still a problem | Still a problem |

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. MLE vs. p-value — numerically reproducing the slide example
2. The p-value as a tail probability — visualization
3. Misinterpretation #1 — Bayesian posterior vs. p-value
4. Misinterpretation #4 — what non-significance does and doesn't mean
5. Misinterpretation #7 — sample size inflates significance, not importance
6. CI duality — geometric proof by simulation
7. Misinterpretation #21 — overlapping CIs trap

---

## 📚 References

- Schwartzman, A. DSC 215 Lecture Notes, UCSD Spring 2026.
- Greenland, S. et al. (2016). *Statistical tests, P values, confidence intervals, and power: a guide to misinterpretations.* European Journal of Epidemiology 31: 337–350.
- Wasserstein, R.L. & Lazar, N.A. (2016). *The ASA Statement on p-Values.* The American Statistician 70(2): 129–133.
