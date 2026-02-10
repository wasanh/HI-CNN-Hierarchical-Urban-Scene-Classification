# HI-CNN-Hierarchical-Urban-Scene-Classification
A lightweight three-stage hierarchical CNN framework for efficient and scalable urban scene classification using EfficientNet-B0.

## Overview
This repository contains the implementation of **HI-CNN**, a three-stage **hierarchical convolutional neural network** designed to overcome the limitations of flat CNNs in complex urban scene classification tasks.  

Unlike traditional flat classifiers that predict all classes in a single step, HI-CNN uses a **coarse-to-fine hierarchical decision process**, improving **accuracy, scalability, and inference efficiency**.

---

## Motivation
Flat CNN architectures face several challenges:  

- Feature competition between semantically unrelated classes  
- Poor scalability when new classes are introduced  
- Inefficient inference due to full model execution for each input  
- Limited interpretability of classification decisions  

Urban scenes naturally follow a **semantic hierarchy** (e.g., vegetation vs. man-made, human-centric vs. structural), which flat models ignore. **HI-CNN explicitly models this structure**.

---

## Hierarchical Architecture
HI-CNN follows a **three-stage decision hierarchy**:

### Stage 1: Environmental Classification
- **Classes:** Vegetation vs. Man-Made  
- Vegetation is treated as a **terminal class** for early exit, reducing inference cost  

### Stage 2: Domain Refinement
- **Classes:** Human-Centric vs. Structural  
- Reduces visual ambiguity before fine-grained classification  

### Stage 3: Fine-Grained Classification
- **Human-Centric branch:** Car vs. Person  
- **Structural branch:** Building vs. Laboratory  
- Each stage is implemented as an **independent binary classifier**

---

## Model Design
- **Backbone:** EfficientNet-B0 (ImageNet pre-trained)  
- **Transfer learning** with frozen feature extractor layers  
- **Lightweight classification heads** per node  
- **Loss:** Binary cross-entropy  
- **Optimizer:** Adam  

**Advantages:**  
- Modular training  
- Incremental updates  
- Edge-device compatibility  

---

## Dataset
- **Custom urban scene dataset** collected by students at the University of Jordan  
- **Classes:** Tree, Building, Laboratory, Car, Person  
- Balanced class distribution  
- **Train/Validation/Test split:** 60% / 20% / 20%  

**Incremental Learning Extension:**  
- Added **Bus** class to Human-Centric branch  
- Only Stage-3 node retrained to demonstrate **light incremental learning**  

---

## Preprocessing & Augmentation
- **Image size:** 224 × 224  
- **Normalization:** EfficientNet `preprocess_input`  
- **Data augmentation:**  
  - Random rotation (±10°)  
  - Zoom (up to 30%)  
  - Horizontal flipping  
  - Minor spatial shifts  

---

## Experimental Setup
- **Platform:** Google Colab  
- **GPU:** Tesla T4  
- **Batch size:** 32  
- **Learning rate:** 1e−3  
- **Epochs:** up to 15  
- **Early stopping:** patience = 3  
- Each hierarchical node trained **independently**  

---

## Results
- **Overall accuracy:** 95%  
- Reduced **cross-domain confusion** compared to flat CNN baseline  
- Improved **inference efficiency** via early-exit mechanism  
- Successful **light incremental learning** without full retraining
