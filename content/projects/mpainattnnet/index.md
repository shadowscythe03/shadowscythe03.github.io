---
title: 'Multimodal Pain Classification (m-PainAttnNet)'
summary: 'Extended PainAttnNet with attention-based fusion of ECG, EMG, and EDA signals, achieving 98.8% accuracy on 5-class pain intensity classification from the BioVid dataset.'
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
links:
  - icon: brands/github
    name: GitHub
    url: 'https://github.com/shadowscythe03/projects/tree/main/m-PainAttnNet'
---

Automated pain assessment using physiological signals offers an objective alternative to self-reporting. m-PainAttnNet extends [PainAttnNet](https://www.frontiersin.org/journals/physiology/articles/10.3389/fphys.2023.1294577/full) to a **multimodal setting**, fusing ECG, EMG, and EDA signals through attention mechanisms to classify pain into 5 intensity levels. Evaluated on the BioVid Heat Pain Database (87 participants).

**Key result: 98.8% accuracy on 5-class pain intensity classification**, with cross-session robustness >75%.

## Architecture

The model stacks three learned components:

1. **Multi-Scale CNN (MSCN)** — extracts temporal features at short, medium, and long scales from 1D physiological signals; dropout 0.4–0.5 for regularisation.
2. **Squeeze-and-Excitation ResNet (SEResNet)** — channel-wise attention recalibrates feature importance; residual connections maintain gradient flow; output dimensionality reduced to 30 channels.
3. **Transformer Encoder** — 2-layer encoder, 6 attention heads; captures long-range temporal dependencies with layer normalisation and feed-forward networks.

### Multimodal Fusion Strategies

Three fusion points were evaluated:

- **Early fusion**: concatenate modalities before MSCN
- **Late fusion**: process each modality independently, combine at the final layer
- **Attention fusion**: learn weighted modality combinations (best results)

## Results

### Ablation over architecture components

| Architecture | Accuracy | F1-Score |
| --- | --- | --- |
| MSCN only | 70.2% | 70.7% |
| MSCN + SEResNet | **98.8%** | **98.8%** |
| MSCN + Transformer | ~93% | ~93% |
| Full m-PainAttnNet | 97.1% | 97.1% |

SEResNet's channel attention provided the single largest accuracy jump (~28 pp). The full model trades a marginal accuracy drop for better generalisation.

### Modality ablation (full model)

| Modalities | Accuracy |
| --- | --- |
| ECG only | 96.8% |
| ECG + EMG | 97.2% |
| ECG + EMG + EDA | **98.8%** |

### Dataset

**BioVid Heat Pain Database** — 87 participants, 5 pain levels (0–4: none to very high), synchronised ECG, EMG (trapezius, corrugator, zygomaticus), and EDA recordings across multiple sessions.

## Technical Stack

PyTorch · NumPy · SciPy · Scikit-learn · K-fold cross-validation · Google Colab (GPU)

## Project Report

<iframe
  src="https://docs.google.com/viewer?url=https://raw.githubusercontent.com/shadowscythe03/projects/main/m-PainAttnNet/G-15_Final_Project_Draft_Abhiroop.pdf&embedded=true"
  width="100%"
  height="850px"
  style="border: 1px solid #e5e7eb; border-radius: 8px; display: block; margin: 1rem 0;">
</iframe>

[Download PDF](https://raw.githubusercontent.com/shadowscythe03/projects/main/m-PainAttnNet/G-15_Final_Project_Draft_Abhiroop.pdf) · [Presentation slides](https://github.com/shadowscythe03/projects/tree/main/m-PainAttnNet/G-15_Final_Presentation.pptx)

---

**Course**: CS6530 — Advanced Topics in AI, IIT Hyderabad (Jan–Apr 2024) · Supervised by Prof. Nagarajan Ganapati
