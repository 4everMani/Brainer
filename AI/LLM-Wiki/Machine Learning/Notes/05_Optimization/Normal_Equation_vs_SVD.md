---
id: 05-norm-a1b2
tags: [agentic-ai, 05_Optimization, linear-regression]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Normal Equation vs SVD

> [!ABSTRACT]
> There are two main ways to solve the Linear Regression problem analytically: the Normal Equation and the Singular Value Decomposition (SVD) approach. Both are "closed-form" solutions that directly calculate the optimal model parameters.

## 🧠 Intuition First
- Imagine you're trying to find the exact point where a ball settles at the bottom of a bowl. 
- **Normal Equation:** You use a mathematical formula to calculate the exact coordinate of the bottom in one go. 
- **SVD (Singular Value Decomposition):** You use a more complex formula that first breaks down the shape of the bowl into its fundamental geometric parts to find the bottom more reliably, even if the bowl is a strange shape (singular).

## 🎯 Why This Matters
- Problem it solves: Provides a way to train a linear regression model without the need for iterative tuning of the learning rate.
- Real-world usage: Small to medium-sized datasets where the number of features is not excessively large ($n < 100,000$).

## 🧩 Glossary
- [[Normal Equation]] : An analytical equation that directly computes the model parameters ($\boldsymbol{\hat{\theta}}$) that minimize the cost function.
- [[Pseudoinverse]] : A generalized inverse of a matrix (Moore-Penrose inverse) used in the SVD approach.
- [[SVD]] : Singular Value Decomposition. A matrix factorization technique used by Scikit-Learn's `LinearRegression` class.
- [[Singular Matrix]] : A matrix that cannot be inverted (e.g., due to redundant features).

## ⚙️ Mechanics (First Principles)
### The Normal Equation:
$\boldsymbol{\hat{\theta}} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$
- *Limitation:* If $\mathbf{X}^T \mathbf{X}$ is not invertible (singular), the equation fails.

### The SVD Approach (Scikit-Learn default):
- Uses `scipy.linalg.lstsq()` to compute the pseudoinverse $\mathbf{X}^+$.
$\boldsymbol{\hat{\theta}} = \mathbf{X}^+ \mathbf{y}$
- *Advantage:* It is more efficient ($O(n^2)$) and handles non-invertible matrices perfectly (e.g., when the number of features exceeds the number of instances).

## 📐 Mathematical Foundations
- **Computational Complexity:**
  - Normal Equation: $O(n^{2.4})$ to $O(n^3)$. 
  - SVD: $O(n^2)$. 
  - Scaling: If you double the number of features, computation time increases by roughly 4x for SVD, and 5-8x for the Normal Equation.

## 💻 Implementation
- Calculating Normal Equation with NumPy:
```python
import numpy as np
X_b = np.c_[np.ones((100, 1)), X] # Add bias x0 = 1
theta_best = np.linalg.inv(X_b.T @ X_b) @ X_b.T @ y
```

## 🧪 Experiments
1. **Redundant Feature Test:** Create a dataset where one feature is exactly double another. Try to solve using the Normal Equation (will fail due to singular matrix) vs. Scikit-Learn's `LinearRegression` (will succeed).

## ⚠️ Constraints & Pitfalls
- **High Memory Usage:** Both methods require the training set to fit into memory.
- **Large n Failure:** As the number of features ($n$) increases, these methods become extremely slow. For very large $n$, use Gradient Descent instead.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Linear_Regression_Mechanics]]
- Used in → [[Gradient_Descent_Variants]]
- Related to → [[Bias_And_Variance]]
---
(MINIMUM 3 links)
