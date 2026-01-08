# Generative Digit Classification and Inpainting using Gaussian Mixture Models

This repository presents a **generative modeling approach** for handwritten digit classification and image reconstruction (inpainting) on the **MNIST dataset**, where each digit class is modeled using a **Gaussian Mixture Model (GMM)** trained via the **Expectation–Maximization (EM)** algorithm.

The project demonstrates how probabilistic generative models can:
- Perform multi-class classification
- Handle missing (censored) data
- Reconstruct missing image regions using Bayesian inference

---

## 📌 Project Overview

Unlike discriminative models that directly learn decision boundaries, this project models the **class-conditional data distribution**.

Each digit class `c` is represented as a mixture of `K` Gaussian components:

P(x | y = c) = Σₖ π(c,k) · N(x; μ(c,k), Σ(c,k))

This formulation allows the model to capture multiple writing styles within the same digit class, improving robustness and interpretability.

---

## 🔧 Methodology

### 1. Generative Classification
- Each digit class is modeled using a **K-component GMM**
- Model parameters are learned using the **Expectation–Maximization (EM)** algorithm
- Classification is performed using **Bayes’ rule**, selecting the class with the highest posterior probability

### 2. Expectation–Maximization (EM)
- **E-step:** Compute soft assignments (responsibilities) of data points to mixture components
- **M-step:** Update mixture weights, means, and covariances
- Training is performed independently for each digit class

### 3. Handling Missing Pixels (Censored Data)
- Classification with missing pixels is done by **marginalizing unobserved features**
- Image reconstruction (inpainting) uses **conditional Gaussian inference**
- In the GMM setting, reconstructions are obtained as a **responsibility-weighted combination** of component-wise conditional means

---

## 📊 Experimental Results

### Classification Accuracy

| Setting | Best Accuracy |
|-------|---------------|
| Uncensored Images | **89.17%** (K = 10) |
| 50% Missing Pixels | **79.8%** (K = 20) |

### Key Observations
- Increasing the number of mixture components improves accuracy up to a point (bias–variance trade-off)
- For censored images, higher model complexity continues to improve performance
- GMMs significantly outperform single-Gaussian models in both classification and reconstruction quality

### Hybrid-K Strategy
- Simple digits (e.g., 0, 1, 6, 8) require fewer components
- Complex digits (e.g., 2, 3, 4, 5, 7, 9) benefit from higher K
- A hybrid strategy achieved **88.43% accuracy** while significantly reducing the number of parameters

---

## 🖼️ Image Reconstruction (Inpainting)

The GMM-based approach produces **sharper and more plausible reconstructions** compared to single-Gaussian models by:
- Identifying the most likely writing style (mixture component)
- Filling missing pixels using component-specific conditional means

This highlights the interpretability and robustness of **generative probabilistic models** under severe data corruption.

---

## 📁 Repository Structure

```
.
├── report
│   └── Generative_Digit_Classification_and_Inpainting.pdf
├── figures
│   ├── accuracy_uncensored.png
│   ├── accuracy_censored.png
│   └── reconstruction_examples.png
├── code
│   └── FinalCode.ipynb
└── README.md
```

