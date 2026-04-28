---
id: 02-line-a1b2
tags: [agentic-ai, 02_Mathematics, regression]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Linear Regression Mechanics

> [!ABSTRACT]
> Linear Regression is a model that makes a prediction by computing a weighted sum of the input features plus a constant called the bias term. Training this model involves finding the parameters that minimize the Mean Squared Error (MSE) over the training set.

## 🧠 Intuition First
- Imagine you're trying to predict the price of a house. You look at its size (feature 1) and the number of bedrooms (feature 2). You give each feature a "weight" (e.g., $200 per sq ft) and add a base price (bias). The result is your predicted price. Training is the process of adjusting those weights until your predictions are as close as possible to the actual historical prices.

## 🎯 Why This Matters
- Problem it solves: Provides a simple, interpretable baseline for predicting continuous values.
- Real-world usage: Predicting sales revenue, estimating physical properties, or baseline financial modeling.

## 🧩 Glossary
- [[Bias Term]] : The constant value added to the weighted sum (also called the intercept).
- [[Feature Weights]] : The coefficients ($\theta_1, \theta_2, ...$) that determine the importance of each feature.
- [[MSE]] : Mean Squared Error. The average of the squared differences between predictions and actual targets.
- [[Vectorized Form]] : A compact way to write the model equation using matrix multiplication.

## ⚙️ Mechanics (First Principles)
### The Model Equation:
$\hat{y} = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \dots + \theta_n x_n$
- $\hat{y}$ is the predicted value.
- $n$ is the number of features.
- $x_i$ is the $i^{th}$ feature value.
- $\theta_j$ is the $j^{th}$ model parameter (including the bias $\theta_0$).

### Vectorized Form:
$\hat{y} = h_{\boldsymbol{\theta}}(\mathbf{x}) = \boldsymbol{\theta}^T \mathbf{x}$
- $\boldsymbol{\theta}$ is the model's parameter vector.
- $\mathbf{x}$ is the instance's feature vector (with $x_0 = 1$ for the bias).

## 📐 Mathematical Foundations
- **MSE Cost Function:**
  $MSE(\mathbf{X}, h_{\boldsymbol{\theta}}) = \frac{1}{m} \sum_{i=1}^{m} (\boldsymbol{\theta}^T \mathbf{x}^{(i)} - y^{(i)})^2$
- **Training Goal:** Find $\boldsymbol{\theta}$ that minimizes $MSE(\boldsymbol{\theta})$.

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.linear_model import LinearRegression
lin_reg = LinearRegression()
lin_reg.fit(X, y)
# Bias term and weights
print(lin_reg.intercept_, lin_reg.coef_)
```

## 🧪 Experiments
1. **Manual Prediction:** Take the learned `intercept_` and `coef_` from a model and manually calculate the prediction for a new instance using the dot product formula. Compare it to `model.predict()`.

## ⚠️ Constraints & Pitfalls
- **Linearity Assumption:** Assumes a straight-line relationship exists. If the data is curved, the model will underfit.
- **Outlier Sensitivity:** Because MSE squares the errors, large outliers can pull the model away from the majority of the data.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[Polynomial_Regression]]
- Related to → [[Regression_Metrics]]
---
(MINIMUM 3 links)
