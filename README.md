# The Spatial-Spectral Bottleneck

### How Local Attention Constraints Amplify Color Shortcuts in Convolutional Neural Networks

This repository contains the implementation, experimental configurations, results, and research paper for the study of the **Spatial-Spectral Bottleneck**, a phenomenon observed in convolutional neural networks trained on color-biased data.

## Overview

Neural networks can exploit spurious correlations such as color, texture, or background instead of learning meaningful object features. This work investigates whether spatial attention regularization can effectively suppress color-based shortcut learning.

The experiments demonstrate that restricting spatial attention alone can backfire: although border activation is reduced, the model can increase its reliance on spectral/color information.

A spectral color-invariance constraint substantially improves out-of-distribution (OOD) performance, while the combined spatial + spectral constraint simultaneously addresses both pathways.

## Experimental Setup

The experiments use a color-biased version of CIFAR-10.

- Dataset: Colored CIFAR-10
- Training samples: 50,000
- OOD test samples: 10,000
- Image size: 32 × 32
- Batch size: 128
- Optimizer: Adam
- Learning rate: 0.001
- Training epochs: 71
- Random seed: 42

All four experimental models use the same CNN architecture so that differences in performance can be attributed to the applied loss constraints.

## Experimental Models

| Model | λs | λc | Active Constraints |
|---|---:|---:|---|
| Baseline | 0.0 | 0.0 | None |
| Spatial-only | 1.0 | 0.0 | Spatial |
| Spectral-only | 0.0 | 2.5 | Spectral |
| Synergistic | 1.0 | 2.5 | Spatial + Spectral |

The combined objective is:

`L = L_cls + λs L_spatial + λc L_color`

## Key Results

| Model | Train Accuracy | OOD Accuracy | OOD Δ | Color Confused |
|---|---:|---:|---:|---:|
| Baseline CNN | 99.97% | 43.36% | — | 26.19% |
| Spatial-only | 99.84% | 36.48% | −6.88% | 30.29% |
| Spectral-only | 99.80% | 59.30% | +15.94% | 6.71% |
| Synergistic | 99.68% | 56.62% | +13.26% | 6.86% |

### Main Finding

Spatial-only regularization reduces spatial border activation but worsens OOD performance and increases color confusion.

The spectral-only constraint achieves the highest OOD accuracy and lowest color confusion among the four experimental conditions.

The results support the **Spatial-Spectral Bottleneck** hypothesis: restricting one shortcut pathway can cause the network to increase its reliance on another available pathway.

## Repository Structure

```text
spatial-spectral-bottleneck/
│
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── figures/
├── notebooks/
└── research paper/

## Reproducibility

The complete experimental implementation is provided in:

**[`notebooks/spatial_spectral_bottleneck_experiments.ipynb`](notebooks/spatial_spectral_bottleneck_experiments.ipynb)**

The notebook includes:

- Dataset preparation
- CNN architecture
- Spatial attention constraint
- Spectral color-invariance constraint
- Training procedure
- Evaluation metrics
- Experimental comparisons
- Visualization and Grad-CAM analysis

The CIFAR-10 dataset is downloaded programmatically during notebook execution and is **not included** in this repository.

---

## Research Paper

The complete research paper is available here:

**[`spatial_spectral_bottleneck.pdf`](research paper/spatial_spectral_bottleneck.pdf)**

> *The Spatial-Spectral Bottleneck: How Local Attention Constraints Amplify Color Shortcuts in Convolutional Neural Networks*

---

##  Authors

**Aditya Jhamnani**  
**Sarim Kazmi**  
**Dr. Monica Tolani**  
**Gunjan Gyanchandani**  
**Hemang Ganjsinghani**

**Department of Artificial Intelligence and Data Science**  
**Thadomal Shahani Engineering College**