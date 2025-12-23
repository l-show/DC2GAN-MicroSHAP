# DC2GAN-MicroSHAP
An improved DC2GAN framework featuring diversity constraints to mitigate mode collapse. This repository also provides a micro-perspective SHAP interpretation module to reveal how data balancing and category-specific collapse influence Shapley values and the causal relationships between features and accident severity.

# DC2GAN: Diversity-Constrained Deep Convolutional GAN for Traffic Crash Prediction

[![Version](https://img.shields.io/badge/version-1.0.0-blue)](https://github.com/your-username/DC2GAN)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

---

### [English](#english-version) | [中文版](#中文版)

---

## 中文版

### 1. 模型简介 (Model Architecture)
**DC2GAN** 是一种改进的生成对抗网络，专为解决交通事故数据中的**类别不平衡**问题而设计。
*   **核心创新**：
    *   **伪图像编码 (Pseudo-image Coding)**：通过特征重排将 1D 交通数据转化为 2D 结构，保留变量间的空间耦合关系。
    *   **多样性约束 (Diversity-Constrained Loss)**：引入模式寻求损失（Mode-seeking loss）和分布矩匹配损失，确保生成的少数类样本（如严重事故）具有高度的多样性和真实性。

### 2. 微观可解释性分析 (Microscopic SHAP Analysis)
本项目使用 SHAP 揭示了模型预测逻辑与现实因果关系之间的差异，主要结论如下：

#### A. SHAP 摘要图：预测贡献 $\neq$ 因果关系
*   **分布偏差影响**：SHAP 值反映的是特征对**模型预测**的贡献，而非直接的物理因果。由于数据分布偏差，模型在不同类别上的逻辑存在差异。
*   **严重事故 (Class 2) 的一致性**：实验发现，Class 2 的 SHAP 排序与现实风险（如：无灯光、未系安全带、非分道行驶）高度吻合。
*   **异常现象**：在 Class 0/1 中，某些风险因素（如无灯光环境 `LGHT_COND_CD`）反而表现出负相关。这并非现实规律，而是由于模型基于不平衡数据的学习偏差导致的逻辑异化。

#### B. 3D 热图：动态 vs. 静态特征
*   **动态参与者贡献更高**：3D 热图显示，**车辆 (Vehicle)** 和 **人员 (Person)** 等动态特征的 Shapley 值显著高于 **环境 (Event)** 等静态特征。
*   **关注重点**：在预防事故严重性时，应优先关注动态元素的行为风险。

#### C. 堆叠图：数据平衡对决策逻辑的影响
*   **逻辑迁移**：数据平衡过程会改变个别特征的 SHAP 值，导致决策边界发生偏移。
*   **稳定性**：Class 2（严重事故）的特征贡献分布最均衡、最稳定。相比之下，Class 1 的决策边界较模糊，因果分析结果不如 Class 2 鲁棒。

---

## English Version

### 1. Model Overview
**DC2GAN** is an advanced Generative Adversarial Network designed to address **class imbalance** in traffic crash datasets.
*   **Core Innovations**:
    *   **Pseudo-image Coding**: Reorganizes 1D features into 2D space based on correlation to preserve latent coupling relationships.
    *   **Diversity Constraints**: Integrates mode-seeking and distribution moment-matching losses to generate diverse, high-fidelity minority samples (e.g., severe crashes).

### 2. Microscopic Interpretability (SHAP)
This project employs SHAP to bridge the gap between model predictive logic and real-world causality:

#### A. SHAP Summary Plot: Prediction $\neq$ Causality
*   **Distribution Bias**: Shapley values represent feature contributions to the **model's output**, not necessarily direct causal effects. 
*   **Class 2 Alignment**: For **Severe Injury (Class 2)**, SHAP rankings align closely with real-world risks (e.g., unlit roads, no seatbelts).
*   **Logic Anomalies**: In Class 0/1, factors like "No Light" (`LGHT_COND_CD`) may show negative correlations due to data distribution bias, highlighting that SHAP should be interpreted with caution in multi-class tasks.

#### B. 3D Heatmap: Dynamic vs. Static Features
*   **Higher Contribution from Dynamic Elements**: 3D heatmaps reveal that **Vehicle** and **Person** features contribute significantly more to severity prediction than static **Event** (environmental) features.
*   **Key Insight**: Safety interventions should prioritize dynamic behavioral risks over static environmental conditions.

#### C. Stacked Plot: Impact of Data Balancing
*   **Decision Shift**: Data balancing procedures alter individual Shapley values, shifting the model's decision boundaries.
*   **Robustness**: Class 2 (Green) exhibits a balanced and stable distribution of feature contributions, whereas Class 1 (Orange) shows higher ambiguity, suggesting that causal inferences derived from Class 2 are more robust.

---

## 快速开始 / Quick Start

```python
# 示例代码
# Example
```

## 引用 / Citation

```
