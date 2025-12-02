---
title: 'Semantic Segmentation of Aerial Drone Images'
summary: 'Benchmarked UNet, DeepLabV3+, SegNet, and Swin Transformer architectures for high-resolution drone imagery segmentation'
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
---

## Overview

This project implements and benchmarks multiple state-of-the-art semantic segmentation architectures on high-resolution aerial drone imagery. The goal is to automatically classify each pixel in drone-captured images into 23 different categories including buildings, roads, trees, water bodies, and vehicles—enabling applications in urban planning, environmental monitoring, and autonomous navigation.

## Problem Statement

Aerial imagery from drones presents unique challenges for semantic segmentation:
- **High Resolution**: Images up to 6000×4000 pixels require memory-efficient processing
- **Small Objects**: Vehicles and pedestrians appear tiny relative to image size
- **Class Imbalance**: Some categories (e.g., sky, vegetation) dominate the dataset
- **Computational Cost**: Real-time inference needed for drone applications

## Dataset

**Semantic Drone Dataset**:
- 400 high-resolution images (typical size: 4000×6000 pixels)
- 23 semantic classes for urban/suburban scenes
- RGB images with pixel-level annotations
- Captured from drone flights over European cities
- Split: 350 training, 50 testing

### Class Distribution
Major classes include:
- **Structures**: Building, wall, fence, bridge
- **Nature**: Tree, vegetation, grass, water
- **Infrastructure**: Road, sidewalk, parking, rail track
- **Objects**: Car, truck, person, bicycle
- **Environment**: Sky, ground, terrain

## Architectures Evaluated

### 1. UNet
- **Architecture**: Encoder-decoder with skip connections
- **Resolution**: 384×512 (downscaled for memory)
- **Parameters**: ~34.6M
- **Strengths**: Fast training, good localization
- **Limitations**: Struggles with small objects

### 2. DeepLabV3+
- **Architecture**: Atrous convolutions + encoder-decoder
- **Backbone**: ResNet-50
- **Key Feature**: Atrous Spatial Pyramid Pooling (ASPP)
- **Strengths**: Multi-scale context, strong boundaries
- **Limitations**: Computationally expensive

### 3. SegNet
- **Architecture**: VGG-based encoder-decoder
- **Key Feature**: Pooling indices for upsampling
- **Strengths**: Memory efficient upsampling
- **Limitations**: Limited receptive field

### 4. Swin Transformer
- **Architecture**: Hierarchical vision transformer
- **Key Feature**: Shifted windows for efficiency
- **Strengths**: Global receptive field, fine details
- **Limitations**: High computational cost

## Implementation Details

### Preprocessing Pipeline
```python
- Input Resolution: 384×512 (from original 4000×6000)
- Normalization: [0,1] scaling
- Data Augmentation: None (kept original distributions)
- Batch Size: 16 (limited by GPU memory)
```

### Training Configuration
- **Optimizer**: Adam
- **Loss Function**: Sparse Categorical Crossentropy
- **Epochs**: 500 (with early stopping)
- **Learning Rate**: 0.001 (default Adam)
- **Framework**: TensorFlow/Keras

### Model Architecture (UNet Example)
```
Encoder: 5 blocks with [32, 64, 128, 256, 512] filters
Bottleneck: 1024 filters
Decoder: 5 upsampling blocks with skip connections
Output: 23-class softmax classifier
Dropout: [0.1, 0.2, 0.4, 0.4, 0.45] progressive regularization
```

## Results

### Quantitative Performance

| Model | Accuracy | Loss | Training Time | Inference Time |
|-------|----------|------|---------------|----------------|
| **UNet** | **86.4%** | 0.574 | Fast | Fast |
| DeepLabV3+ | ~80% | 0.642 | Slow | Medium |
| SegNet | ~75% | 0.712 | Medium | Fast |
| Swin Transformer | ~82% | 0.601 | Very Slow | Slow |

### Key Observations

1. **UNet Performance**: Achieved best accuracy (~86%) with reasonable computational cost
2. **Resolution Trade-off**: Downscaling to 384×512 was necessary for GPU memory constraints
3. **Class Imbalance**: Dominant classes (sky, vegetation) achieved >95% accuracy, while rare classes (bicycle, person) struggled (<60%)
4. **Training Dynamics**: Models converged around epoch 300-400
5. **Small Object Detection**: All models struggled with vehicles and pedestrians

### Comparative Analysis

**Model Selection Criteria**:
| Criterion | Best Model | Reasoning |
|-----------|------------|-----------|
| Accuracy | UNet | Consistent 86%+ performance |
| Speed | SegNet | Fastest inference |
| Memory | SegNet | Efficient pooling indices |
| Scalability | DeepLabV3+ | Best for full resolution |
| Fine Details | Swin Transformer | Global attention |

## Technical Stack

- **Framework**: TensorFlow 2.x, Keras
- **Libraries**: NumPy, Pandas, OpenCV, Matplotlib
- **Environment**: Google Colab with T4 GPU
- **Tools**: TensorBoard for monitoring
- **Storage**: Google Drive for dataset and models

## Key Learnings

1. **Resolution Matters**: Full-resolution inference would significantly improve small object detection
2. **Architecture Trade-offs**: No single model dominates all metrics—deployment context matters
3. **Data Augmentation**: Could improve rare class performance
4. **Class Balancing**: Weighted loss or focal loss could address imbalance
5. **Computational Constraints**: Memory limitations are primary bottleneck for aerial imagery

## Challenges Faced

| Challenge | Impact | Solution |
|-----------|--------|----------|
| High-resolution images | Out-of-memory errors | Downscaled to 384×512 |
| Class imbalance | Poor rare-class accuracy | Noted for future work |
| Long training time | Limited experiments | Used Colab Pro for faster GPUs |
| Small objects | Missed detections | Documented resolution dependency |

## Future Enhancements

1. **Full Resolution**: Implement patch-based training/inference
2. **Advanced Augmentation**: Rotation, scaling, color jittering
3. **Loss Functions**: Focal loss or weighted CE for imbalance
4. **Ensemble Models**: Combine multiple architectures
5. **Post-processing**: CRF for boundary refinement
6. **Real-time Deployment**: Model quantization and pruning

## Reproducibility

All code is available in Jupyter notebooks with:
- Clear data loading and preprocessing steps
- Model definitions with hyperparameters
- Training loops with progress monitoring
- Evaluation metrics and visualizations
- Model checkpointing for best weights

## Course Context

**Course**: CS5480 - Deep Learning for Vision  
**Institution**: IIT Hyderabad  
**Instructor**: Prof. Summohana Channapayya  
**Duration**: August 2023 - November 2023

## Resources

- [GitHub Repository](https://github.com/shadowscythe03/projects/tree/main/aerial_sem_seg_FINAL_SUBMISSION)
- [Semantic Drone Dataset](http://dronedataset.icg.tugraz.at/)
- [Colab Notebooks](#) (Available in repo)

---

**Impact**: This project demonstrates the feasibility of automated aerial image understanding for urban planning and environmental monitoring, while highlighting the computational challenges of deploying such systems on resource-constrained drone platforms.
