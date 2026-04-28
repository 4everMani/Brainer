---
id: 06-cust-a1b2
tags: [agentic-ai, 06_Implementation, data-preparation]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Custom Transformers

> [!ABSTRACT]
> Scikit-Learn allows building custom data preparation steps using `FunctionTransformer` for simple tasks or by creating custom classes. These classes inherit from `BaseEstimator` and `TransformerMixin` to integrate seamlessly into Scikit-Learn pipelines.

## 🧠 Intuition First
- Imagine you have a Lego set with all standard pieces. You need a piece that's both a wheel and a connector. You can either take a standard wheel and glue a connector on it (`FunctionTransformer`) or you can 3D print a brand-new type of brick that fits exactly into the Lego system (`Custom Class`). This new piece will now work with all other Lego bricks perfectly.

## 🎯 Why This Matters
- Problem it solves: Automates custom feature engineering (like combining attributes or specialized cleanup) that isn't provided by standard libraries.
- Real-world usage: Creating a "Distance to Cluster Center" feature or combining multiple columns into a single ratio.

## 🧩 Glossary
- [[Duck Typing]] : A design principle where an object's suitability is determined by the presence of certain methods (like `fit` and `transform`) rather than its actual type.
- [[TransformerMixin]] : A mixin class that automatically adds the `fit_transform()` method.
- [[BaseEstimator]] : A base class that adds `get_params()` and `set_params()` for hyperparameter tuning.

## ⚙️ Mechanics (First Principles)
### The Two Approaches:
1. **`FunctionTransformer`:** For transformations that don't require training (e.g., taking the log, square root).
    - *Constraint:* The transformation must be stateless (no parameters learned from `fit()`).
2. **Custom Class:** For transformations that learn from data (e.g., standardizing using the mean of the training set).
    - *Methods needed:*
        - `__init__`: For hyperparameters (no `*args` or `**kwargs`).
        - `fit()`: Learns from data and returns `self`.
        - `transform()`: Applies the transformation.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Creating a custom class transformer:
```python
from sklearn.base import BaseEstimator, TransformerMixin

class AttrAdder(BaseEstimator, TransformerMixin):
    def __init__(self, add_total_rooms=True): # Hyperparameter
        self.add_total_rooms = add_total_rooms
        
    def fit(self, X, y=None):
        return self # No learning here
        
    def transform(self, X):
        # Perform custom logic (e.g., column ratios)
        return X_new
```

## 🧪 Experiments
1. **Pipeline Integration:** Create a custom transformer that adds a "Rooms per Household" ratio. Add it to a standard pipeline and observe if it's correctly applied during both `fit_transform` and `transform` calls.

## ⚠️ Constraints & Pitfalls
- **Parameter Naming:** Always use public instance variables for hyperparameters (no underscores) to ensure `get_params()` works correctly for cross-validation.
- **Learned Parameters:** Use trailing underscores for variables learned during `fit()` (e.g., `self.mean_`).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Scikit_Learn_API_Design]]
- Used in → [[End_to_End_Project_Checklist]]
- Related to → [[Feature_Scaling_and_Transformation]]
---
(MINIMUM 3 links)
