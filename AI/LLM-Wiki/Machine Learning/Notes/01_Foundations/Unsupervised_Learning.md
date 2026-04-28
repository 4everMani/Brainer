---
id: 01-unsu-c3d4
tags: [agentic-ai, 01_Foundations, unsupervised-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Unsupervised Learning

> [!ABSTRACT]
> Unsupervised learning is a machine learning category where algorithms analyze unlabeled data to discover hidden patterns. It includes tasks like clustering, visualization, dimensionality reduction, anomaly detection, and association rule learning.

## 🧠 Intuition First
- Imagine being given a pile of mixed coins from different countries and time periods without being told what they are. You would naturally start grouping them based on similarities like size, weight, color, or the symbols stamped on them. You wouldn't know their names or values, but you would successfully organize them into meaningful clusters.

## 🎯 Why This Matters
- Problem it solves: Finding structure in large, unstructured datasets where labeling is impractical or impossible.
- Real-world usage: Customer segmentation, dimensionality reduction for faster training, and fraud detection (anomaly detection).

## 🧩 Glossary
- [[Unlabeled Data]] : Data points that lack a pre-defined target or categorical label.
- [[Clustering]] : The process of grouping data points based on their similarities.
- [[Visualization]] : Creating 2D or 3D representations of complex data to identify patterns.
- [[Dimensionality Reduction]] : Simplifying data by merging correlated features without losing too much information.
- [[Anomaly Detection]] : Identifying unusual data points that differ significantly from the "normal" training instances.
- [[Association Rule Learning]] : Discovering interesting relations between attributes in large datasets (e.g., people who buy BBQ sauce also buy steak).

## ⚙️ Mechanics (First Principles)
- **Data Input:** Feed a dataset consisting only of input variables (X).
- **Pattern Identification:** The algorithm analyzes features to find underlying relationships, distances, or density regions.
- **Tasks:**
    - **Visualization:** Preserves structure in a lower-dimensional space for plotting (e.g., t-SNE).
    - **Feature Extraction:** A type of dimensionality reduction that merges multiple correlated features into one.
    - **Anomaly vs. Novelty Detection:** Anomaly detection identifies outliers in a "normal" dataset; novelty detection identifies instances that differ from a "clean" training set.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Minimal working example using Scikit-Learn (K-Means):
```python
from sklearn.cluster import KMeans
import numpy as np

# Unlabeled data points
X = np.array([[10, 2], [12, 3], [10, 1], [30, 8], [32, 9], [31, 7]])

# Initialize model to find 2 clusters
model = KMeans(n_clusters=2)
model.fit(X)

# See which cluster each point belongs to
labels = model.labels_
```

## 🧪 Experiments
1. **Dimensionality Reduction:** Use PCA or t-SNE to reduce a dataset to 2D and plot it to see if clusters naturally emerge.
2. **Anomaly Detection:** Train an isolation forest on a "clean" dataset and see if it can identify manually injected outliers.

## ⚠️ Constraints & Pitfalls
- **Subjectivity:** Validation is harder because there are no "correct" labels.
- **Scaling Sensitivity:** Many algorithms (like clustering) are sensitive to feature scales.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[K_Means_Clustering]]
- Related to → [[Supervised_Learning]]
