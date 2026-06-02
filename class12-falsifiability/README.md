# Week 12 — Falsifiability & Karl Popper

**DSC 215 · Statistical Critical Thinking & Experimental Design**

---

## 📖 Theory Summary

### The Core Idea

Karl Popper (1902–1994) asked a deceptively simple question: **what separates science from non-science?** His answer — *falsifiability* — became one of the most influential ideas in the philosophy of science.

> "In so far as a scientific statement speaks about reality, it must be falsifiable; and in so far as it is not falsifiable, it does not speak about reality." — Karl Popper

---

## 🗺️ Historical Context: Vienna in the 1920s

Popper developed his ideas in post-WWI Vienna — a cauldron of competing ideologies and intellectual movements:

| Movement | Key Figure | Popper's Assessment |
|----------|-----------|---------------------|
| Marxism | Marx / Lenin | Originally scientific, became dogmatic |
| Psychoanalysis | Sigmund Freud | Interesting, but explains everything — untestable |
| Theory of Relativity | Albert Einstein | Paradigm of genuine science: bold, risky, falsifiable predictions |

The contrast between Einstein and Freud/Marx was the seed of Popper's entire philosophy.

---

## 🔍 Deep Dives

### 1. Against Induction

Classical philosophy of science held that science works by **induction**: accumulating observations and deriving general laws.

Popper's objection: **you can never logically prove a universal law from a finite number of observations.** No matter how many white swans you observe, you cannot prove "all swans are white." (In fact, black swans exist in Australia.)

His alternative: theory comes first — from intuition, not induction — and is then tested by attempting to falsify it.

### 2. The Asymmetry Principle

| Direction | Logic | Example |
|-----------|-------|---------|
| Verification | Impossible — finite data cannot confirm a universal claim | 1,000 white swans ≠ proof all swans are white |
| Falsification | Logically decisive — one counterexample refutes the universal | 1 black swan falsifies "all swans are white" |

This asymmetry is the logical foundation of Popper's criterion. It maps directly onto statistical hypothesis testing:
- We never *accept* $H_0$, we *fail to reject* it (verification impossible)
- We *reject* $H_0$ when evidence is incompatible with it (falsification decisive)

### 3. Falsifiability as Demarcation

A theory is **scientific** if and only if it makes at least one prediction that could, in principle, be shown false by observation. The *potential* for falsification is what matters, not whether it has been falsified.

| Criterion | Science | Pseudo-science |
|-----------|---------|----------------|
| Falsifiability | Contains potential falsifiers | Consistent with all observations |
| Predictions | Bold, risky, specific | Vague or non-committal |
| Use of evidence | To test the theory | To confirm the theory |
| Response to anomalies | Modifies or rejects theory | Ad hoc hypotheses to rescue it |

### 4. Corroboration vs. Verification

Popper carefully distinguished:
- **Verification**: proof that a theory is *true* — logically impossible for universal statements
- **Corroboration**: the theory has survived rigorous attempts to falsify it — all we can say positively

A well-corroborated theory is not a *confirmed* theory; it is simply one that has not yet been falsified.

### 5. Basic Statements

In practice, a single anomaly is rarely enough to overturn a well-established theory. Popper introduced the concept of a **basic statement** — a formally accepted potential falsifier that must:
- Refer to a single, specific observable event
- Be reproducible by anyone with appropriate equipment
- Be accepted by convention within the scientific community

### 6. Connection to Hypothesis Testing

Statistical hypothesis testing is Popperian science in formal clothing:

| Popper | Statistics |
|--------|-----------|
| Current theory | Null hypothesis $H_0$ |
| Risky prediction | Test statistic, critical region |
| Basic statement | Observed data, p-value |
| Falsification | Reject $H_0$ |
| Corroboration | Fail to reject $H_0$ |
| New theory | Alternative hypothesis $H_A$ becomes the new $H_0$ to be tested |

### 7. Popper's Propensity Theory of Probability

Popper was dissatisfied with both the frequentist and Bayesian views and proposed a third: **propensity**.

| View | Definition | Problem |
|------|-----------|---------|
| Frequentist | Long-run frequency | Requires infinite repetitions |
| Bayesian | Degree of belief | Subjective |
| **Propensity** | Physical tendency of a setup to produce an outcome | Objective, applies to single events |

Propensity is a property of the experimental *setup*, not of sequences of outcomes or of minds.

### 8. Evolution of Science

Science progresses not by accumulating truths, but by eliminating errors:

**Early Conjectures → Bold Predictions → Critical Tests → Error Correction → Refined Knowledge → (repeat)**

Theories compete for survival like organisms — the "fittest" (most corroborated, most informative) survive. Knowledge grows by discarding what is false.

---

## 🧪 Science or Pseudo-science?

The course slides worked through several examples. Key takeaways:

- **Falsifiable**: vaccination prevents disease, natural selection, general relativity, conservation of energy, "deep neural networks outperform dermatologists at melanoma classification"
- **Not falsifiable** (as typically stated): "God exists," "my girlfriend hates me," "AI has consciousness"
- **Borderline / context-dependent**: economics, history, climate change, astrology

The boundary is not always sharp. A claim can be made more or less scientific by how precisely it is stated.

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Visualizing the asymmetry principle with a simulation of swan sampling
2. Classifying statements as falsifiable or not, and scoring their "boldness"
3. Mapping the Popperian cycle onto a real hypothesis test step-by-step
4. Simulating how ad hoc hypotheses inflate Type I error and destroy falsifiability
5. The evolution of science: a toy model where theories compete and are replaced

---

## 📚 References

- Popper, K. (1934/1959). *The Logic of Scientific Discovery.* Hutchinson.
- Popper, K. (1963). *Conjectures and Refutations.* Routledge.
- Lakatos, I. (1978). *The Methodology of Scientific Research Programmes.* Cambridge.
- Mayo, D.G. (2018). *Statistical Inference as Severe Testing.* Cambridge University Press.
