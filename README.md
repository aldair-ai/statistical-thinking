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
| 08 | [Multiple Testing](./class08-multiple-testing/) | FWER · Bonferroni · P-value distributions · Benford's Law | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class08-multiple-testing/notebook.ipynb) |
| 09 | [Why Most Research Findings Are False](./class09-why-findings-are-false/) | PPV · FDR · Publication Bias · P-hacking · Ioannidis (2005) | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class09-why-findings-are-false/notebook.ipynb) |
| 10 | [Distribution Shift](./class10-distribution-shift/) | Covariate · Prior Probability · Concept Shift · MCAR/MAR/MNAR · WILDS | [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](./class10-distribution-shift/notebook.ipynb) |

*More classes added weekly as the course progresses.*

---

## 🧠 What This Repo Demonstrates

- **Statistical reasoning** — FWER, PPV/FDR, p-value distributions, decomposing joint distributions
- **Experimental design** — power, sample size, bias sources, what makes a finding trustworthy
- **Critical thinking** — recognizing when standard assumptions break down in real-world deployment
- **Scientific communication** — translating math into reproducible, well-documented, visualized code

---

## 🛠️ Setup

```bash
git clone https://github.com/YOUR_USERNAME/dsc215-statistical-thinking.git
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
├── class08-multiple-testing/
│   ├── README.md        ← Theory notes with full math
│   ├── notebook.ipynb   ← FWER, Bonferroni, p-value distributions, Benford
│   └── figures/
├── class09-why-findings-are-false/
│   ├── README.md        ← PPV derivation, Ioannidis framework
│   ├── notebook.ipynb   ← Bias simulation, replication crisis
│   └── figures/
├── class10-distribution-shift/
│   ├── README.md        ← Covariate/prior/concept shift taxonomy
│   ├── notebook.ipynb   ← Shift simulations, MCAR/MAR/MNAR, WILDS
│   └── figures/
└── ...
```

---

## 👤 About

**MS Data Science — UCSD (2025–2026)**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/YOUR_PROFILE)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?logo=github)](https://github.com/YOUR_USERNAME)

---
*Instructor: Prof. Armin Schwartzman · UCSD Halıcıoğlu Data Science Institute*
