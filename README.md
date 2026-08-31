# 🛡️ Advancing Biometric Authentication: Template Reconstruction Attack Detection

<div align="center">

![Python](https://img.shields.io/badge/Python-3.9+-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-red)
![ResNet50](https://img.shields.io/badge/Model-ResNet50-green)
![Biometrics](https://img.shields.io/badge/Domain-Biometric%20Security-orange)
![Research](https://img.shields.io/badge/Type-Research%20Project-purple)

**A Hybrid Dynamic Projection Framework for Detecting Fingerprint Template Reconstruction Attacks**

</div>

---

## 📖 Overview

Biometric authentication systems are widely used in smartphones, banking applications, access control systems, and digital identity verification. However, biometric templates face a critical security threat known as **Template Reconstruction Attacks**, where attackers reconstruct original fingerprint patterns from stolen biometric templates.

This project proposes a **Hybrid Dynamic Projection-Based Detection Framework** that actively detects reconstructed fingerprint templates before they can be misused.

The framework combines:

* Deep Learning-based Feature Extraction
* Dynamic Random Projection (DRP)
* Secure Template Generation
* Projection Consistency Analysis
* Reconstruction Attack Detection

The system is capable of distinguishing between:

✅ Genuine Fingerprints

❌ Reconstructed / Synthetic Fingerprints

while maintaining high authentication accuracy.

---

# 🎯 Problem Statement

Traditional biometric systems focus on protecting templates through encryption and cancelable biometrics.

However, if an attacker successfully reconstructs a fingerprint from a stolen template, the system may still accept it as genuine.

The challenge is:

> How can we detect whether a fingerprint originates from a real user or from a reconstructed biometric template?

This project addresses that challenge by introducing a behavioral consistency-based detection mechanism.

---

# 🚀 Key Features

### 🔹 Deep Feature Extraction

* Fine-tuned ResNet-50 architecture
* Extracts robust fingerprint embeddings
* Learns ridge patterns and spoofing artifacts

### 🔹 Dynamic Random Projection (DRP)

* User-specific secure projection
* Non-invertible template generation
* Revocable biometric templates

### 🔹 Reconstruction Attack Detection

Detects:

* Synthetic fingerprints
* Reconstructed templates
* Spoofed biometric representations

### 🔹 Secure Template Storage

* Projected feature vectors stored instead of raw fingerprints
* Improved privacy and security

### 🔹 Lightweight Detection Framework

* Minimal computational overhead
* Suitable for real-time deployment

---

# 🏗️ System Architecture

```text
                    ┌─────────────────────┐
                    │ Fingerprint Image   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Preprocessing     │
                    │ Resize + Normalize  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     ResNet-50       │
                    │ Feature Extraction  │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Dynamic Random      │
                    │ Projection (DRP)    │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Protected Template  │
                    └──────────┬──────────┘
                               │
             ┌─────────────────┴─────────────────┐
             │                                   │
             ▼                                   ▼
     Enrollment Phase                 Authentication Phase
             │                                   │
             ▼                                   ▼
     Template Storage                Similarity + Detection
                                                 │
                                                 ▼
                                 Real / Reconstructed
```

---

# 📂 Dataset

### CASIA Fingerprint V5 Dataset

The project uses the CASIA fingerprint database containing approximately:

| Property     | Value   |
| ------------ | ------- |
| Total Images | ~20,000 |
| Subjects     | 501     |
| Train Split  | 80%     |
| Test Split   | 20%     |

---

## Simulated Attack Generation

To train the model against reconstruction attacks, synthetic attack samples are generated using:

* Gaussian Blur
* Brightness Modification
* Contrast Manipulation
* JPEG Compression
* Additive Gaussian Noise

These transformations simulate reconstructed fingerprint templates.

---

# 🔬 Methodology

## 1. Image Preprocessing

Each fingerprint undergoes:

```python
Resize → 224×224
Normalize → ImageNet Statistics
Augmentation → Rotation, Flip, Perspective
```

### Data Augmentation

* Random Rotation (±15°)
* Horizontal Flip
* Perspective Transformation
* Color Jitter

Benefits:

* Prevents overfitting
* Improves generalization
* Mimics real-world conditions

---

## 2. Feature Extraction using ResNet-50

A pre-trained ResNet-50 model is fine-tuned.

### Architecture Modifications

* Freeze initial layers
* Fine-tune deeper layers
* Add custom classifier head
* Dropout regularization

### Loss Function

```python
CrossEntropyLoss(
    label_smoothing=0.1
)
```

### Optimizer

```python
Adam
Learning Rate = 1e-4
```

---

## 3. Dynamic Random Projection (DRP)

The extracted embeddings are transformed using a user-specific projection matrix.

### Security Properties

#### Non-Invertibility

Original features cannot be recovered.

#### Revocability

Templates can be regenerated using a new key.

#### Diversity

Different templates generated for different applications.

#### Cross-Matching Resistance

Prevents linking templates across databases.

---

## 4. Reconstruction Attack Detection

The framework analyzes:

### Projection Consistency

Measures whether projected features behave like genuine samples.

### Correlation Preservation

Checks structural relationships within embeddings.

### Score Distribution Analysis

Identifies abnormal score patterns.

### Reconstruction Residual Analysis

Measures deviations caused by inversion attacks.

These metrics are fed into a lightweight classifier.

---

# ⚙️ Training Configuration

| Parameter         | Value             |
| ----------------- | ----------------- |
| Backbone          | ResNet-50         |
| Optimizer         | Adam              |
| Learning Rate     | 1e-4              |
| Loss Function     | Cross Entropy     |
| Label Smoothing   | 0.1               |
| Scheduler         | ReduceLROnPlateau |
| Gradient Clipping | Enabled           |
| Early Stopping    | Enabled           |
| Batch Strategy    | Balanced Sampling |

---

# 📊 Performance Metrics

The framework is evaluated using:

## Classification Metrics

* Accuracy
* Precision
* Recall
* F1-Score
* False Positive Rate (FPR)
* False Negative Rate (FNR)

## Authentication Metrics

* Genuine Acceptance Rate (GAR)
* ROC Curve
* AUC-ROC
* Equal Error Rate (EER)

## Statistical Metrics

* KS-Test
* Sensitivity Index (d')
* AUPR

---

# 🏆 Results

## Classification Report

| Class         | Precision | Recall | F1-Score |
| ------------- | --------- | ------ | -------- |
| Real          | 0.99      | 1.00   | 1.00     |
| Reconstructed | 1.00      | 0.98   | 0.99     |

### Overall Accuracy

```text
99%
```

---

## EER Comparison

| Method          | EER   | FAR   | Accuracy |
| --------------- | ----- | ----- | -------- |
| Existing Method | 2.10% | 2.15% | 97.8%    |
| Proposed Method | 1.25% | 1.30% | 99.0%    |

---

## KS-Test Comparison

| Method             | KS Score    |
| ------------------ | ----------- |
| Existing Methods   | 0.75 - 0.85 |
| Proposed Framework | 0.95        |

The higher KS score indicates superior separation between genuine and reconstructed fingerprints.

---

# 📈 Advantages

✅ High Detection Accuracy

✅ Low False Acceptance Rate

✅ Revocable Templates

✅ Real-Time Detection

✅ Enhanced Privacy Protection

✅ Lightweight Deployment

✅ Resistance to Template Reconstruction

---

# 🛠️ Technology Stack

### Programming Language

* Python

### Deep Learning Framework

* PyTorch

### Computer Vision

* OpenCV
* PIL

### Machine Learning

* Scikit-Learn

### Data Processing

* NumPy
* Pandas

### Visualization

* Matplotlib
* Seaborn

---

# 📁 Project Structure

```text
Fingerprint-Reconstruction-Detection/
│
├── dataset/
│   ├── real/
│   └── reconstructed/
│
├── models/
│   ├── resnet50_model.py
│   └── detector.py
│
├── preprocessing/
│   ├── augmentation.py
│   └── preprocessing.py
│
├── projection/
│   ├── dynamic_projection.py
│   └── template_generation.py
│
├── training/
│   ├── train.py
│   └── evaluate.py
│
├── results/
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   └── training_curves.png
│
├── requirements.txt
├── README.md
└── LICENSE
```

---

# 🔮 Future Work

* Cross-dataset evaluation
* Cross-sensor fingerprint testing
* Diffusion-based reconstruction attack detection
* Federated biometric authentication
* Privacy-preserving detection models
* Edge-device deployment optimization

---

# 👨‍💻 Authors

### Venkata Satya Koushik Devarabhotla

Department of Computer Science and Engineering
SRM University-AP


### Dilip Kumar Vallabhadas

Department of Computer Science and Engineering
Centre for Interdisciplinary Research, SRM University-AP

---

# 📜 Citation

```bibtex
@article{TemplateReconstructionDetection2025,
  title={Advancing Biometric Authentication:
  A Framework for Template Reconstruction Attack Detection},
  author={Venkata Satya Koushik Devarabhotla and Dilip Kumar Vallabhadas},
  year={2025},
  journal={Fingerprint Biometric Security Research}
}
```

---

## ⭐ If you find this project useful, consider giving it a star on GitHub and contributing to future research in secure biometric authe
