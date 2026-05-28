# Week 11 — Frequentist vs. Bayesian Duality

**DSC 215 · Statistical Critical Thinking & Experimental Design**

---

## 📖 Theory Summary

### The Core Duality

Every statistical concept has **two valid interpretations** depending on what you mean by "probability":

| School | Also Called | Core Claim |
|--------|------------|------------|
| **Frequentist** | Aleatory | Probability = long-run frequency of repeatable events |
| **Bayesian** | Epistemic | Probability = a rational agent's degree of belief |

Both frameworks satisfy the **same axioms** (Kolmogorov):
- $P(A) \geq 0$, $P(S) = 1$
- $P(A \cup B) = P(A) + P(B)$ if $A \cap B = \emptyset$

They disagree not on the math, but on what the symbols *mean*.

---

## 🗺️ Taxonomy of Statistical Concepts

The same quantities carry different interpretations depending on your framework:

| Concept | Definition | Interpretation |
|---------|-----------|----------------|
| **P-value** | $P(Z > z \mid H_0)$ | Frequentist |
| **Confidence** | $P(\text{CI}(X) \ni \theta)$ | Frequentist |
| **Bias** | $E[\hat\theta] - \theta$ | Frequentist |
| **Standard error** | $\sqrt{\text{Var}(\hat\theta)}$ | Frequentist |
| **Sensitivity** | $P(Z > z \mid H_A)$ | Frequentist |
| **Specificity** | $1 - P(Z > z \mid H_0)$ | Frequentist |
| **Positive predictive value** | $P(H_A \mid Z > z)$ | Bayesian |
| **False discovery rate** | $P(H_0 \mid Z > z)$ | Bayesian |

The critical split: **p-values and confidence levels condition on hypotheses** (frequentist), while **PPV and FDR condition on the data** (Bayesian).

---

## 🔍 Deep Dives

### 1. The Sun Exploded (xkcd)

A neutrino detector checks whether the sun has gone nova. It rolls two dice: if both show six it lies; otherwise it tells the truth. The detector says "YES."

**Frequentist answer:**  
Under $H_0$ (sun intact), the probability of the detector saying YES is $\frac{1}{36} \approx 0.028 < 0.05$. Reject $H_0$.

**Bayesian answer:**  
Let $H_A$ = sun exploded. Using Bayes' theorem:

$$P(H_A \mid \text{YES}) = \frac{\frac{1}{36} \times P(\text{sun exploded})}{\frac{1}{36} \times P(\text{sun exploded}) + \frac{35}{36} \times P(\text{sun intact})}$$

With a tiny prior on solar explosion ($P(H_A) \approx 10^{-5}$):

$$P(H_A \mid \text{YES}) \approx 0.028\% \times 100 = \text{still nearly zero}$$

**Lesson:** The frequentist p-value ignores the prior plausibility of the hypothesis. The Bayesian posterior does not.

### 2. Pascal & Fermat's Interrupted Game (1654)

Two players each ante \$0.50. They flip a fair coin repeatedly until one side reaches 10 wins. If the game is interrupted, **how should the pot be split fairly?**

**Solution:** Give each player their *expected winnings* from the current game state. If heads needs $h$ more wins and tails needs $t$ more wins, the probability that heads wins is:

$$P(\text{heads wins}) = \sum_{k=0}^{t-1} \binom{h+t-1}{k} \left(\frac{1}{2}\right)^{h+t-1}$$

This is a **frequentist** argument: the split is fair because over infinitely many such interruptions, each player receives the right long-run average.

### 3. Leibniz's Legal Problem (1657)

A judge decides whether to grant bail. Leibniz proposed quantifying this as $P(\text{violent act} \mid \text{history})$.

**The frequentist challenge:** What population do you repeat the bail decision over? The accused is a specific individual with a specific history.

**The Bayesian answer:** Probability quantifies the judge's *rational belief*, updated from prior experience to the specific evidence at hand — prior → evidence → posterior.

### 4. Bayesian Updating

The Bayesian cycle:

1. **Prior** $P(\theta)$ — what you believe before seeing data
2. **Likelihood** $P(X \mid \theta)$ — how well $\theta$ explains the data
3. **Posterior** $P(\theta \mid X) \propto P(X \mid \theta) \cdot P(\theta)$ — updated belief

The posterior from one experiment becomes the prior for the next. This formalizes *learning*.

---

## ⚖️ Criticisms & Tensions

### Against Frequentism
- Frequency limits are mathematical ideals — no experiment is truly infinite or exactly repeatable
- P-values are notoriously hard to understand and routinely misinterpreted
- Cannot assign probabilities to one-off events (a specific election, an individual patient's outcome)

### Against Bayesianism
- Priors are subjective — different analysts, different answers
- Computing the posterior is often intractable
- Choosing a "non-informative" prior is itself a subtle judgment

### A Middle View (Schwartzman)
- Frequentist limits are approximations — chaotic, ergodic systems behave as if they had stable long-run frequencies
- Bayesian beliefs are ultimately *grounded in* observed frequencies — we form priors by extrapolating from prior data
- The two frameworks are complementary lenses, not competing religions

---

## 🔖 Nomenclature

Newton separated *mass* (inherent) from *weight* (measurable). We lack an equally clean vocabulary for probability:

| Term | Meaning |
|------|---------|
| **Propensity** | Inherent tendency of a random system |
| **Chance** | Long-run frequency |
| **Credence** | Degree of rational belief |

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Numerically reproducing the "sun exploded" Bayesian calculation
2. Simulating Pascal & Fermat's interrupted game to verify fair-split probabilities
3. Visualizing Bayesian updating as new coin-flip data arrives
4. Classifying the standard statistical concepts as frequentist or Bayesian
5. A sensitivity analysis: how different priors change the posterior conclusion

---

## 📚 References

- Hacking, I. (1975). *The Emergence of Probability.* Cambridge University Press.
- Jaynes, E.T. (2003). *Probability Theory: The Logic of Science.* Cambridge University Press.
- Efron, B. (2013). *A 250-year argument: Belief, behavior, and the bootstrap.* Bulletin of the American Mathematical Society.
- Wasserstein, R.L. & Lazar, N.A. (2016). *The ASA statement on p-values: Context, process, and purpose.* The American Statistician.
