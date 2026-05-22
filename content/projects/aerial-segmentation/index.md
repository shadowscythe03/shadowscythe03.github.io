---
title: 'Semantic Segmentation of Aerial Drone Images'
summary: 'Benchmarked UNet, DeepLabV3+, SegNet, and Swin Transformer on 4000×6000 px drone imagery across 23 semantic classes; UNet achieved best accuracy at 86.4%.'
date: 2023-11-01
authors:
  - admin
tags:
  - Computer Vision
  - Semantic Segmentation
  - Deep Learning
  - Drone Imagery
  - CNNs
  - Transformers
image:
  caption: 'Aerial Segmentation Results'
  focal_point: ''
  preview_only: false
url_code: 'https://github.com/shadowscythe03/projects/tree/main/aerial_sem_seg_FINAL_SUBMISSION'
links:
  - icon: brands/github
    name: GitHub
    url: 'https://github.com/shadowscythe03/projects/tree/main/aerial_sem_seg_FINAL_SUBMISSION'
---

A systematic benchmark of four segmentation architectures on the [Semantic Drone Dataset](http://dronedataset.icg.tugraz.at/) — 400 high-resolution aerial images (up to 4000×6000 px) with pixel-level labels across 23 urban classes. The goal: understand the accuracy–cost tradeoff across CNN and transformer approaches under real GPU memory constraints.

**Best result: UNet at 86.4% accuracy**, outperforming DeepLabV3+ (~80%), Swin Transformer (~82%), and SegNet (~75%).

## Dataset

**Semantic Drone Dataset** — 400 images, 350 train / 50 test, 23 semantic classes:

- **Structures**: building, wall, fence, bridge
- **Nature**: tree, vegetation, grass, water
- **Infrastructure**: road, sidewalk, parking, rail track
- **Objects**: car, truck, person, bicycle
- **Environment**: sky, ground, terrain

Images were downscaled to 384×512 for training due to GPU memory constraints (original 4000×6000 px).

## Architectures

| Model | Params | Accuracy | Inference |
| --- | --- | --- | --- |
| **UNet** | ~34.6M | **86.4%** | Fast |
| Swin Transformer | — | ~82% | Slow |
| DeepLabV3+ (ResNet-50) | — | ~80% | Medium |
| SegNet (VGG) | — | ~75% | Fast |

All models trained with Adam (lr=0.001), sparse categorical crossentropy, up to 500 epochs with early stopping; convergence around epoch 300–400.

**Key tradeoffs:**

- UNet's encoder–decoder with skip connections gave the best overall accuracy with fast inference.
- Swin Transformer captured finer details thanks to global attention but at high compute cost.
- SegNet was the most memory-efficient via pooling-index upsampling.
- DeepLabV3+ with ASPP is best suited for full-resolution inference when memory allows.

**Known limitation:** all models struggled with small objects (vehicles, pedestrians <60% accuracy) due to downscaling; patch-based inference at full resolution would close this gap.

## Technical Stack

TensorFlow 2.x / Keras · NumPy · OpenCV · Google Colab (T4 GPU) · TensorBoard

## Project Report

<!-- TODO: Upload your project report PDF and replace the src URL below.
     Recommended: upload as a GitHub Release asset on this repo, then use:
     https://docs.google.com/viewer?url=<raw-pdf-url>&embedded=true -->

<iframe
  src="https://docs.google.com/viewer?url=https://raw.githubusercontent.com/shadowscythe03/projects/main/aerial_sem_seg_FINAL_SUBMISSION/6-final_report.pdf&embedded=true"
  width="100%"
  height="850px"
  style="border: 1px solid #e5e7eb; border-radius: 8px; display: block; margin: 1rem 0;">
</iframe>

[Download PDF](https://raw.githubusercontent.com/shadowscythe03/projects/main/aerial_sem_seg_FINAL_SUBMISSION/6-final_report.pdf)

---

**Course**: CS5480 — Deep Learning for Vision, IIT Hyderabad (Aug–Nov 2023) · Supervised by Prof. Summohana Channapayya
