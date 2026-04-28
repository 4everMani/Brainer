---
id: 05-gdev-a1b2
tags: [agentic-ai, 05_Optimization, gradient-descent]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Gradient Descent Variants

> [!ABSTRACT]
> Gradient Descent is an iterative optimization algorithm that minimizes a cost function by tweaking parameters in the direction of steepest descent. The three main variants differ in the amount of data used at each step: full dataset (Batch), single instance (Stochastic), or small subset (Mini-batch).

## 🧠 Intuition First
- Imagine you're trying to find the bottom of a dark valley.
- **Batch GD:** You take a long time to look at every single point on the valley walls before taking one step. You're very steady but move very slowly.
- **Stochastic GD:** You just feel the slope under your left foot and jump. You move very fast, but you're hopping around like a maniac and might never settle at the very bottom.
- **Mini-batch GD:** You look at a small circle of ground around you and take a step. It's a balance of speed and stability.

## 🎯 Why This Matters
- Problem it solves: Optimizes models on datasets that are too large to fit in memory or have hundreds of thousands of features.
- Real-world usage: Training large-scale deep learning models on GPUs (Mini-batch) or online learning on streaming data (Stochastic).

## 🧩 Glossary
- [[Epoch]] : One full pass through the training set.
- [[Learning Schedule]] : A function that gradually reduces the learning rate to help the model settle at the minimum.
- [[Convex Function]] : A function with a single global minimum (no local minima), shaped like a bowl.
- [[Tolerance]] : A tiny number ($\epsilon$) used to stop training when the gradient becomes too small.

## ⚙️ Mechanics (First Principles)
### The 3 Variants:
1. **Batch GD:** Uses the **entire training set** to compute the gradient at each step.
    - *Pros:* Steady, stops at the minimum.
    - *Cons:* Extremely slow on large datasets; doesn't support out-of-core learning.
2. **Stochastic GD (SGD):** Uses a **single random instance** at each step.
    - *Pros:* Fast, can handle huge datasets (out-of-core), escapes local minima.
    - *Cons:* Erratic, never truly settles at the minimum (unless you use a learning schedule).
3. **Mini-batch GD:** Uses a **small random set** (batch size 10-1000) at each step.
    - *Pros:* Stable than SGD, can benefit from hardware acceleration (GPUs).
    - *Cons:* Slightly more complex to tune (batch size).

## 📐 Mathematical Foundations
- **Gradient Vector Equation:**
  $\nabla_{\boldsymbol{\theta}}MSE(\boldsymbol{\theta}) = \frac{2}{m} \mathbf{X}^T (\mathbf{X} \boldsymbol{\theta} - \mathbf{y})$
- **Gradient Descent Step:**
  $\boldsymbol{\theta}^{(next step)} = \boldsymbol{\theta} - \eta \nabla_{\boldsymbol{\theta}}MSE(\boldsymbol{\theta})$

## 💻 Implementation
- Using Scikit-Learn for SGD:
```python
from sklearn.linear_model import SGDRegressor
# penalty=None means no regularization
sgd_reg = SGDRegressor(max_iter=1000, tol=1e-5, penalty=None, eta0=0.01)
sgd_reg.fit(X, y.ravel())
```

## 🧪 Experiments
1. **Convergence Speed:** Train Batch GD and SGD on a dataset with 10,000 instances. Track the time taken to reach a certain RMSE and observe the speed difference.

## ⚠️ Constraints & Pitfalls
- **Feature Scaling:** Gradient descent requires all features to have a similar scale (e.g., via `StandardScaler`), or it will take much longer to converge.
- **Learning Rate Tuning:** If $\eta$ is too high, the model will diverge; if too low, it will be painfully slow.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Linear_Regression_Mechanics]]
- Used in → [[Learning_Rate_and_Schedules]]
- Related to → [[Normal_Equation_vs_SVD]]
---
(MINIMUM 3 links)
