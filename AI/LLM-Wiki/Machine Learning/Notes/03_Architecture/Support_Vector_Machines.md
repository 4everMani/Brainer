---
id: 03-svma-m3n4
tags: [agentic-ai, 03_Architecture, svm]
source: 0812_Machine-Learning-for-Absolute-Beginners.pdf
date: 2026-04-22
type: technical-note
---

# Support Vector Machines (SVM)

> [!ABSTRACT]
> Support Vector Machines (SVM) are supervised learning models used for classification and regression. SVM finds the optimal hyperplane that maximizes the "margin" (distance) between two classes of data points, ensuring a robust decision boundary that generalizes well to new data.

## 🧠 Intuition First
- Imagine a road separating two fields of flowers: red roses and white lilies. A simple path might separate them, but if it's too close to one side, a new white lily might grow on the "wrong" side of the path. SVM tries to build the widest possible highway between the two fields. The edges of this highway are supported by the flowers closest to the middle (the support vectors).

## 🎯 Why This Matters
- Problem it solves: Creating a clear decision boundary even in high-dimensional spaces or when data is not linearly separable.
- Real-world usage: Face detection, categorization of images, and bioinformatics (e.g., protein classification).

## 🧩 Glossary
- [[Hyperplane]] : A decision boundary that separates different classes (a line in 2D, a plane in 3D).
- [[Margin]] : The distance between the hyperplane and the nearest data points from either class.
- [[Support Vectors]] : The data points that lie closest to the decision boundary and define the margin.

## ⚙️ Mechanics (First Principles)
- **Identify Boundary:** Calculate potential hyperplanes that separate the classes.
- **Maximize Margin:** Select the hyperplane that has the largest distance to any support vector from either class.
- **Soft Margin (Slack):** Introduce a hyperparameter (C) to allow some misclassifications if it results in a better overall boundary (handling outliers).
- **Kernel Trick:** For non-linear data, map points to a higher-dimensional space where a linear boundary can separate them.

## 📐 Mathematical Foundations
- The decision function is typically defined as:
$$f(x) = \text{sign}(w \cdot x + b)$$
- Where $w$ is the weight vector and $b$ is the bias.

## 💻 Implementation
- Minimal working example using Scikit-Learn:
```python
from sklearn import svm
import numpy as np

# X: height, weight, y: class (0 or 1)
X = np.array([[2, 2], [2, 3], [8, 8], [8, 9]])
y = np.array([0, 0, 1, 1])

# Initialize SVM with a linear kernel
model = svm.SVC(kernel='linear', C=1.0)
model.fit(X, y)

# Predict for a new point
prediction = model.predict([[5, 5]])
```

## 🧪 Experiments
1. **The Kernel Swap:** Try training an SVM on a circular "donut" dataset using a 'linear' kernel versus an 'rbf' (radial basis function) kernel and observe the difference in accuracy.
2. **C-Parameter Tuning:** Vary the value of C from 0.01 to 1000. Observe how a small C creates a "softer" wide margin (more errors allowed) and a large C creates a "hard" narrow margin (strictly separating training points).

## ⚠️ Constraints & Pitfalls
- **Training Time:** SVMs can be computationally expensive on very large datasets.
- **Sensitivity to Scaling:** Features must be scaled (standardized) because SVM relies on calculating distances.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Logistic_Regression]]
- Used in → [[Image_Recognition]]
- Related to → [[Kernel_Methods]]
