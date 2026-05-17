# Class 01 — Experimental Design

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

---

## 📖 Theory Summary

### What Is Experimental Design?

Experimental design is the process of planning an experiment so that data can be analyzed by statistical methods to produce **valid and objective conclusions**. The core question it answers is:

> "Does a change in X **cause** a change in Y?"

This is distinct from two related but different problems:
- **Causal discovery** — inferring directionality from the joint distribution of observed data
- **Causal inference** — mimicking an experiment using observational data

Experimental design is the direct route: you control the world, rather than reason about it after the fact.

---

## 🗂️ Key Variables

| Variable Type | Role | Example |
|--------------|------|---------|
| **Independent** | Manipulated by the researcher — the "cause" | Drug dosage |
| **Dependent** | Measured outcome — the "effect" | Blood pressure |
| **Extraneous / Confounders** | Not of interest but could influence results if uncontrolled | Patient age, diet |

---

## 🧪 Core Design Elements

### Control Groups

- **Experimental group** — receives the treatment
- **Control group** — receives no treatment, but is otherwise treated identically
- **Purpose** — isolates the effect of the independent variable by ruling out outside influences like environmental factors or the passage of time

### Randomization

The gold standard for preventing bias. Subjects are assigned to groups by chance (coin flip, random number generator). This ensures:
- Groups are as similar as possible before the experiment begins
- Individual differences (age, health, genetics) are spread across all groups
- No systematic bias can favor one group

### Confounders

A confounder correlates with **both** the independent and dependent variable, creating a spurious apparent effect.

**Classic example:** Ice cream consumption correlates with drowning deaths. The confounder is summer heat — it drives both. Mistaking this for causation leads to absurd recommendations.

**Solution:** Randomization and strict control protocols eliminate lurking variables.

### Placebo and Blinding

| Design | What's hidden | Eliminates |
|--------|--------------|------------|
| **Open label** | Nothing | — |
| **Single-blind** | Treatment assignment from participants | Participant expectation bias |
| **Double-blind** | Treatment assignment from participants AND researchers | Both participant and researcher bias |

The placebo effect is real and measurable — participants can show genuine physiological improvement simply from believing they are receiving treatment. A placebo group quantifies this so it can be subtracted from the treatment effect.

---

## 🎲 Forms of Randomization

### Completely Randomized Design (CRD)
Every unit has equal probability of assignment to any group. Simplest design. Best when units are homogeneous.

### Randomized Block Design (RBD)
When a known variable affects the outcome, **block** on it first. Randomly assign treatments *within* each block. Blocks are groups homogeneous in that variable (e.g., gender, age group, soil quality). Reduces noise from the blocked variable.

### Matched Pairs Design
Specialized RBD where subjects are paired on a very similar characteristic (e.g., identical twins, or the same person tested twice under both conditions). One member of each pair gets each treatment.

### Factorial Design
Test more than one independent variable simultaneously. Allows studying **interactions** — where the effect of one factor depends on the level of another.

**Example:** Testing drug dosage (5 mg vs 10 mg) × time of day (morning vs evening) on sleep quality. Four conditions, one experiment. Efficient and reveals interactions that one-factor designs miss.

---

## ✅ Internal vs. External Validity

| | Internal Validity | External Validity |
|--|-------------------|------------------|
| **Definition** | Degree to which the study demonstrates a true causal relationship | Degree to which results generalize to real-world settings |
| **Threat** | Confounders, bias, measurement error | Artificial lab setting, unrepresentative sample |
| **Trade-off** | High control → high internal, often low external | Naturalistic study → high external, harder to control internally |

### Threats to Internal Validity

- **Maturation** — natural changes in subjects over time (fatigue, hunger, growth)
- **History** — external events during the experiment that affect outcomes
- **Instrumentation** — changes in measurement procedures or calibration mid-study
- **Learning / Testing effects** — participants perform differently on repeated tests simply from prior exposure

---

## 📊 Meta-Analysis

When individual studies disagree, meta-analysis finds the signal in the noise.

**Definition:** A statistical technique that combines results from multiple independent studies on the same question to produce a more precise estimate of the true effect.

**Key advantages:**
- **Increased power** — pooling 10 studies of n=100 creates an effective N=1000
- **Generalizability** — if an effect holds across different labs, populations, and time periods, confidence in its real-world validity increases substantially
- **Resolves inconsistency** — weights studies by precision, reducing the influence of small noisy studies

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) covers:

1. Simulating the confounding problem — showing how observational estimates can be badly wrong
2. Randomization as a fix — demonstrating covariate balance before/after
3. CRD vs. RBD — comparing variance reduction from blocking
4. Factorial design — interaction plots and why one-factor-at-a-time misses them
5. Internal vs. external validity trade-off — concrete simulation
6. Meta-analysis basics — pooling estimates, forest plots

---

## 📚 References

- Schwartzman, A. DSC 215 Lecture Notes, UCSD Spring 2026.
- Fisher, R.A. (1935). *The Design of Experiments.* Oliver & Boyd.
- Shadish, W.R., Cook, T.D., & Campbell, D.T. (2002). *Experimental and Quasi-Experimental Designs for Generalized Causal Inference.* Houghton Mifflin.
