---
id: 04-fimp-a1b2
tags: [agentic-ai, 04_Training, ensemble-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Feature Importance

> [!ABSTRACT]
> One of the most useful features of Random Forests is their ability to measure the relative importance of each feature. Scikit-Learn calculates this by measuring how much the tree nodes that use a specific feature reduce impurity on average across all trees in the forest.

## 🧠 Intuition First
- Imagine you're trying to figure out why people like a certain restaurant. You look at 100 different factors (price, location, food quality, lighting, etc.). You notice that every time a review is "Positive," the "Food Quality" score was high. In contrast, the "Lighting" score didn't seem to correlate with the review at all. "Food Quality" is therefore a high-importance feature.

## 🎯 Why This Matters
- Problem it solves: Provides an automated way to perform feature selection and understand what drives a model's predictions.
- Real-world usage: Identifying key risk factors in health data or identifying which pixels in an image are most critical for digit recognition.

## 🧩 Glossary
- [[Impurity Reduction]] : The decrease in Gini or Entropy impurity achieved by splitting a node on a particular feature.
- [[Weighted Average]] : An average where each value is multiplied by a weight (in this case, the number of samples associated with the node).
- [[Feature Selection]] : The process of selecting a subset of relevant features for use in model construction.

## ⚙️ Mechanics (First Principles)
### The Calculation:
1. **At each node:** Calculate how much the split reduced impurity.
2. **Weighting:** Multiply the reduction by the number of instances in that node.
3. **Across Trees:** Sum these weighted reductions for each feature across all trees in the Random Forest.
4. **Normalization:** Scale the results so that the sum of all feature importances equals 1.0.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Accessing importance in Scikit-Learn:
```python
from sklearn.ensemble import RandomForestClassifier

rnd_clf = RandomForestClassifier(n_estimators=500)
rnd_clf.fit(X_train, y_train)

for name, score in zip(feature_names, rnd_clf.feature_importances_):
    print(name, score)
```

## 🧪 Experiments
1. **Noise Test:** Add 5 features of purely random numbers to your dataset. Train a Random Forest and verify that these noise features have near-zero importance compared to the real features.

## ⚠️ Constraints & Pitfalls
- **High Cardinality Bias:** Random Forest feature importance can be biased towards features with many unique values (high cardinality).
- **Redundant Features:** If two features are highly correlated, the importance will be split between them, making each look less important than it truly is.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Random_Forests_and_Extra_Trees]]
- Used in → [[Main_Challenges_of_Machine_Learning]]
- Related to → [[CART_Algorithm]]
---
(MINIMUM 3 links)
