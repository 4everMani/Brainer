---
id: 02-logi-a1b2
tags: [agentic-ai, 02_Mathematics, classification]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Logistic Regression Mechanics

> [!ABSTRACT]
> Logistic Regression (also called Logit Regression) is used to estimate the probability that an instance belongs to a particular class. If the estimated probability is greater than 50%, then the model predicts that the instance belongs to that class (binary classifier).

## 🧠 Intuition First
- Imagine you're trying to predict if an email is "Spam" based on how many exclamation marks it has. A simple line wouldn't work because it could predict "150% Spam." Logistic Regression takes that line and "squashes" it through a S-shaped curve (the sigmoid) so that every prediction is between 0% and 100%.

## 🎯 Why This Matters
- Problem it solves: Provides a calibrated probability for classification tasks, not just a hard "yes" or "no."
- Real-world usage: Credit scoring (probability of default), medical diagnosis, and click-through rate prediction.

## 🧩 Glossary
- [[Sigmoid Function]] : An S-shaped function that outputs a number between 0 and 1. Also called the **Logistic function**.
- [[Logit]] : The unnormalized score before being passed to the sigmoid function (equal to $\boldsymbol{\theta}^T \mathbf{x}$).
- [[Log Loss]] : The cost function for logistic regression, which penalizes the model heavily when it predicts a high probability for the wrong class.
- [[Decision Boundary]] : The line (or surface) where the estimated probability is exactly 50%.

## ⚙️ Mechanics (First Principles)
### The Model Equation:
$\hat{p} = \sigma(\boldsymbol{\theta}^T \mathbf{x})$
- $\sigma(t) = \frac{1}{1 + \exp(-t)}$ (Sigmoid function).

### Making Predictions:
- $\hat{y} = 1$ if $\hat{p} \geq 0.5$ (i.e., $\boldsymbol{\theta}^T \mathbf{x} \geq 0$).
- $\hat{y} = 0$ if $\hat{p} < 0.5$ (i.e., $\boldsymbol{\theta}^T \mathbf{x} < 0$).

### Decision Boundaries:
- In a 2D space with two features, the decision boundary is a straight line where $\theta_0 + \theta_1 x_1 + \theta_2 x_2 = 0$.

## 📐 Mathematical Foundations
- **Cost Function (Log Loss):**
  $J(\boldsymbol{\theta}) = -\frac{1}{m} \sum_{i=1}^{m} [y^{(i)} \log(\hat{p}^{(i)}) + (1 - y^{(i)}) \log(1 - \hat{p}^{(i)})]$
- *Note:* There is no closed-form solution to minimize this function (no Normal Equation). It must be minimized via Gradient Descent.

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.linear_model import LogisticRegression
# C is the inverse of regularization strength
log_reg = LogisticRegression(C=1.0)
log_reg.fit(X_train, y_train)

# Predict probabilities
probabilities = log_reg.predict_proba(X_new)
```

## 🧪 Experiments
1. **The Overlap Test:** Plot the iris petal widths for two species. Identify the overlap region where the model's confidence (predicted probability) is close to 50%.

## ⚠️ Constraints & Pitfalls
- **Regularization:** Scikit-Learn adds $\ell_2$ regularization by default. Tune the `C` hyperparameter (lower `C` = more regularization).
- **Mutually Exclusive:** Standard Logistic Regression only handles binary classification (though it can be used for multiclass via OvR).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Linear_Regression_Mechanics]]
- Used in → [[Softmax_Regression]]
- Related to → [[Classification_Metrics]]
---
(MINIMUM 3 links)
