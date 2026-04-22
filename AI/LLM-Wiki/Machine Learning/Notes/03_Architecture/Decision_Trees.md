---
id: 03-dtree-q7r8
tags: [agentic-ai, 03_Architecture, decision-trees]
source: 0812_Machine-Learning-for-Absolute-Beginners.pdf
date: 2026-04-22
type: technical-note
---

# Decision Trees

> [!ABSTRACT]
> A Decision Tree is a supervised learning algorithm that works by recursively splitting a dataset into smaller subsets based on the most significant features. It creates a flowchart-like structure where each internal node represents a test on an attribute, and each leaf node represents a final decision or outcome.

## 🧠 Intuition First
- Imagine playing a game of "20 Questions." You start with a broad question (e.g., "Is it an animal?") to eliminate half the possibilities. Then you ask more specific questions based on the previous answer ("Does it have wings?") until you narrow down the specific item. A decision tree does exactly this with data.

## 🎯 Why This Matters
- Problem it solves: Making complex decisions through a series of simple, logical steps that are easy for humans to understand and visualize.
- Real-world usage: Loan approval (Yes/No based on credit score and income), medical diagnosis, and predicting customer churn.

## 🧩 Glossary
- [[Entropy]] : A measure of disorder or uncertainty in a dataset.
- [[Information Gain]] : The reduction in entropy achieved by splitting the data on a specific attribute.
- [[Root Node]] : The starting point of the tree containing the entire dataset.

## ⚙️ Mechanics (First Principles)
- **Select Feature:** Calculate Information Gain (or Gini Impurity) for all features to find the one that best separates the classes.
- **Split Data:** Divide the dataset into subsets based on the values of the chosen feature.
- **Recursive Branching:** Repeat the process for each subset, creating new nodes and branches.
- **Leaf Assignment:** Stop splitting when a branch is pure (all points belong to one class) or a pre-defined depth limit is reached.

## 📐 Mathematical Foundations
- Entropy Formula:
$$H(S) = -\sum_{i=1}^{c} p_i \log_2(p_i)$$
- Where $p_i$ is the probability of class $i$ in dataset $S$.

## 💻 Implementation
- Minimal working example using Scikit-Learn:
```python
from sklearn.tree import DecisionTreeClassifier
import numpy as np

# X: outlook (0: sunny, 1: overcast), humidity (0: high, 1: normal)
# y: play tennis (0: no, 1: yes)
X = np.array([[0, 0], [0, 0], [1, 0], [1, 1], [0, 1]])
y = np.array([0, 0, 1, 1, 1])

model = DecisionTreeClassifier()
model.fit(X, y)

# Predict if we play tennis when sunny and normal humidity
prediction = model.predict([[0, 1]])
```

## 🧪 Experiments
1. **Pruning:** Train a tree to full depth and then use the `max_depth` parameter to limit it. Compare the accuracy on test data to see if the simpler tree generalizes better.
2. **Feature Importance:** Use `model.feature_importances_` to see which input variables had the most impact on the final decision structure.

## ⚠️ Constraints & Pitfalls
- **Overfitting:** Decision trees can easily create overly complex structures that fit the training data perfectly but fail on new data.
- **Instability:** Small changes in the data can result in a completely different tree structure being generated.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Supervised_Learning]]
- Used in → [[Ensemble_Modeling]]
- Related to → [[Random_Forests]]
