---
title: 'Multimodal Pain Classification (m-PainAttnNet)'
summary: 'Extended PainAttnNet with attention fusion of physiological modalities (ECG, EMG, EDA) for robust 5-class pain intensity classification'
date: 2024-04-01
authors:
  - admin
tags:
  - Multimodal Learning
  - Deep Learning
  - Healthcare AI
  - Attention Mechanisms
  - Transformers
image:
  caption: 'm-PainAttnNet Architecture'
  focal_point: ''
  preview_only: false
url_code: 'https://github.com/shadowscythe03/projects/tree/main/m-PainAttnNet'
---

## Overview

m-PainAttnNet is a multimodal extension of the PainAttnNet model for automated pain intensity classification using physiological signals. The model fuses three modalities—ECG (electrocardiogram), EMG (electromyography), and EDA (electrodermal activity)—through attention mechanisms to achieve robust pain level inference across different experimental sessions.

## Problem Statement

Pain assessment is crucial for medical diagnosis and treatment, but traditional methods rely on subjective self-reporting. Automated pain classification using physiological signals offers an objective alternative. The challenge lies in:
- Fusing heterogeneous physiological signals effectively
- Maintaining performance across different recording sessions
- Classifying pain into multiple intensity levels (not just binary)

## Technical Approach

### Architecture Components

1. **Multi-Scale Convolutional Network (MSCN)**:
   - Extracts features at three temporal scales (short, medium, long)
   - Processes 1D physiological signals with varying frequency characteristics
   - Dropout regularization (0.4-0.5) for robustness

2. **Squeeze-and-Excitation ResNet (SEResNet)**:
   - Channel-wise attention for feature recalibration
   - Residual connections for gradient flow
   - Reduces feature dimensionality to 30 channels

3. **Transformer Encoder**:
   - 2-stack encoder with 6 attention heads
   - Multi-head self-attention for temporal dependencies
   - Layer normalization and feed-forward networks

### Multimodal Fusion Strategies

- **Early Fusion**: Concatenate modalities before MSCN
- **Late Fusion**: Process each modality independently, then combine at the final layer
- **Attention Fusion**: Learn weighted combinations of modality-specific features

### Ablation Study

Evaluated four architecture variants:
1. **MSCN Only**: Baseline multi-scale convolution
2. **MSCN + SE**: Added channel attention
3. **MSCN + Transformer**: Added temporal attention
4. **Full (m-PainAttnNet)**: Complete architecture

## Dataset

**BioVid Heat Pain Database**:
- 87 participants
- 5 pain levels (0-4): No pain, Low, Medium, High, Very High
- Synchronized recordings of ECG, EMG (trapezius, corrugator, zygomaticus), EDA
- Multiple sessions per participant for cross-session evaluation

## Results

### Classification Performance

| Architecture | Modality | Accuracy | F1-Score | Precision | Recall |
|-------------|----------|----------|----------|-----------|---------|
| MSCN | ECG+EMG+EDA | 70.2% | 70.7% | 70.2% | 70.0% |
| MSCN+SE | ECG+EMG+EDA | **98.8%** | **98.8%** | **98.8%** | **98.8%** |
| Full Model | ECG+EMG+EDA | 97.1% | 97.1% | 97.1% | 97.1% |

### Key Findings

1. **SE-ResNet Impact**: Adding channel attention improved accuracy by ~28%
2. **Modality Contribution**: All three modalities contributed to performance
3. **Cross-Session Robustness**: Model maintained >75% accuracy across different sessions
4. **Ablation Insights**: SE-ResNet provided the largest performance gain

### Modality Ablation

- **ECG Only**: 96.8% accuracy
- **ECG + EMG**: 97.2% accuracy  
- **ECG + EMG + EDA**: 98.8% accuracy (best)

## Technical Stack

- **Framework**: PyTorch
- **Libraries**: NumPy, SciPy, Scikit-learn, Pandas
- **Models**: Custom CNN, ResNet, Transformer
- **Evaluation**: K-fold cross-validation, stratified sampling
- **Environment**: Google Colab with GPU acceleration

## Key Contributions

1. Extended PainAttnNet to multimodal setting with 3 physiological signals
2. Implemented comprehensive ablation study across architecture components
3. Evaluated both early and late fusion strategies
4. Demonstrated importance of channel attention (SEResNet) for physiological signals
5. Achieved near-perfect accuracy (98.8%) on 5-class pain classification

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Signal heterogeneity | Multi-scale convolutional processing |
| Class imbalance | Stratified sampling + weighted loss |
| Cross-session variance | Data augmentation + dropout regularization |
| Feature alignment | Attention mechanisms for adaptive fusion |

## Implementation Highlights

```python
# Key architecture blocks
- MSCN: Multi-scale temporal feature extraction
- SENet: Channel-wise feature recalibration  
- Transformer: Temporal dependency modeling
- Fusion: Early/late modality integration
```

## Future Work

- Extend to continuous pain monitoring (regression)
- Test on additional physiological modalities (e.g., fNIRS, fMRI)
- Deploy as real-time pain monitoring system
- Investigate explainability through attention visualization
- Cross-database validation for generalization

## Course Context

**Course**: CS6530 - Advanced Topics in AI  
**Institution**: IIT Hyderabad  
**Instructor**: Prof. Nagarajan Ganapati  
**Duration**: January 2024 - April 2024

## Resources

- [GitHub Repository](https://github.com/shadowscythe03/projects/tree/main/m-PainAttnNet)
- [Project Presentation](https://github.com/shadowscythe03/projects/tree/main/m-PainAttnNet/G-15_Final_Presentation.pptx)
- [Project Report](https://github.com/shadowscythe03/projects/tree/main/m-PainAttnNet/G-15_Final_Project_Draft_Abhiroop.pdf)
- [Original PainAttnNet Paper](https://www.frontiersin.org/journals/physiology/articles/10.3389/fphys.2023.1294577/full)
