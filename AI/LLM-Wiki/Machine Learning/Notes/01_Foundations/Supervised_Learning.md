---
id: 01-supe-a1b2
tags: [agentic-ai, 01_Foundations, supervised-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Supervised Learning

> [!ABSTRACT]
> Supervised learning is a core machine learning category where the training set fed to the algorithm includes the desired solutions, called labels or targets. It focuses on learning the mapping from inputs (features) to outputs based on historical examples.

## 🧠 Intuition First
- Imagine learning to differentiate between apples and oranges by being shown hundreds of pictures of each, explicitly labeled "apple" or "orange." Over time, you build a mental model of their features (color, shape, texture) and can classify a new fruit correctly without being told its label beforehand.

## 🎯 Why This Matters
- Problem it solves: Automating the classification of new items or the prediction of continuous outcomes based on historical labeled data.
- Real-world usage: Estimating the selling price of a used car based on past sales data, or categorizing incoming emails as spam or not spam.

## 🧩 Glossary
- [[Labels]] : The desired solutions or categories provided in the training set (often used in classification).
- [[Target]] : The numeric value the model is trying to predict (often used in regression).
- [[Features]] : The individual attributes or predictors used as input (e.g., car mileage, age, brand).
- [[Classification]] : A task where the goal is to predict a discrete class or category (e.g., spam vs. ham).
- [[Regression]] : A task where the goal is to predict a continuous numeric value (e.g., car price).

## ⚙️ Mechanics (First Principles)
- **Data Collection:** Gather a labeled dataset where both inputs (X) and desired outputs (y) are known.
- **Model Training:** Feed the combinations of inputs and outputs into an algorithm. The algorithm learns to associate patterns in features with specific labels or targets.
- **Prediction:** Pass new, unlabeled data through the trained model to generate predicted outputs.

## 📐 Mathematical Foundations
- **Logistic Regression:** Often used for classification as it outputs the probability of belonging to a given class.
- **Linear Regression:** Used for predicting numeric values.

## 💻 Implementation
- Minimal working example using Scikit-Learn:
```python
from sklearn.linear_model import LinearRegression
import numpy as np

# X: input features (e.g., car mileage), y: output (e.g., price)
X = np.array([[50000], [80000], [20000]])
y = np.array([15000, 12000, 18000])

model = LinearRegression()
model.fit(X, y)

# Predict price for a car with 60000 miles
prediction = model.predict([[60000]])
```

## 🧪 Experiments
1. **Feature Engineering:** Try building a supervised learning model with only one independent variable versus multiple to see how accuracy improves.
2. **Algorithm Swapping:** Replace the Linear Regression model in the code snippet with a Decision Tree and compare their predictions on the same dataset.

## ⚠️ Constraints & Pitfalls
- **Labeled Data Dependency:** Requires a significant amount of accurately labeled historical data to learn effectively; manual labeling is often expensive and time-consuming.
- **Garbage In, Garbage Out:** If the training data contains errors or bias, the model will learn and replicate those flaws in its predictions.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[Linear_Regression]]
- Related to → [[Unsupervised_Learning]]
