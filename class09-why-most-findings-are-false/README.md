# Class 09 — Why Most Research Findings Are False

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

*Based on Ioannidis (2005), PLOS Medicine — ~16,000 citations*

---

## 📖 Theory Summary

### The Core Insight

A p-value answers the wrong question for most researchers:

> **P-value:** P(finding | null is true) — probability of seeing data this extreme *if there's no effect*

> **What we actually want:** P(true effect | finding) — probability the finding is real *given we saw it*

These are not the same thing. The second quantity is the **Positive Predictive Value (PPV)**, and it depends critically on a prior probability that p-values completely ignore.

---

## 🔬 PPV: The Medical Diagnosis Analogy

The slides open with lung cancer screening as an anchor:

| Parameter | Value |
|-----------|-------|
| Prevalence (prior) | ~1% |
| Sensitivity P(+\|cancer) | 94% |
| Specificity P(−\|healthy) | 73% |
| False positive rate P(+\|healthy) | 27% |

**Question:** If the test is positive, what's the probability you have cancer?

$$\text{PPV} = P(\text{cancer} \mid +) = \frac{\text{Sensitivity} \times \text{Prevalence}}{\text{Sensitivity} \times \text{Prevalence} + (1-\text{Specificity}) \times (1-\text{Prevalence})}$$

$$= \frac{0.94 \times 0.01}{0.94 \times 0.01 + 0.27 \times 0.99} = \mathbf{3.4\%}$$

Despite a 94% sensitive test, a positive result only means 3.4% chance of cancer. This is the **base rate problem** — low prevalence drowns the signal.

---

## 📐 Mathematical Model for Research (Ioannidis)

Treat each research study as a hypothesis test with:

| Symbol | Meaning |
|--------|---------|
| $\alpha$ | Significance level (Type-I error rate) |
| $\gamma = 1 - \beta$ | Statistical power (1 − Type-II error rate) |
| $f$ | Prior probability that a true effect exists |
| $R = f/(1-f)$ | Pre-study odds of a true effect |

The probability of a **finding** (rejecting H₀) in each scenario:

$$P(\text{finding} \mid \text{no effect}) = \alpha \quad \text{(false positive)}$$
$$P(\text{finding} \mid \text{effect}) = \gamma \quad \text{(true positive)}$$

### PPV Formula

By Bayes' rule — identical structure to the medical diagnosis:

$$\text{PPV} = \frac{\gamma f}{\gamma f + \alpha(1-f)} = \frac{(1-\beta)R}{(1-\beta)R + \alpha}$$

**Notice:** this is exactly the medical formula with sensitivity = $\gamma$, prevalence = $f$, false positive rate = $\alpha$.

---

## 🔧 Three Factors That Destroy PPV

### 1. Low Prior $f$ (Exploratory Fields)

When most hypotheses tested are wrong (small $f$), the false positive pool dominates. Even at $\alpha = 0.05$, $\gamma = 0.8$:

- $f = 0.5$ → PPV = 89%
- $f = 0.1$ → PPV = 64%
- $f = 0.01$ → PPV = 14%
- $f = 0.001$ → PPV = 2%

**Implication:** Genome-wide association studies, exploratory neuroscience, nutrition epidemiology — fields with thousands of hypotheses and low $f$ — are especially vulnerable.

### 2. Low Power $\gamma$ (Small Samples, Small Effects)

Low power means true effects are missed *and* the ratio of false positives to true positives worsens. A study that's 80% powered is much more trustworthy than one at 20%.

### 3. Bias $u$ (P-hacking, Publication Bias)

Define $u$ as the fraction of non-significant results that get reported as significant anyway (p-hacking, selective reporting, HARKing):

$$P(\text{finding} \mid \text{no effect}) = \alpha + u(1-\alpha)$$
$$P(\text{finding} \mid \text{effect}) = \gamma + u(1-\gamma)$$

$$\text{PPV}_{\text{biased}} = \frac{(1-\beta+u\beta)R}{(1-\beta+u\beta)R + \alpha + u(1-\alpha)}$$

As $u \to 1$: every analysis gets reported as a finding regardless of truth → PPV collapses toward the prior $f$ alone.

---

## 🔁 Multiple Independent Teams

When $n$ teams independently test the same hypothesis:

$$\text{Type-I error} = 1 - (1-\alpha)^n \quad \text{(grows with } n\text{)}$$
$$\text{Type-II error} = \beta^n \quad \text{(shrinks with } n\text{)}$$

$$\text{PPV} = \frac{(1-\beta^n)R}{(1-\beta^n)R + 1-(1-\alpha)^n}$$

Counter-intuitive result: more teams actually *hurts* PPV because the Type-I error accumulates faster than power improves. The first team to get a positive result publishes; the ones that fail to replicate often don't.

---

## 📋 Corollaries — When Are Findings Least Trustworthy?

| Condition | Why PPV Drops |
|-----------|--------------|
| Small sample size | Low power $\gamma$ |
| Small true effect size | Low power $\gamma$ |
| Undisciplined study selection | Low prior $f$ |
| Non-rigorous analysis | High bias $u$ |
| Financial conflicts of interest | High bias $u$ |
| Exploratory/"hot" field | Low $f$, high $u$ |

---

## 🩺 Frequentist vs. Bayesian Framing

The slides make an important philosophical point:

**Frequentist:** decides based on the p-value alone — P(data | H₀). Ignores prior plausibility of H₀.

**Bayesian (PPV):** updates the prior probability of an effect after observing significance. Requires knowing $f$, which is uncomfortable but honest.

The PPV is literally a Bayesian update: prior odds $R$ → posterior odds $R \cdot (\gamma / \alpha)$ after a significant result.

---

## ⚖️ Reactions and Criticism

Jager & Leek (Biostatistics, 2014) pushed back empirically:
- Ioannidis' assumptions ($f$, $u$, $\gamma$) are "justifiable but arbitrary"
- Using actual p-value distributions from published literature, they estimated FDR ≈ 14%, not >50%
- Key lesson: Ioannidis' framework is directionally correct but quantitatively sensitive to assumed priors

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. PPV from scratch — replicating the lung cancer calculation
2. Interactive PPV surface as a function of $f$, $\gamma$, $\alpha$
3. Simulating publication bias via $u$
4. The multiple-teams paradox
5. Connecting PPV to the False Discovery Rate (FDR)
6. Real-world examples: genomics, nutrition, psychology replication crisis

---

## 📚 References

- Ioannidis, J.P.A. (2005). *Why Most Published Research Findings Are False.* PLOS Medicine 2(8): e124.
- Jager, L.R. & Leek, J.T. (2014). *An estimate of the science-wise false discovery rate and application to the top medical literature.* Biostatistics 15(1): 1–12.
