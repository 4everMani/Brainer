---
id: 03-pcam-a1b2
tags: [agentic-ai, 03_Architecture, dimensionality-reduction]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# PCA Mechanics

> [!ABSTRACT]
> Principal Component Analysis (PCA) identifies the hyperplane that lies closest to the data and projects the data onto it. It selects the axis that preserves the maximum amount of variance, ensuring that as much information as possible is retained in the reduced space.

## 🧠 Intuition First
- Imagine you're taking a photo of a flat, floating object in a room. You want to pick an angle that captures the most detail. If you look at it from the side, it's just a thin line (low variance). If you look at it from above, you see the full shape (maximum variance). PCA is the mathematical process of finding that "top-down" angle for your high-dimensional data.

## 🎯 Why This Matters
- Problem it solves: Automates the selection of the most informative features by transforming the original features into a new, smaller set of uncorrelated components.
- Real-world usage: Compressing image data, preprocessing for machine learning to reduce noise, and noise reduction.

## 🧩 Glossary
- [[Principal Component]] : The unit vector ($\mathbf{c}_i$) that defines an axis of maximum variance in the data.
- [[SVD]] : Singular Value Decomposition. A matrix factorization technique used to find principal components.
- [[Explained Variance]] : The proportion of the dataset's total variance that lies along each principal component.
- [[Hyperplane]] : A subspace with one fewer dimension than its ambient space (e.g., a plane in 3D).

## ⚙️ Mechanics (First Principles)
### The 3 Steps of PCA:
1. **Centering:** Zero-center the data (subtract the mean).
2. **Finding PCs:** Find the axis that accounts for the largest variance. Then find a second axis, orthogonal to the first, that accounts for the remaining variance, and so on.
3. **Projection:** Select the first $d$ principal components and project the data onto the hyperplane they define.

### Singular Value Decomposition (SVD):
- Standard PCA uses SVD to decompose the data matrix $X$ into $U \Sigma V^T$. 
- The matrix $V$ contains the unit vectors of all principal components.

## 📐 Mathematical Foundations
- **Projection Equation:**
  $\mathbf{X}_{d-proj} = \mathbf{X} \mathbf{W}_d$
  Where $\mathbf{W}_d$ is the matrix containing the first $d$ principal components (columns of $V$).

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
# Automatically centers the data
X2D = pca.fit_transform(X)

# The unit vectors (PCs)
print(pca.components_)
```

## 🧪 Experiments
1. **Variance Retention:** Plot the "Explained Variance Ratio" for each component in a 10-feature dataset. Observe how many components you need to capture 95% of the total variance.

## ⚠️ Constraints & Pitfalls
- **Centering Required:** Standard PCA assumes the data is centered around the origin. Scikit-Learn handles this, but custom implementations or other libraries might not.
- **Linearity:** PCA only finds linear subspaces. If your data lies on a curved manifold, PCA will perform poorly compared to Manifold Learning techniques.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Dimensionality_Reduction_Basics]]
- Used in → [[Linear_Regression]]
- Related to → [[Support_Vector_Machines_Linear]]
---
(MINIMUM 3 links)
