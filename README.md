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
  A temporal mixture-of-experts framework for apex-free micro-expression recognition.
</p>

---

## Abstract

Micro-expression recognition aims to identify subtle and short-lived facial movements that reveal genuine emotional states. However, many existing methods rely on apex-frame annotations or predefined temporal priors, limiting their applicability in apex-free settings.

We propose **DisMoE**, a temporal mixture-of-experts framework that models complementary motion patterns within the onset--offset interval without apex annotations. Dynamic Interval Sampling constructs onset-referenced temporal observations, which are processed by slot-specific experts and adaptively fused through frame-level expert routing. Frame-level distillation further transfers knowledge from the fused representation to individual experts, promoting consistent and complementary temporal modeling.

## Contributions

- **Apex-free temporal modeling.** Dynamic Interval Sampling (DIS) constructs onset-referenced motion observations without apex annotations.
- **Slot-specific temporal experts.** Independent experts model complementary motion patterns at different temporal positions.
- **Adaptive expert routing.** The Frame-level Expert Routing Module (FERM) performs sample-adaptive fusion of temporal expert features.
- **Frame-level distillation.** Knowledge from the fused representation is transferred to individual experts to improve temporal consistency.

## Method Overview

| Stage | Module | Function |
| :---: | :--- | :--- |
| 1 | Dynamic Interval Sampling | Constructs apex-free temporal observations. |
| 2 | Continuous Attention | Enhances emotion-relevant spatial representations. |
| 3 | Frame-level Expert Routing | Adaptively aggregates slot-specific expert features. |
| 4 | Frame-level Distillation | Transfers fused temporal knowledge to individual experts. |

## Overall Architecture

<div align="center">
  <img src="assets/DisMoE_overview.png" alt="Overall architecture of DisMoE" width="98%">
</div>
<p align="center">
  <em>Overview of DisMoE. DIS constructs apex-free temporal observations, while FERM adaptively aggregates slot-specific experts. Routing regularization and frame-level distillation are applied during training.</em>
</p>
### Design Principle

DisMoE maintains a fixed correspondence between each temporal sampling slot and its expert. The routing network therefore learns the relative importance of temporal observations for each sample while preserving expert-specific temporal specialization.

## Model Variants

| Variant | Fusion strategy | Characteristic |
| :--- | :--- | :--- |
| **DisMoE-S** | Weighted summation | Compact representation with an efficient accuracy--cost trade-off. |
| **DisMoE-C** | Weighted concatenation with projection | Retains richer slot-specific information before projection. |

Both variants share the same apex-free sampling, temporal expert routing, routing regularization, and frame-level distillation framework.

---

<div align="center">
  <sub>DisMoE-S · Temporal Expert Routing and Distillation for Apex-Free Micro-Expression Recognition</sub>
</div>
