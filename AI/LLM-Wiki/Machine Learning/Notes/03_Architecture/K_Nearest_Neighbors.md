---
id: 03-knne-i9j0
tags: [agentic-ai, 03_Architecture, k-nearest-neighbors]
source: 0812_Machine-Learning-for-Absolute-Beginners.pdf
date: 2026-04-22
type: technical-note
---

# k-Nearest Neighbors (k-NN)

> [!ABSTRACT]
> k-Nearest Neighbors (k-NN) is a simple, instance-based learning algorithm used for both classification and regression. it works on the principle that similar data points exist in close proximity to each other in a multi-dimensional space.

## 🧠 Intuition First
- Imagine you are a new kid at school and you need to decide which clique to join. You look at the three students closest to you in the cafeteria. If two of them are "athletes" and one is a "gamer," you decide you are likely an "athlete" too. You are classifying yourself based on your nearest neighbors.

## 🎯 Why This Matters
- Problem it solves: Classifying items or predicting values based on historical proximity without needing a complex training phase.
- Real-world usage: Recommender systems (suggesting products similar to ones you've bought) or handwriting recognition.

## 🧩 Glossary
- [[k (Hyperparameter)]] : The number of nearest neighbors to consider when making a prediction.
- [[Euclidean Distance]] : The most common distance metric used to calculate the "closeness" of two points.

## ⚙️ Mechanics (First Principles)
- **Store Data:** k-NN is a "lazy learner," meaning it simply stores the entire training dataset.
- **Calculate Distance:** When a new data point arrives, the algorithm calculates the distance between it and every point in the training set.
- **Find Neighbors:** It identifies the "k" points with the smallest distances to the new point.
- **Vote/Average:**
    - For classification: The algorithm takes a majority vote among the neighbors' classes.
    - For regression: It takes the average of the neighbors' values.

## 📐 Mathematical Foundations
- Euclidean Distance formula (for 2 dimensions):
$$d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$

## 💻 Implementation
- Minimal working example using Scikit-Learn:
```python
from sklearn.neighbors import KNeighborsClassifier
import numpy as np

# X: height and weight, y: t-shirt size (0: S, 1: L)
X = np.array([[160, 60], [165, 65], [170, 70], [180, 80], [185, 85]])
y = np.array([0, 0, 0, 1, 1])

# Initialize with k=3
model = KNeighborsClassifier(n_neighbors=3)
model.fit(X, y)

# Predict size for someone 175cm and 75kg
prediction = model.predict([[175, 75]])
```

## 🧪 Experiments
1. **k-Value Optimization:** Test the model with different values of k (e.g., 1, 3, 10, 20) and observe how the decision boundary changes from complex to smooth.
2. **Distance Metrics:** Swap Euclidean distance for Manhattan distance and see if it improves classification accuracy on a specific dataset.

## ⚠️ Constraints & Pitfalls
- **Computational Cost:** Since it calculates distance to every point during prediction, it becomes extremely slow as the dataset size grows.
- **Feature Scaling:** If one feature has a much larger range than others (e.g., salary vs. age), it will unfairly dominate the distance calculation. Standardization is mandatory.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Supervised_Learning]]
- Used in → [[Recommender_Systems]]
- Related to → [[K_Means_Clustering]]
