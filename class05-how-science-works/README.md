# Class 05 — How Science Works

**DSC 215 · Statistical Critical Thinking & Experimental Design · UCSD**

*Based on Science Fictions, Chapter 1 — Stuart Ritchie*

---

## 📖 Theory Summary

### Science as a Social Construct

Science doesn't happen in isolation. Results become accepted knowledge through a social process: publication, peer review, replication, and consensus. This means the quality of science depends not just on individual researchers but on the **institutions and incentives** surrounding them.

**The iteration of scientific activity (from slides):**
1. Read existing work
2. Form a new hypothesis
3. Exploratory experiments
4. Apply for funding
5. Verification experiments
6. Submit for publication → peer review → publish
7. Wait for replication

Each step is a potential failure point.

---

## 📚 Finding and Reading Literature

- Papers after 1985 are mostly available online; Google Scholar and PubMed are primary search tools
- **Citation count** is the standard popularity proxy — but citation distributions are highly skewed (power-law / Lotka's Law). The top 10% of papers attract the majority of citations
- Most readers only see the title. A smaller fraction read the abstract. Fewer still read the full paper
- ArXiv publishes any article (within reason) and serves as a timestamp for priority claims

**Reading order in practice:**
1. Title → if relevant
2. Abstract → if interesting
3. Introduction → if important
4. Full article → rarely

This means the abstract carries enormous weight and is frequently the only thing cited or quoted — even if it misrepresents the paper's actual findings.

---

## 💰 Funding

- **Basic science:** NSF
- **Clinical applications:** NIH
- Funding follows popular areas: bioinformatics (2000s), brain imaging (2010s), AI (2020s)
- Politics matters: federal vs. industry funding shapes which questions get asked
- Financial conflicts of interest are one of Ioannidis' key factors inflating bias $u$

---

## 🔍 Peer Review — How It Should Work

1. Paper submitted to journal or conference
2. Area editor assigns multiple reviewers
3. Reviewers write critiques independently
4. Editor makes accept/reject decision (sometimes with rebuttal)
5. Prestigious venues have low acceptance rates (~10–25%)

**The ideal:** expert, independent, unbiased evaluation. The reality is messier.

---

## ⚠️ Peer Review Failures

| Problem | Consequence |
|---------|-------------|
| Reviewers not always qualified | Noisy quality signal — false accepts and false rejects |
| Reviewer likes/dislikes author | Bias; solution: double-blind reviewing |
| Papers in new areas always rejected | Stagnation; solution: start new journals |
| Publishers restrict access | Knowledge silos; solution: ArXiv, open access |

Peer review is best modeled as a **noisy binary classifier**: it has false accept rates and false reject rates that depend on reviewer quality and the number of reviewers.

---

## 🧭 Mertonian Norms

Robert Merton (1942) proposed four norms for ethical scientific practice:

| Norm | Meaning | Violation example |
|------|---------|------------------|
| **Universalism** | Knowledge is objective, not tied to who produced it | Rejecting results because of the author's identity |
| **Disinterestedness** | Scientists are not motivated by personal gain | Pharma-funded trials with financial conflict of interest |
| **Communality** | Knowledge should be shared | File drawer problem: hiding negative results |
| **Organized skepticism** | Any claim can be questioned and tested | Not requiring replication before acceptance |

Each violation has a direct, quantifiable effect on the reliability of published research — mapping into the Ioannidis PPV framework as increases in bias $u$ or decreases in power $\gamma$.

---

## ❌ Famous Scientific Mistakes

The slides list errors that were once accepted consensus:

| Mistake | Core failure |
|---------|-------------|
| Geocentrism | Unfalsifiable (epicycles could explain anything) |
| Phlogiston | Measurement error (mass increase contradicted theory) |
| Miasma theory | Confounding (bad smells and disease co-occur) |
| Bloodletting | No control group |
| Aether | Unfalsifiable auxiliary hypotheses |
| Spontaneous generation | Poorly controlled experiments |
| Phrenology | Motivated reasoning + no replication |
| Martian canals | Observer bias + instrument limits |

Almost every error traces to a problem covered elsewhere in this course.

---

## 🔬 Consensus vs. Controversy

**Solid consensus (from slides):** plate tectonics, general relativity, quantum mechanics, germ theory
**Still debated:** anthropogenic climate change (politically contested, scientifically robust), Darwinian evolution, epigenetics

The distinction matters: scientific controversy ≠ public controversy. The degree of consensus correlates strongly with the falsifiability of the core claims and the number of independent replications.

---

## 🎯 Karl Popper and Falsifiability

Popper's criterion: a scientific claim must be *in principle disprovable* by evidence.

**Why this matters statistically:**
- An unfalsifiable claim can never be refuted — the researcher can always add an auxiliary hypothesis
- This is equivalent to high bias $u$ in the Ioannidis model: every experiment can be made to "support" the theory
- Replication under independent conditions is the empirical enforcement mechanism

**Popper's three requirements for replication:**
1. Enough replications
2. Under sufficiently many conditions
3. Compared against other replicable claims

---

## 💻 Notebook

The companion notebook [`notebook.ipynb`](./notebook.ipynb) demonstrates the quantitative structure behind these concepts:

1. Citation power-law distribution and Lorenz curve
2. Peer review modeled as a noisy classifier — false accept/reject rates vs. noise and reviewer count
3. Each Mertonian norm violation plotted as a PPV degradation curve (connecting to Class 09)
4. Famous mistakes categorized by failure mode with course cross-references
5. Replication rate simulated as a function of the "unfalsifiability bias" parameter
6. Course synthesis: every class mapped to the scientific failure it prevents

---

## 📚 References

- Ritchie, S. (2020). *Science Fictions.* Metropolitan Books.
- Merton, R.K. (1942). *The Normative Structure of Science.* In: The Sociology of Science (1973).
- Popper, K. (1959). *The Logic of Scientific Discovery.* Basic Books.
- Lotka, A.J. (1926). *The frequency distribution of scientific productivity.* Journal of the Washington Academy of Sciences 16: 317–323.
- Ioannidis, J.P.A. (2005). *Why Most Published Research Findings Are False.* PLOS Medicine.
