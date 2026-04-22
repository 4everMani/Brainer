---
id: 02-logi-g7h8
tags: [agentic-ai, 02_Mathematics, logistic-regression]
source: 0812_Machine-Learning-for-Absolute-Beginners.pdf
date: 2026-04-22
type: technical-note
---

# Logistic Regression

> [!ABSTRACT]
> Logistic regression is a statistical method used for binary classification, predicting the probability that a data point belongs to one of two categories. Despite its name, it is a classification algorithm that uses a logistic function to map any real-valued number into a value between 0 and 1.

## 🧠 Intuition First
- Imagine you are trying to predict whether a student will pass an exam based on their study hours. Instead of drawing a straight line (which could predict "150% chance of passing"), you draw an S-shaped curve. As study hours increase, the curve stays flat near zero, then suddenly rises quickly, and eventually flattens out near 100%. This curve tells you the probability of a "Pass" outcome.

## 🎯 Why This Matters
- Problem it solves: Categorizing data points into discrete groups when the relationship between features and outcomes isn't linear.
- Real-world usage: Predicting if an email is spam (1) or not spam (0), or determining if a bank loan will be approved (1) or rejected (0).

## 🧩 Glossary
- [[Sigmoid Function]] : An S-shaped function that maps any value to a range between 0 and 1.
- [[Binary Classification]] : A task where the output variable has only two possible values.

## ⚙️ Mechanics (First Principles)
- **Linear Combination:** Calculate a linear score based on input features (similar to linear regression).
- **Transformation:** Pass the linear score through the sigmoid function to get a probability.
- **Decision Boundary:** Apply a threshold (usually 0.5) to the probability. If the value is > 0.5, classify as "1"; otherwise, classify as "0".
- **Optimization:** The model's weights are adjusted to minimize the error in its probability estimates.

## 📐 Mathematical Foundations
- The Logistic (Sigmoid) Function:
$$y = \frac{1}{1 + e^{-x}}$$
- Where:
    - $y$ is the predicted probability.
    - $e$ is Euler's constant (~2.718).
    - $x$ is the linear input from features.

## 💻 Implementation
- Minimal working example using Scikit-Learn:
```python
from sklearn.linear_model import LogisticRegression
import numpy as np

# X: study hours, y: pass (1) or fail (0)
X = np.array([[1], [2], [3], [5], [6], [7]])
y = np.array([0, 0, 0, 1, 1, 1])

model = LogisticRegression()
model.fit(X, y)

# Predict probability for 4 study hours
prob = model.predict_proba([[4]])
```

## 🧪 Experiments
1. **Threshold Testing:** Change the decision threshold from 0.5 to 0.8 and observe how it affects the number of "positive" classifications.
2. **Feature Scaling:** Apply standardization to features before training and compare the model's convergence speed and accuracy.

## ⚠️ Constraints & Pitfalls
- **Independence Assumption:** Assumes that the independent variables are not highly correlated with each other (no multi-collinearity).
- **Outlier Sensitivity:** Can be influenced by extreme outliers that don't follow the general pattern of the data.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Linear_Regression]]
- Used in → [[Artificial_Neural_Networks]]
- Related to [[Support_Vector_Machines]]
