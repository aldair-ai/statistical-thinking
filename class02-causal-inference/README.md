# Class 02 — Introduction to Causal Inference

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

*Based on the Rubin Causal Model (Potential Outcomes Framework)*

---

## 📖 Theory Summary

### The Fundamental Problem of Causal Inference

For every individual $i$ in a population of size $n$, define two **potential outcomes**:

- $Y_i(1)$: outcome if individual $i$ receives treatment ($T_i = 1$)
- $Y_i(0)$: outcome if individual $i$ receives control ($T_i = 0$)

The **Individual Treatment Effect** is:

$$\tau_i = Y_i(1) - Y_i(0)$$

**The fundamental problem:** only one of $Y_i(1)$ or $Y_i(0)$ is ever observed. The unobserved one is the **counterfactual** — what would have happened under the other condition. This is not a data collection problem; it is logically impossible to observe both.

### What We Can Estimate: The ATE

Because individual effects are unidentifiable, we target the **Average Treatment Effect**:

$$\text{ATE} = E[\tau_i] = E[Y_i(1) - Y_i(0)] = E[Y_i(1)] - E[Y_i(0)]$$

This requires estimating the *population average* under each condition — not the individual effects.

---

## ⚠️ The Flawed Reasoning — Why Observational Data Fails

We observe $Y_i = T_i Y_i(1) + (1 - T_i) Y_i(0)$. It is tempting to argue:

$$E[Y_i \mid T_i = 1] - E[Y_i \mid T_i = 0] = E[Y_i(1)] - E[Y_i(0)] = \text{ATE}$$

The proof seems to work:

$$E[Y_i \mid T_i = 1] = E[Y_i(1) \mid T_i = 1]$$

But the critical step is wrong:

$$E[Y_i(1) \mid T_i = 1] \neq E[Y_i(1)]$$

**Why?** Treatment assignment often depends on potential outcomes:
- People with poor health (high risk) are more likely to seek treatment ($T_i = 1$)
- People feeling healthy (low risk) stay in the control group ($T_i = 0$)

The treated group is not a random sample of the population — it's a selected sample. Their average $Y_i(1)$ is not the population average $E[Y_i(1)]$.

---

## 🍊 The Vitamin C Example

The slides show a concrete case where **selection bias creates a spurious 100% apparent effect** when the true causal effect is zero.

| T | Y | Y(0) | Y(1) |
|---|---|------|------|
| 0 | 0 | 0 | 0* |
| 0 | 0 | 0 | 0* |
| 0 | 0 | 0 | 0* |
| 0 | 0 | 0 | 0* |
| 1 | 1 | *1 | 1 |
| 1 | 1 | *1 | 1 |
| 1 | 1 | *1 | 1 |
| 1 | 1 | *1 | 1 |

*Starred values are unobserved counterfactuals.*

**Observed:** $E[Y \mid T=1] - E[Y \mid T=0] = 1 - 0 = 1$

**True ATE:** $E[Y(1)] - E[Y(0)] = 0.5 - 0.5 = 0$

The sick people took vitamin C; the healthy people didn't. Vitamin C has zero effect — but observing it non-experimentally gives a massive apparent effect.

---

## 🎲 The Role of Randomization

In an RCT, treatment assignment $T_i$ is determined by a random mechanism (coin flip), giving the **randomization assumption**:

$$T_i \perp (Y_i(1), Y_i(0), X_i)$$

This independence has two critical consequences:

**1. Covariate balance:**
$$P(X_i \mid T_i = 1) = P(X_i \mid T_i = 0)$$
The distribution of every baseline characteristic is the same in both groups.

**2. Unconfounded potential outcomes:**
$$E[Y_i(1) \mid T_i = 1] = E[Y_i(1)]$$
$$E[Y_i(0) \mid T_i = 0] = E[Y_i(0)]$$

The step that was wrong before is now valid. The proof goes through:

$$E[Y_i \mid T_i = 1] - E[Y_i \mid T_i = 0] = E[Y_i(1)] - E[Y_i(0)] = \text{ATE}$$

### Why Covariates Cancel Out

Expanding the treatment group expectation:

$$E[Y_i \mid T_i = 1] = \int E[Y_i \mid T_i=1, X_i=x] \cdot P(X_i=x \mid T_i=1)\, dx$$

Under randomization, $P(X_i = x \mid T_i = 1) = P(X_i = x)$, so:

$$= \int E[Y_i(1) \mid X_i = x] \cdot P(X_i = x)\, dx = E[Y_i(1)]$$

The covariates are **averaged out** regardless of their distribution. No matter how many confounders exist, randomization neutralizes all of them simultaneously — including ones you haven't measured or don't know about.

---

## 📋 Why Randomization Works — Two Mechanisms

| Mechanism | Effect |
|-----------|--------|
| $T_i \perp X_i$ | Every covariate has the same distribution in both groups — confounders cancel |
| Counterfactual substitution | Can't observe both $Y_i(1)$ and $Y_i(0)$ for any individual, but randomization produces comparable independent samples under each condition |

---

## 🔗 Relation to Distribution Shift (Class 10)

The selection bias mechanism in observational studies is precisely the MNAR case from the distribution shift lecture: whether someone ends up in the treatment group ($s=1$) depends on their potential outcome $Y_i$, which is the MNAR condition $P(s=1 \mid x, y) = P(s=1 \mid y)$. Randomization is the design-based fix; propensity score methods are the post-hoc fix for observational data.

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. The fundamental problem — simulation showing unobservable counterfactuals
2. Selection bias — replicating the vitamin C example numerically
3. Randomization — showing how it produces covariate balance
4. ATE estimation from an RCT vs. naive observational estimate
5. Confounding bias decomposition — what goes wrong without randomization
6. Sensitivity analysis — how much hidden confounding would overturn a result

---

## 📚 References

- Schwartzman, A. DSC 215 Lecture Notes, UCSD Spring 2026.
- Rubin, D.B. (1974). *Estimating causal effects of treatments in randomized and nonrandomized studies.* Journal of Educational Psychology 66(5): 688–701.
- Holland, P.W. (1986). *Statistics and causal inference.* JASA 81(396): 945–960.
- Imbens, G.W. & Rubin, D.B. (2015). *Causal Inference for Statistics, Social, and Biomedical Sciences.* Cambridge University Press.
