---
id: 05-pcan-a1b2
tags: [agentic-ai, 05_Optimization, dimensionality-reduction]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Choosing PCA Dimensions

> [!ABSTRACT]
> Instead of arbitrarily choosing the number of dimensions, it is better to select the number of principal components that preserve a specific ratio of the dataset's variance (e.g., 95%). This can be determined by analyzing the explained variance ratio or by tuning the number of dimensions as a hyperparameter for downstream tasks.

## 🧠 Intuition First
- Imagine you're packing a suitcase. You want to bring as much as possible but you have a weight limit. You start with your most important items (high variance). You keep adding items until you have "95% of what you need." You don't know the exact number of items beforehand; you just know when you've reached enough "usefulness."

## 🎯 Why This Matters
- Problem it solves: Balances the trade-off between computational speed (fewer dimensions) and information retention (more dimensions).
- Real-world usage: Compressing MNIST digits from 784 pixels to ~154 components while keeping 95% of the visual information.

## 🧩 Glossary
- [[Explained Variance Ratio]] : The proportion of the dataset's total variance that lies along each principal component.
- [[Elbow Plot]] : A plot of cumulative explained variance vs. number of dimensions. The "elbow" is the point where adding more dimensions yields diminishing returns.
- [[Reconstruction Error]] : The mean squared distance between the original data and its compressed-then-decompressed version.

## ⚙️ Mechanics (First Principles)
### The 3 Strategies:
1. **Variance Ratio:** Set a target (e.g., 0.95) and calculate how many components are needed to sum to that value.
2. **Elbow Method:** Plot the cumulative sum of `explained_variance_ratio_` and look for the point where the curve stops growing fast.
3. **Hyperparameter Tuning:** Wrap PCA and a classifier in a pipeline and use `GridSearchCV` or `RandomizedSearchCV` to find the $d$ that results in the best classification performance.

## 📐 Mathematical Foundations
- **Cumulative Variance:**
  $V_{total}(d) = \sum_{i=1}^{d} \text{explained\_variance\_ratio}_i$

## 💻 Implementation
- Preserving 95% variance in Scikit-Learn:
```python
from sklearn.decomposition import PCA

# Set n_components to a float between 0.0 and 1.0
pca = PCA(n_components=0.95)
X_reduced = pca.fit_transform(X_train)

# Check how many components were actually kept
print(pca.n_components_)
```

## 🧪 Experiments
1. **The Grid Search Test:** Use `RandomizedSearchCV` on a pipeline of `PCA` + `RandomForest`. Observe that the "optimal" number of components might be much lower (e.g., 23) than what 95% variance would suggest (e.g., 154).

## ⚠️ Constraints & Pitfalls
- **Visualization Exception:** For 2D/3D visualization, you *must* choose $d=2$ or $d=3$, regardless of the variance ratio.
- **Decompression Loss:** Decompressing using `inverse_transform()` will never perfectly recreate the original data because information was discarded.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[PCA_Mechanics]]
- Used in → [[End_to_End_Project_Checklist]]
- Related to → [[Hyperparameter_Tuning_Strategies]]
---
(MINIMUM 3 links)
