# 📊 DSC 215 — Statistical Critical Thinking & Experimental Design
### University of California San Diego · MS Data Science · 2025–2026

[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

> A structured portfolio of **theory notes, code implementations, and real-world examples** from DSC 215 at UCSD. Each module pairs lecture concepts with reproducible Python notebooks — simulating, visualizing, and stress-testing the ideas from scratch.

---

## 🗂️ Course Modules

| Class | Topic | Core Concepts | Notebook |
|-------|-------|---------------|----------|
| 01 | [Experimental Design](./class01-experimental-design/) | Confounding · Randomization · Blocking · Factorial Design · Meta-Analysis | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class01-experimental-design/notebook.ipynb) |
| 02 | [Introduction to Causal Inference](./class02-causal-inference/) | Potential Outcomes · ATE · Selection Bias · Rubin Model · RCT | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class02-causal-inference/notebook.ipynb) |
| 06 | [Bias, Multiple Testing & P-Hacking](./class06-bias-multiple-testing/) | Publication Bias · Confirmation Bias · FWER · P-Hacking · P-HARKing · Benford's Law | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class06-bias-multiple-testing/notebook.ipynb) |
| 07 | [Meta-Analysis and Publication Bias](./class07-meta-analysis/) | Inverse-Variance Weighting · Funnel Plot · Boundary Derivation · Egger's Test | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class07-meta-analysis/notebook.ipynb) |
| 08 | [Multiple Testing](./class08-multiple-testing/) | FWER · Bonferroni · P-value Distributions · Benford's Law | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class08-multiple-testing/notebook.ipynb) |
| 09 | [Why Most Research Findings Are False](./class09-why-findings-are-false/) | PPV · FDR · Publication Bias · P-hacking · Ioannidis (2005) | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class09-why-findings-are-false/notebook.ipynb) |
| 10 | [Distribution Shift](./class10-distribution-shift/) | Covariate · Prior Probability · Concept Shift · MCAR/MAR/MNAR · WILDS | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class10-distribution-shift/notebook.ipynb) |

*More classes added weekly as the course progresses.*

---

## 🧠 What This Repo Demonstrates

- **Experimental design** — confounding, randomization, blocking, factorial designs, meta-analysis
- **Causal reasoning** — potential outcomes framework, ATE, why observational estimates fail
- **Bias & integrity** — publication bias, confirmation bias, p-hacking, P-HARKing, data fabrication detection
- **Meta-analysis** — inverse-variance weighting, funnel plots, boundary derivation, Egger's test
- **Statistical reliability** — FWER, PPV/FDR, p-value distributions, Bonferroni & BH corrections
- **ML robustness** — covariate, prior probability, and concept shift; MCAR/MAR/MNAR
- **Scientific communication** — translating math into reproducible, well-documented, visualized code

---

## 🛠️ Setup

```bash
git clone https://github.com/aldair-ai/dsc215-statistical-thinking.git
cd dsc215-statistical-thinking
pip install -r requirements.txt
jupyter lab
```

---

## 📁 Repo Structure

```
dsc215-statistical-thinking/
├── README.md
├── requirements.txt
├── class01-experimental-design/
│   ├── README.md        ← Theory: confounding, blocking, factorial, meta-analysis
│   ├── notebook.ipynb   ← Simulations, interaction plots, forest plots
│   └── figures/
├── class02-causal-inference/
│   ├── README.md        ← Potential outcomes, ATE, selection bias, RCT proof
│   ├── notebook.ipynb   ← Vitamin C example, selection bias, sensitivity analysis
│   └── figures/
├── class06-bias-multiple-testing/
│   ├── README.md        ← Publication bias, confirmation bias, FWER, p-hacking, Benford's Law
│   ├── notebook.ipynb   ← Funnel plots, p-value distributions, Bonferroni & BH, last-digit test
│   └── figures/
├── class07-meta-analysis/
│   ├── README.md        ← Inverse-variance weighting, funnel plot derivation, Egger's test
│   ├── notebook.ipynb   ← Weighted estimator, simple model, publication bias simulation
│   └── figures/
├── class08-multiple-testing/
│   ├── README.md
│   ├── notebook.ipynb
│   └── figures/
├── class09-why-findings-are-false/
│   ├── README.md
│   ├── notebook.ipynb
│   └── figures/
├── class10-distribution-shift/
│   ├── README.md
│   ├── notebook.ipynb
│   └── figures/
└── ...
```

---

## 👤 About

**MS Data Science — UCSD (2025–2026)**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/aldair-ai/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?logo=github)](https://github.com/aldair-ai)

---
*Instructor: Prof. Armin Schwartzman · UCSD Halıcıoğlu Data Science Institute*
