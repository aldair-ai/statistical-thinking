# Class 08 — Multiple Testing

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

---

## 📖 Theory Summary

### The Core Problem

A single hypothesis test at level $\alpha$ gives:

$$P(\text{false rejection} \mid H_0) = \alpha$$

Test $m$ hypotheses simultaneously and, under the **complete null** (all $H_0$ true):

$$E[\text{# false rejections}] = m\alpha$$

With $\alpha = 0.05$ and $m = 10{,}000$ tests (e.g. a genomics study), you expect **500 false positives by pure chance**. This is the multiple testing problem.

---

## 📐 Error Criteria

### Family-Wise Error Rate (FWER)

The probability of making **at least one** false positive across all tests:

$$\text{FWER} = P_{H_0}[\text{at least one false rejection}]$$

Under the complete null with **independent** tests:

$$\text{FWER} = 1 - P_{H_0}[\text{no false rejections}] = 1 - (1-\alpha)^m$$

This grows rapidly — at $m = 14$, FWER already exceeds 50%.

**First-order approximation** (when $\alpha$ is small):

$$\text{FWER} \approx 1 - (1 - m\alpha) = m\alpha$$

### Bonferroni Correction

For **dependent** tests we can't use the independence formula. Instead, the union bound gives:

$$\text{FWER} = P_{H_0}\left[\bigcup_{k=1}^m \text{reject } H_{0k}\right] \leq \sum_{k=1}^m P_{H_0}[\text{reject } H_{0k}] = m\alpha$$

**Key result:** Control FWER at target level $\alpha^*$ by using per-test threshold:

$$\alpha = \frac{\alpha^*}{m}$$

This is the **Bonferroni correction** — valid for any dependence structure and any $\alpha$.

**Trade-off:** Bonferroni is conservative (it's an upper bound). With many truly non-null hypotheses and high correlation, it loses power severely.

---

## 📊 Distribution of P-values

P-values are random variables — their distribution changes fundamentally depending on whether $H_0$ is true.

### Under the Null

**Theorem:** If $F_0$ is continuous and monotone increasing, then under $H_0$ the p-value $P \sim \text{Uniform}(0,1)$.

**Proof:**

$$P_{H_0}[P \leq p] = P_{H_0}[1 - F_0(T^*) \leq p]$$
$$= P_{H_0}[T^* \geq F_0^{-1}(1-p)]$$
$$= 1 - F_0[F_0^{-1}(1-p)] = p$$

This is why under the complete null, a histogram of p-values should look flat/uniform. Any spike away from uniformity is a signal.

### Under the Alternative

For a one-sided Z-test with $F_0(z) = \Phi(z)$ and true effect size $\theta$:

$$P_{H_A}[P \leq p] = 1 - \Phi[\Phi^{-1}(1-p) - \theta]$$

This distribution is **stochastically smaller** than Uniform(0,1) — p-values pile up near 0 when there's a real effect. Larger $\theta$ = more extreme leftward skew.

**Practical implication:** The shape of a p-value histogram from a multiple testing study is a diagnostic tool:
- Flat → mostly nulls, no signal
- Spike near 0 + flat elsewhere → mixture of nulls and true effects
- Spike near 0 + elevated everywhere → inflation (calibration problem)

---

## 🔢 Benford's Law (bonus)

The last slide introduces Benford's Law as a related application of distributional reasoning. In naturally occurring numerical data, the leading digit $d$ follows:

$$P(d) = \log_{10}\left(1 + \frac{1}{d}\right)$$

| Digit | Expected % |
|-------|-----------|
| 1 | 30.1% |
| 2 | 17.6% |
| 3 | 12.5% |
| 4 | 9.7% |
| 5 | 7.9% |
| 6 | 6.7% |
| 7 | 5.8% |
| 8 | 5.1% |
| 9 | 4.6% |

Used in forensic statistics and fraud detection — fabricated data tends to deviate from this law because people don't intuitively generate Benford-distributed leading digits.

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Expected false positives under the complete null
2. FWER growth curve — exact and approximation
3. Bonferroni correction — implementation and power cost
4. P-value distributions under $H_0$ and $H_A$ — proof by simulation
5. P-value histogram diagnostics (flat vs. spiked vs. inflated)
6. Benford's Law — verification on real financial data

---

## 📚 References

- Schwartzman, A. DSC 215 Lecture Notes, UCSD Spring 2026.
- Benjamini, Y. & Hochberg, Y. (1995). *Controlling the false discovery rate.* JRSS-B 57(1): 289–300.
- Bland, J.M. & Altman, D.G. (1995). *Multiple significance tests: the Bonferroni method.* BMJ 310: 170.
