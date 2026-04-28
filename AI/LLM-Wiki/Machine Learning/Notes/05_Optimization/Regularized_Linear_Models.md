---
id: 05-regu-a1b2
tags: [agentic-ai, 05_Optimization, linear-regression]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Regularized Linear Models

> [!ABSTRACT]
> Regularization reduces overfitting by constraining model weights. For linear models, this is achieved by adding a penalty term to the cost function. The three main types are Ridge Regression ($\ell_2$), Lasso Regression ($\ell_1$), and Elastic Net (a combination of both).

## 🧠 Intuition First
- Imagine you're fitting a curve to data points. 
- **Unregularized:** You let the curve wiggle as much as it wants to hit every point perfectly. This leads to a messy, complex line (overfitting).
- **Regularized:** You add a "leash" to the curve. Every time the curve wiggles too much (weights get large), it gets penalized. This forces the model to stay simpler and smoother.

## 🎯 Why This Matters
- Problem it solves: Prevents models with many features from over-reacting to noise in the training set.
- Real-world usage: Handling high-dimensional data where many features may be redundant or irrelevant.

## 🧩 Glossary
- [[Ridge Regression]] : Adds an $\ell_2$ penalty (square of weights) to the cost function. Also called Tikhonov regularization.
- [[Lasso Regression]] : Adds an $\ell_1$ penalty (absolute value of weights). Tends to eliminate weights of least important features (feature selection).
- [[Elastic Net]] : A middle ground between Ridge and Lasso, controlled by a mix ratio $r$.
- [[Hyperparameter Alpha]] : Controls the strength of regularization. $\alpha=0$ is plain linear regression.

## ⚙️ Mechanics (First Principles)
### The 3 Regularizers:
1. **Ridge ($\ell_2$):** $J(\boldsymbol{\theta}) = MSE(\boldsymbol{\theta}) + \alpha \frac{1}{m} \sum_{i=1}^{n} \theta_i^2$. 
    - *Effect:* Weights stay small but rarely reach exactly zero.
2. **Lasso ($\ell_1$):** $J(\boldsymbol{\theta}) = MSE(\boldsymbol{\theta}) + \alpha \sum_{i=1}^{n} |\theta_i|$. 
    - *Effect:* Performs automatic feature selection by setting unimportant weights to zero.
3. **Elastic Net:** $J(\boldsymbol{\theta}) = MSE(\boldsymbol{\theta}) + r\alpha \sum_{i=1}^{n} |\theta_i| + \frac{1-r}{2}\alpha \sum_{i=1}^{n} \theta_i^2$.

### When to use which?
- **Ridge:** Generally the default.
- **Lasso:** If you suspect only a few features are actually useful.
- **Elastic Net:** Preferred over Lasso when features are highly correlated or when the number of features is greater than training instances.

## 📐 Mathematical Foundations
- **Weight Vector Norms:**
  - $\ell_1$ norm: $\|\mathbf{w}\|_1$
  - $\ell_2$ norm: $\|\mathbf{w}\|_2$ (Euclidean)

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.linear_model import Ridge, Lasso, ElasticNet

ridge_reg = Ridge(alpha=0.1, solver="cholesky")
lasso_reg = Lasso(alpha=0.1)
elastic_net = ElasticNet(alpha=0.1, l1_ratio=0.5)
```

## 🧪 Experiments
1. **The Zero Test:** Train Lasso on a dataset with 10 features, where 8 are just random noise. Observe that Lasso sets the weights of the noise features to exactly zero.

## ⚠️ Constraints & Pitfalls
- **Feature Scaling:** Regularization is extremely sensitive to feature scales. Always use `StandardScaler` first.
- **Bias-Variance Trade-off:** Increasing $\alpha$ reduces variance (less overfitting) but increases bias (more underfitting).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Linear_Regression_Mechanics]]
- Used in → [[Bias_And_Variance]]
- Related to → [[Early_Stopping]]
---
(MINIMUM 3 links)
