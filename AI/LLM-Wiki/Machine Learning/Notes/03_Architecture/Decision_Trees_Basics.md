---
id: 03-dtbr-a1b2
tags: [agentic-ai, 03_Architecture, classification]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Decision Trees Basics

> [!ABSTRACT]
> Decision Trees are versatile machine learning algorithms that can perform both classification and regression. They are non-parametric models that learn a sequence of if-then-else rules to predict targets, making them highly interpretable and requiring very little data preparation.

## 🧠 Intuition First
- Imagine a game of 20 Questions. Each question (e.g., "Is it bigger than a breadbox?") narrows down the possibilities. A Decision Tree is a structured version of this game, where each question is a feature threshold (e.g., "petal length $\leq$ 2.45 cm") that splits the data into two branches.

## 🎯 Why This Matters
- Problem it solves: Provides highly interpretable models that don't require feature scaling or complex mathematical assumptions about the data distribution.
- Real-world usage: Credit risk assessment, medical diagnosis, and customer segmentation.

## 🧩 Glossary
- [[Root Node]] : The top-most node where the first split occurs.
- [[Leaf Node]] : A node that does not split further and contains the final prediction.
- [[Gini Impurity]] : A measure of a node's "purity." A node is pure (Gini=0) if all its training instances belong to the same class.
- [[Non-parametric Model]] : A model where the number of parameters is not determined prior to training, allowing it to adapt closely to the data.

## ⚙️ Mechanics (First Principles)
### Making Predictions:
1. Start at the root node.
2. If the condition is met (e.g., $x_1 \leq 2$), go to the left child; else go to the right.
3. Repeat until a leaf node is reached.
4. The leaf node's most frequent class (classification) or average value (regression) is the prediction.

### Model Advantages:
- **Interpretability:** You can visualize the exact reasoning for every prediction ("White Box" model).
- **Little Preparation:** Feature scaling is not required.

### Model Limitations:
- **High Variance:** Small changes in data can result in a completely different tree.
- **Axis Sensitivity:** Splits are always perpendicular to axes, making them sensitive to data rotation.

## 📐 Mathematical Foundations
- **Gini Impurity Equation ($G_i$):**
  $G_i = 1 - \sum_{k=1}^{n} p_{i,k}^2$
  Where $p_{i,k}$ is the ratio of class $k$ instances in the $i^{th}$ node.

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.tree import DecisionTreeClassifier

tree_clf = DecisionTreeClassifier(max_depth=2)
tree_clf.fit(X, y)

# Visualizing the tree
from sklearn.tree import export_graphviz
# (generates .dot file)
```

## 🧪 Experiments
1. **The Rotation Test:** Train a tree on a simple diagonal split dataset. Then, rotate the dataset 45 degrees and retrain. Observe how much more complex the tree becomes to achieve the same result.

## ⚠️ Constraints & Pitfalls
- **Overfitting:** Left unconstrained (no `max_depth`), a tree will grow until every instance is in its own leaf (Gini=0), resulting in poor generalization.
- **Greedy Algorithm:** The CAR T algorithm makes the best split at each step but doesn't guarantee the overall optimal tree.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[CART_Algorithm]]
- Related to [[Ensemble_Modeling]]
---
(MINIMUM 3 links)
