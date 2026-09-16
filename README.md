<div align="center">

# DisMoE-S

### Temporal Expert Routing and Distillation for Apex-Free Micro-Expression Recognition

<p>
  <img src="https://img.shields.io/badge/Task-Micro--Expression%20Recognition-355070?style=flat-square" alt="Task">
  <img src="https://img.shields.io/badge/Setting-Apex--Free-5C7AEA?style=flat-square" alt="Setting">
  <img src="https://img.shields.io/badge/Framework-PyTorch-EE4C2C?style=flat-square" alt="PyTorch">
</p>

<b>A temporal mixture-of-experts framework for apex-free micro-expression recognition.</b>

</div>

---

## Overview

Micro-expression recognition requires modeling subtle and short-lived facial dynamics. However, many existing methods rely on apex-frame annotations or predefined temporal priors, limiting their applicability in apex-free settings.

**DisMoE** addresses this limitation by constructing onset-referenced temporal observations within the onset--offset interval and assigning them to slot-specific temporal experts. A sample-adaptive routing network integrates complementary temporal evidence, while frame-level distillation transfers knowledge from the fused representation back to individual experts.

> **Key idea:** DisMoE avoids explicit apex localization and instead learns which temporal observations are informative for each sample.

---

## Highlights

- **Apex-free temporal modeling.**  
  Dynamic Interval Sampling (DIS) constructs onset-referenced motion observations without apex annotations.

- **Slot-specific temporal experts.**  
  Independent experts capture complementary motion patterns at different temporal positions.

- **Sample-adaptive expert routing.**  
  The Frame-level Expert Routing Module (FERM) dynamically aggregates temporal expert features according to sample-specific routing weights.

- **Frame-level distillation.**  
  Knowledge from the fused representation is transferred to individual experts to improve temporal consistency.

---

## Architecture

<div align="center">
  <img src="assets/DisMoE_overview.png"
       alt="Overall architecture of DisMoE"
       width="92%"><br>
  <sub>
    <b>Overview of DisMoE.</b>
    DIS constructs apex-free temporal observations, while FERM adaptively aggregates slot-specific experts.
    Routing regularization and frame-level distillation are applied during training.
  </sub>
</div>

---

## Method

<div align="center">

**Dynamic Interval Sampling**
&nbsp;&nbsp;→&nbsp;&nbsp;
**Temporal Experts**
&nbsp;&nbsp;→&nbsp;&nbsp;
**Expert Routing**
&nbsp;&nbsp;→&nbsp;&nbsp;
**Frame-level Distillation**

</div>

| Module | Function |
| :--- | :--- |
| **Dynamic Interval Sampling (DIS)** | Constructs onset-referenced temporal observations without apex annotations. |
| **Continuous Attention** | Enhances emotion-relevant spatial representations across feature layers. |
| **Frame-level Expert Routing Module (FERM)** | Adaptively aggregates slot-specific temporal expert features. |
| **Frame-level Distillation (FD)** | Transfers fused temporal knowledge to individual experts during training. |

### Expert Routing

Unlike conventional mixture-of-experts architectures that route a shared input among interchangeable experts, DisMoE maintains a fixed correspondence between each temporal sampling slot and its expert. The routing network therefore estimates the relative importance of temporal observations for each sample while preserving expert-specific temporal specialization.

---

## Model Variants

| Variant | Fusion Strategy | Characteristic |
| :---: | :--- | :--- |
| **DisMoE-S** | Weighted summation | Compact fused representation with lower computational overhead. |
| **DisMoE-C** | Weighted concatenation + projection | Retains richer slot-specific temporal information before projection. |

Both variants share the same apex-free sampling, temporal expert routing, routing regularization, and frame-level distillation framework.

---

<div align="center">
  <sub>
    DisMoE-S · Temporal Expert Routing and Distillation for Apex-Free Micro-Expression Recognition
  </sub>
</div>
