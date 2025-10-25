# Team MemeMasters @ CASE 2025 

[![Paper](https://img.shields.io/badge/Paper-ACL%20Anthology-red)](https://acl-bg.org/proceedings/2025/CASE%202025/pdf/2025.case-1.18.pdf)
[![Conference](https://img.shields.io/badge/Conference-RANLP%202025-green)](https://ranlp.org/ranlp2025/)

> **Adapting Vision-Language Models for Understanding Hate Speech in Multimodal Content**

This repository contains the code and implementation for our participation in the **Shared Task on Multimodal Hate, Humor, and Stance Detection in Marginalized Movement@CASE2025*

## 📄 Paper

**Authors:** Shruti Gurung¹, Shubham Shakya²

¹ Patan College for Professional Studies, Kathmandu, Nepal  
² Department of Computer Science and Engineering, Kathmandu University, Dhulikhel, Nepal


## 🎯 Overview

Social media memes have become powerful tools for digital communication, combining images and text to convey humor, social commentary, and sometimes harmful content. This project presents a **multimodal approach using fine-tuned CLIP models** to analyze text-embedded images across four critical subtasks:

- 🎭 **Subtask A:** Hate Speech Detection
- 🎯 **Subtask B:** Target Classification 
- 📊 **Subtask C:** Stance Detection
- 😄 **Subtask D:** Humor Detection

## 🏆 Results

Our fine-tuned CLIP model achieved strong performance across all subtasks:

| Subtask | Metric | Score |
|---------|--------|-------|
| **Hate Speech Detection** | Precision | **80%** |
| **Humor Detection** | Precision | **76%** |
| **Stance Detection** | Precision | **60%** |
| **Target Classification** | Precision | **54%** |

## 🛠️ Methodology

### Model Architecture

We built our solution around the **CLIP (Contrastive Language-Image Pre-training)** model, specifically using the `openai/clip-vit-large-patch14` variant. The architecture consists of:

- **Vision Encoder:** ViT-L/14 for image understanding
- **Text Encoder:** Transformer for text processing
- **Shared Embedding Space:** Projecting both modalities into a common space
- **Classification Head:** Lightweight fully-connected layers with ReLU activations and dropout

### Training Configuration

```python
Model Backbone: openai/clip-vit-large-patch14
Max Token Length: 77
Batch Size: 16
Epochs: 5
Optimizer: AdamW
Learning Rate (Backbone): 1e-6
Learning Rate (Classifier): 1e-5
Device: Tesla T4 GPU
Loss Function: Cross-Entropy
```

### Subtask-Specific Adaptations

- **Subtask B (Target Classification):** Applied over-sampling to handle class imbalance
- **Subtask C (Stance Detection):** Used deeper 3-layer classifier + cosine learning rate scheduler
- **Subtask D (Humor Detection):** Higher dropout rate + class-weighted loss for imbalance
- **Subtask A (Hate Speech):** Standard configuration

## 📊 Dataset

The CASE 2025 dataset focuses on text-embedded images (memes) related to marginalized movements:

| Subtask | Labels | Distribution |
|---------|--------|--------------|
| **A: Hate Speech** | Non-Hate (0), Hate (1) | 51.0% / 49.0% |
| **B: Target** | Undirected (0), Individual (1), Community (2), Organization (3) | 31.1% / 10.0% / 46.9% / 12.0% |
| **C: Stance** | Neutral (0), Support (1), Oppose (2) | 28.8% / 37.7% / 33.5% |
| **D: Humor** | No Humor (0), Humor (1) | 32.4% / 67.5% |

**Total Samples:** 4,050 text-embedded images

## 🔍 Key Findings

### Strengths
- Strong performance on **binary classification tasks** (hate speech, humor)
- Effective **multimodal fusion** of visual and textual signals
- Robust handling of **class imbalance** through targeted adaptations

### Challenges
- Difficulty distinguishing **semantically similar classes** (e.g., stance categories)
- **Context-dependent features** like sarcasm and implicit meanings remain challenging
- Performance varies with **class imbalance** in target classification


## 🙏 Acknowledgments

- CASE 2025 Workshop organizers
- RANLP 2025 conference
- OpenAI for the CLIP model
- All contributors to the Memeclip and CrisisHateMM datasets
