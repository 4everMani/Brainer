---
id: 03-pcar-a1b2
tags: [agentic-ai, 03_Architecture, dimensionality-reduction]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Incremental and Randomized PCA

> [!ABSTRACT]
> Standard PCA requires the entire dataset to fit in memory. Incremental PCA solves this by splitting the data into mini-batches, while Randomized PCA uses a stochastic algorithm to quickly approximate the principal components, making it ideal for datasets where $d \ll n$.

## 🧠 Intuition First
- **Incremental PCA:** Imagine you're sorting a mountain of mail. Your desk is too small for the whole mountain. So, you take one basket of mail at a time, sort it, and update your master log. You never need more space than one basket.
- **Randomized PCA:** Imagine you're trying to find the tallest mountains in a range. Instead of measuring every single peak with a ruler, you take 1,000 random samples and use statistics to quickly find a very good estimate of the highest peaks. It's much faster and "good enough" for most purposes.

## 🎯 Why This Matters
- Problem it solves: PCA on datasets that exceed RAM (out-of-core learning) and speeding up dimensionality reduction for high-dimensional data.
- Real-world usage: Preprocessing massive log files or high-resolution video frames.

## 🧩 Glossary
- [[Incremental PCA]] : An algorithm that feeds the data into PCA in mini-batches.
- [[Randomized PCA]] : A stochastic algorithm that approximates the first $d$ principal components.
- [[svd_solver]] : A Scikit-Learn hyperparameter that chooses between full, incremental, or randomized SVD.

## ⚙️ Mechanics (First Principles)
### Incremental PCA (IPCA):
- **Workflow:** Split training set into $m$ mini-batches. Call `partial_fit()` for each.
- **Utility:** Perfect for online learning or very large files on disk (using `memmap`).

### Randomized PCA:
- **Computational Complexity:** $O(m \times d^2) + O(d^3)$ instead of $O(m \times n^2) + O(n^3)$ for full SVD.
- **Speed:** Drastically faster when $d$ is much smaller than $n$.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.decomposition import IncrementalPCA, PCA

# Incremental PCA
inc_pca = IncrementalPCA(n_components=154)
for batch in np.array_split(X_train, 100):
    inc_pca.partial_fit(batch)

# Randomized PCA (default when auto and d < 0.8n)
rnd_pca = PCA(n_components=154, svd_solver="randomized")
X_reduced = rnd_pca.fit_transform(X_train)
```

## 🧪 Experiments
1. **The Time Test:** Compare the training time of `svd_solver="full"` vs `svd_solver="randomized"` on a dataset with 1,000 features and 50,000 instances.

## ⚠️ Constraints & Pitfalls
- **IPCA Batch Size:** If the batch size is too small, the principal components might be unstable.
- **Randomized Reproducibility:** Because it's stochastic, you must set `random_state` for reproducible results.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[PCA_Mechanics]]
- Used in → [[Choosing_PCA_Dimensions]]
- Related to → [[Batch_vs_Online_Learning]]
---
(MINIMUM 3 links)
