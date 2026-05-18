# Class 03 — Observational Studies

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

---

## 📖 Theory Summary

### What Is an Observational Study?

An observational study collects data on subjects **without intervening** — the researcher watches, records, and analyzes, but never controls who receives a treatment. Most real-world data is observational: medical records, social media logs, economic surveys, satellite imagery.

The core limitation: **association ≠ causation**.

---

## 🔬 Designed Experiments vs. Observational Studies

| | Designed Experiment | Observational Study |
|--|--------------------|--------------------|
| **Intervention** | Yes | No |
| **Control** | Strict | Limited |
| **Causal conclusion** | Possible | Not possible |
| **Timing** | Prospective | Retrospective |
| **Cost** | High | Low |
| **Confounders** | Eliminated by randomization | Must be controlled statistically |

---

## 🗺️ The 2×2 Causation × Generalizability Matrix

The slides present a crucial framework that most researchers ignore:

|  | **Random Assignment** | **No Random Assignment** |
|--|----------------------|--------------------------|
| **Random Sampling** | Causal conclusion, generalized to whole population *(ideal experiment)* | Correlation only, generalized to population *(most observational studies)* |
| **No Random Sampling** | Causal conclusion for the sample only *(most experiments)* | Correlation for sample only *(bad observational studies)* |

**Key insight:** Most published experiments are in the bottom-left cell — they establish causality but only for their specific sample, not the general population. Most observational studies are in the top-right — they can make population-level correlation statements but nothing causal.

---

## 🔤 Three Meanings of "Control" — A Critical Distinction

The word "control" means three different things in statistics, and conflating them is a common source of confusion:

1. **Controlled experiment** — the researcher assigns who receives treatment and who does not (randomization)
2. **Control subject** — an untreated individual serving as a comparison group
3. **Control for confounders** — making inference conditional on confounding variables (stratification, regression, matching)

---

## 🌀 Confounders

A **confounder** $Z$ simultaneously correlates with both the predictor $X$ and the response $Y$, creating a spurious apparent association:

```
X ←── Z ──→ Y
(no direct arrow X → Y)
```

**Classic example:** Ice cream sales and drowning deaths both rise in summer. Heat is the confounder. The association is real; the causation is not.

**From the slides:**
- Millennials have lower joint replacement rates than Baby Boomers — not because of generational behavior, but because joint replacement is an **age effect**, not a **cohort effect**. Millennials are simply younger.
- Ultra-processed food and anxiety (BMJ 2024), AI use and depression (JAMA 2026) — both observational. Confounders could include socioeconomic status, baseline mental health, or personality traits.

### Strategies for Handling Confounders in Observational Studies

| Method | How it works | Limitation |
|--------|-------------|------------|
| **Stratification** | Analyze within homogeneous subgroups | Only works for measured, discrete confounders |
| **Regression adjustment** | Include confounder as covariate | Assumes correct model; can't fix unmeasured confounders |
| **Matching** | Pair treated and control subjects on confounders | Expensive; residual confounding remains |
| **Propensity scores** | Model P(treatment\|covariates), reweight | Still can't fix unmeasured confounders |

---

## 🌍 Generalizability

Results generalize when the **sample is representative** of the **target population**. This requires **random sampling** from that population.

**Common failures:**
- WEIRD populations (Western, Educated, Industrialized, Rich, Democratic) in psychology studies
- Hospital patients as proxies for the general population
- Convenience samples (online surveys, volunteer studies)
- Historical data that doesn't reflect current conditions

Even a perfectly designed RCT can have poor external validity if its sample isn't representative.

---

## 📋 Real Examples from the Slides

| Study | Claim | Type | Critical Question |
|-------|-------|------|-------------------|
| Lane et al. (BMJ 2024) | Ultra-processed food → +48-53% anxiety risk | Observational | Confounder: people with anxiety may eat worse |
| Perlis et al. (JAMA 2026) | Daily AI use → +30% depression symptoms | Observational | Reverse causation: depressed people may seek AI |
| Pilfold et al. (Nature 2024) | Polar bears lose 1 kg/day on land | Observational | Ecological — no intervention possible |
| Barnola et al. (Nature 1987) | CO₂ and temperature — 160,000-year correlation | Observational | Directionality: CO₂ leads or lags? |
| Nobel 2024 (Acemoglu et al.) | Extractive institutions → persistent poverty | Quasi-experimental | Uses historical natural experiments |

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) demonstrates the concepts the slides assert:

1. The 2×2 matrix — simulating all four cells and verifying what each can and can't conclude
2. Confounding from scratch — building and diagnosing a confounder
3. Confounder correction strategies — stratification, regression, matching
4. Generalizability — how a non-representative sample distorts conclusions
5. Critical reading of observational claims — reverse causation, unmeasured confounders

---

## 📚 References

- Schwartzman, A. DSC 215 Lecture Notes, UCSD Spring 2026.
- Hernán, M.A. & Robins, J.M. (2020). *Causal Inference: What If.* CRC Press.
- Greenland, S. (2017). *For and against methodologies.* European Journal of Epidemiology.
- Pearl, J. & Mackenzie, D. (2018). *The Book of Why.* Basic Books.
