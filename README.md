# Jailbreaking & LLMs: two-level analysis and attack family Classification

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![Libraries](https://img.shields.io/badge/Libraries-Pandas%20%7C%20Scikit--Learn%20%7C%20Seaborn-brightgreen)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-🤗-yellow)
![Transformer](https://img.shields.io/badge/Transformer-all--MiniLM--L6--v2-orange)

---

## Overview

As LLMs become more powerful, defending them against adversarial prompts is a growing challenge. Jailbreak attacks do not rely on obvious keyword, they exploit complex linguistic strategies, indirect instructions, and social engineering to disguise malicious intent inside seemingly legitimate requests.

This project systematically analyzes and classifies malicious prompts with a **two-level methodology**, comparing a surface-level statistical approach with a deep semantic one. The goal is to understand *how* attacks are structured and *which patterns they share*, a necessary foundation for building more adaptive defenses.

---

## Methodology

### Level 1 Statistical Approach
Classification based on structural and surface-level text features:
- Prompt length, word count, punctuation density
- Presence of suspicious keywords

### Level 2 Semantic Approach
Classification based on **sentence embeddings** (`all-MiniLM-L6-v2` via Sentence Transformers):
- Vector representations capturing the semantic intent of the prompt
- Logistic regression classifier trained on embeddings
- Focus on minimizing **false negatives**, undetected attacks are the critical failure mode in a security context

### Attack Family Clustering
Using the semantic embeddings, K-Means clustering is applied to the malicious prompts to discover whether jailbreak attacks organize themselves into semantically coherent **families**, groups of prompts sharing the same underlying strategy.

---

## Key Results

| Model | Accuracy | False Negatives |
|-------|----------|-----------------|
| Statistical (surface features) | Low | Critically high |
| Semantic (embeddings + LogReg) | **93%** | Drastically reduced |

- The statistical model proved **inadequate for a security context**: easily bypassed and producing too many false negatives
- The semantic model correctly intercepted indirect and "creative" attacks by reasoning on intent rather than form
- Clustering revealed that jailbreak attacks are **not randomly distributed**, they cluster into distinct families, each with a specific manipulation strategy

---

## Connection to Current Research

Recent literature (Peng et al., 2024 — *Rapid Response*) shows that the most effective defenses against jailbreaks do not rely on recognizing individual prompts, but on **rapidly responding to emerging attack strategies** by leveraging family-level knowledge.

This project sits **upstream** of such mechanisms: the clustering analysis provides a structured understanding of attack families, forming a natural basis for jailbreak proliferation and family-aware defense strategies.

---

## Workflow

```
1. Data cleaning and preparation
2. Exploratory Data Analysis (EDA)
3. Level 1 — Statistical feature extraction and classification
4. Level 2 — Semantic embedding and classification
5. K-Means clustering on embeddings → attack family discovery
```

---

## Tech Stack

| Tool | Use |
|------|-----|
| Python | Core language |
| Pandas, NumPy | Data manipulation |
| Scikit-learn | Classification, clustering, metrics |
| Matplotlib, Seaborn | Visualization |
| Sentence Transformers (`all-MiniLM-L6-v2`) | Semantic embeddings |
| Google Colab | Development environment |

---

## Dataset

**Malicious Prompt Detection Dataset (MPDD)**
~40k labeled prompts (safe / malicious) for detecting adversarial intent in AI inputs.
[https://www.kaggle.com/datasets/mohammedaminejebbar/malicious-prompt-detection-dataset-mpdd](https://www.kaggle.com/datasets/mohammedaminejebbar/malicious-prompt-detection-dataset-mpdd)

---

## References

Peng, A., Michael, J., Sleight, H., Perez, E., & Sharma, M. (2024).
*Rapid Response: Mitigating LLM Jailbreaks with a Few Examples.*
[https://arxiv.org/pdf/2411.07494](https://arxiv.org/pdf/2411.07494)

---

*Laura Pala — University of Bologna, January 2026*
