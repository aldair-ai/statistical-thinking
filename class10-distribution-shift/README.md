# Week 01 — Distribution Shift

**DSC 215 · Statistical Critical Thinking & Experimental Design**

---

## 📖 Theory Summary

### The Core Problem

Standard ML algorithms assume **i.i.d. data** — that training and test samples are drawn from the same joint distribution:

$$P_{tr}(x, y) = P_{tst}(x, y)$$

In deployment, this assumption breaks constantly. **Distribution shift** is the general term for any case where:

$$P_{tr}(x, y) \neq P_{tst}(x, y)$$

Causes include: changing environments, sampling bias, temporal drift, and adversarial actors.

---

## 🗺️ Taxonomy of Shift Types

The joint distribution $P(x,y)$ can be decomposed two ways depending on the **causal direction**:

| Direction | Decomposition | Example |
|-----------|--------------|---------|
| Causal $X \to Y$ | $P(x,y) = P(y\|x) \cdot P(x)$ | Lab measurements → disease risk |
| Anticausal $Y \to X$ | $P(x,y) = P(x\|y) \cdot P(y)$ | Digit class → pixel values |

This decomposition determines which component can shift:

| Shift Type | Stable | Changes | Typical Cause |
|------------|--------|---------|---------------|
| **Covariate Shift** | $P(y\|x)$ | $P(x)$ | Sample selection bias, deployment in new region |
| **Prior Probability Shift** | $P(x\|y)$ | $P(y)$ | Class imbalance changes over time |
| **Concept Shift** | $P(x)$ | $P(y\|x)$ | World changes, labels become outdated |
| **Total Shift** | — | $P(x,y)$ | Completely different domain |

---

## 🔍 Deep Dives

### 1. Covariate Shift
The relationship between features and labels stays constant, but the *population* you're predicting on looks different from what you trained on.

**Why it hurts**: A model that is *misspecified* (e.g., linear fit on a nonlinear process) will have been optimized for the wrong region of feature space. It extrapolates poorly.

**Fix direction**: Importance reweighting — up-weight training examples that look like the test distribution.

### 2. Prior Probability Shift (Label Shift)
The way classes look in feature space is stable, but the *frequency* of classes shifts. Via Bayes' rule:

$$P(y|x) = \frac{P(x|y) \cdot P(y)}{P(x)}$$

Even a constant $P(x|y)$ means a changed $P(y)$ moves the optimal decision boundary.

**Example**: A spam filter trained when 30% of emails are spam will be badly calibrated when 70% are spam.

### 3. Concept Shift
The hardest to fix. The inputs look the same, but the *meaning* of the labels has changed. The model learned the wrong thing permanently.

**Example**: "Expensive" in 2015 means something different in 2025. A price-sensitivity model needs retraining, not reweighting.

---

## 🎲 Sources of Shift

### Sample Selection Bias
Let $s$ be a binary "selected into training" indicator:

| Missingness Type | Condition | Resulting Shift |
|-----------------|-----------|-----------------|
| MCAR — Missing Completely at Random | $P(s=1 \| x,y) = P(s=1)$ | None |
| MAR — Missing at Random | $P(s=1 \| x,y) = P(s=1\|x)$ | Covariate Shift |
| MNAR — Missing Not at Random | $P(s=1 \| x,y) = P(s=1\|y)$ | Prior Probability Shift |

### Non-Stationary Environments
- **Temporal shift** — distributions drift over time (e.g., weather, language)
- **Spatial shift** — model trained in one location, deployed in another
- **Adversarial shift** — attackers actively push inputs out of the training distribution

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Simulating all three shift types from scratch with NumPy
2. Training a model on $P_{tr}$ and measuring degradation on $P_{tst}$
3. Visualizing the taxonomy with annotated plots
4. A real-world framing: mapping each shift type to a concrete ML failure

---

## 📚 References

- Moreno-Torres et al. (2012). *A unifying view on dataset shift in classification.* Pattern Recognition.
- Koh et al. (2021). *WILDS: A Benchmark of in-the-Wild Distribution Shifts.* ICML.
