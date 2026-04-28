---
id: 04-cart-a1b2
tags: [agentic-ai, 04_Training, classification]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# CART Algorithm

> [!ABSTRACT]
> The Classification and Regression Tree (CART) algorithm is used to train Decision Trees. It works by greedily splitting the training set into two subsets based on a single feature and threshold to minimize impurity (classification) or mean squared error (regression).

## 🧠 Intuition First
- Imagine you're sorting a bag of mixed candies. You want each pile to be as uniform as possible. First, you might split them by color (e.g., Red vs. Not Red). Then, in each pile, you might split by shape. You keep doing this until each pile is nearly pure. You don't care if a different first choice would have been better four steps later; you just pick the best split right now.

## 🎯 Why This Matters
- Problem it solves: Automates the process of finding the most important features and the exact thresholds to use for splitting data.
- Real-world usage: Forms the foundation for powerful ensemble methods like Random Forests and Gradient Boosted Trees.

## 🧩 Glossary
- [[CART]] : Classification and Regression Tree. The algorithm that produces binary trees (each node has exactly two children).
- [[Greedy Algorithm]] : An algorithm that makes the locally optimal choice at each step with the hope of finding a global optimum.
- [[Impurity]] : A measure of how mixed the classes are in a node (Gini or Entropy).
- [[Pruning]] : Deleting unnecessary nodes after the tree is fully grown to reduce overfitting.

## ⚙️ Mechanics (First Principles)
### The Splitting Rule:
- For a feature $k$ and threshold $t_k$, search for the pair $(k, t_k)$ that produces the purest subsets, weighted by their size.
- **Stopping Conditions:**
    1. Reaches `max_depth`.
    2. Cannot find a split that reduces impurity.
    3. Node size falls below `min_samples_split`.

### Regularization Hyperparameters:
- `max_depth`: Limits the number of levels.
- `min_samples_leaf`: Minimum instances required to be in a leaf node.
- `max_leaf_nodes`: Limits the total number of leaves.

## 📐 Mathematical Foundations
- **CART Cost Function (Classification):**
  $J(k, t_k) = \frac{m_{left}}{m} G_{left} + \frac{m_{right}}{m} G_{right}$
- **CART Cost Function (Regression):**
  $J(k, t_k) = \frac{m_{left}}{m} MSE_{left} + \frac{m_{right}}{m} MSE_{right}$

## 💻 Implementation
- Fine-tuning a tree using Grid Search:
```python
from sklearn.model_selection import GridSearchCV

param_grid = {'max_depth': [2, 3, 4], 'min_samples_leaf': [1, 5, 10]}
grid_search = GridSearchCV(DecisionTreeClassifier(), param_grid, cv=5)
grid_search.fit(X_train, y_train)
```

## 🧪 Experiments
1. **The Depth Impact:** Train a tree on the moons dataset with `max_depth=None` vs `max_depth=2`. Observe the decision boundaries and compare test set accuracy to see the effect of regularization.

## ⚠️ Constraints & Pitfalls
- **Intractability:** Finding the absolute optimal tree is an NP-complete problem, which is why greedy heuristics are necessary.
- **Local Optima:** Because it is greedy, it might miss the globally best sequence of splits.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Decision_Trees_Basics]]
- Used in → [[Ensemble_Modeling]]
- Related to → [[Bias_And_Variance]]
---
(MINIMUM 3 links)
