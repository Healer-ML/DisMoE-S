<div align="center">

# DisMoE-S

### Temporal Expert Routing and Distillation for Apex-Free Micro-Expression Recognition

<p>
  <a href="https://github.com/Healer-ML/DisMoE-S">
    <img src="https://img.shields.io/badge/Task-Micro--Expression%20Recognition-34495e?style=flat-square" alt="Task">
  </a>
  <a href="https://github.com/Healer-ML/DisMoE-S">
    <img src="https://img.shields.io/badge/Setting-Apex--Free-5b7c99?style=flat-square" alt="Setting">
  </a>
  <a href="https://github.com/Healer-ML/DisMoE-S">
    <img src="https://img.shields.io/badge/Framework-PyTorch-8c6d62?style=flat-square" alt="Framework">
  </a>
</p>

</div>

<p align="center">
  A temporal mixture-of-experts framework for recognizing subtle facial expressions without apex-frame annotations.
</p>

---

## Abstract

Micro-expression recognition aims to identify genuine emotional states from facial movements that are subtle, localized, and short-lived. Existing approaches often rely on apex-frame annotations or fixed temporal priors, which limits their applicability in apex-free settings.

We propose **DisMoE**, a temporal expert routing and distillation framework for apex-free micro-expression recognition. The method uses the onset frame as a temporal reference and constructs multiple motion observations within the onset–offset interval. Each observation is assigned to an independently parameterized temporal expert, while a sample-adaptive routing network learns how to combine their complementary evidence. Frame-level distillation further transfers knowledge from the fused representation back to individual experts, improving the consistency of temporal predictions.

## Contributions

1. **Apex-free temporal modeling.** Dynamic Interval Sampling (DIS) constructs onset-referenced motion inputs without requiring apex annotations.
2. **Slot-specific temporal experts.** Independently parameterized experts capture complementary motion patterns from different temporal positions.
3. **Adaptive expert fusion.** The Frame-level Expert Routing Module (FERM) uses a Frame-wise Routing Network (FRN) to perform dense, sample-adaptive fusion.
4. **Knowledge transfer across experts.** Frame-level Distillation (FD) transfers complementary information from the fused branch to individual temporal experts.

## Method Overview

The framework contains four main stages:

| Stage | Module | Function |
| :---: | :--- | :--- |
| 1 | Dynamic Interval Sampling | Samples onset-referenced observations within the onset–offset interval. |
| 2 | Continuous Attention | Refines emotion-relevant spatial representations across feature layers. |
| 3 | Frame-level Expert Routing | Predicts sample-adaptive weights and fuses slot-specific expert features. |
| 4 | Frame-level Distillation | Transfers fused temporal knowledge to individual experts during training. |

## Overall Architecture

<div align="center">
  <img src="assets/DisMoE_overview.png" alt="Overall architecture of the DisMoE framework" width="98%">
</div>

<p align="center">
  <em>Overall architecture of DisMoE. DIS constructs apex-free temporal observations; FERM adaptively aggregates independently parameterized experts; routing regularization and frame-level distillation are applied during training.</em>
</p>

### Design principle

Unlike conventional mixture-of-experts models that route a shared input among interchangeable experts, DisMoE maintains a fixed correspondence between each temporal sampling slot and its expert. The routing network therefore learns **which temporal observations are more informative for the current sample**, while preserving complementary temporal specialization across experts.

## Model Variants

| Variant | Fusion strategy | Main characteristic |
| :--- | :--- | :--- |
| **DisMoE-S** | Weighted summation | Compact fused representation with a favorable accuracy–efficiency trade-off. |
| **DisMoE-C** | Weighted concatenation followed by projection | Preserves more slot-specific temporal information before dimensionality reduction. |

Both variants share the same apex-free sampling, temporal expert routing, routing regularization, and frame-level distillation framework.

---

<div align="center">
  <sub>DisMoE-S · Temporal Expert Routing and Distillation for Apex-Free Micro-Expression Recognition</sub>
</div>
