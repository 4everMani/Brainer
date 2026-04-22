---
id: 03-kmea-k1l2
tags: [agentic-ai, 03_Architecture, clustering]
source: 0812_Machine-Learning-for-Absolute-Beginners.pdf
date: 2026-04-22
type: technical-note
---

# k-Means Clustering

> [!ABSTRACT]
> k-Means Clustering is one of the most popular unsupervised learning algorithms used to divide data points into "k" number of discrete, non-overlapping groups. It iteratively assigns points to the nearest cluster center (centroid) and updates centers until the groupings stabilize.

## 🧠 Intuition First
- Imagine you have a large warehouse full of unsorted packages. You decide you want to organize them into 3 piles. You pick 3 random spots on the floor to start your piles. You take every package and put it in the pile whose center is closest. Once all packages are piled, you move the center of each pile to the actual middle of the new heap. You then re-distribute the packages based on these new centers. You repeat this until the piles stop moving.

## 🎯 Why This Matters
- Problem it solves: Uncovering hidden groupings in data without prior knowledge of labels.
- Real-world usage: Customer segmentation for targeted marketing, image compression (by grouping similar pixel colors), and document classification.

## 🧩 Glossary
- [[Centroid]] : The mathematical center of a cluster.
- [[Euclidean Distance]] : The straight-line distance used to determine proximity between a data point and a centroid.

## ⚙️ Mechanics (First Principles)
- **Initialization:** Choose "k" (number of clusters) and randomly place "k" centroids in the data space.
- **Assignment:** Assign each data point to the cluster of the nearest centroid.
- **Update:** Calculate the mean of all points in each cluster and move the centroid to this new mean position.
- **Iteration:** Repeat assignment and update steps until centroids no longer move significantly (convergence).

## 📐 Mathematical Foundations
- Euclidean Distance:
$$d = \sqrt{\sum_{i=1}^{n} (x_i - y_i)^2}$$
- The algorithm seeks to minimize the **Sum of Squared Errors (SSE)** within clusters.

## 💻 Implementation
- Minimal working example using Scikit-Learn:
```python
from sklearn.cluster import KMeans
import numpy as np

# Unlabeled data
X = np.array([[1, 2], [1, 4], [1, 0], [10, 2], [10, 4], [10, 0]])

# Initialize with 2 clusters
model = KMeans(n_clusters=2, random_state=0)
model.fit(X)

# Identify centroids and labels
centroids = model.cluster_centers_
labels = model.labels_
```

## 🧪 Experiments
1. **The Elbow Method:** Run k-Means for values of k from 1 to 10 and plot the SSE. Look for the "elbow" point where the rate of decrease significantly slows to find the optimal k.
2. **Initial Seed Impact:** Run the algorithm multiple times with different random seeds and observe if the final clusters change (use `n_init` in Scikit-Learn).

## ⚠️ Constraints & Pitfalls
- **Choosing K:** The algorithm requires you to specify the number of clusters in advance, which isn't always obvious.
- **Outlier Sensitivity:** Centroids can be pulled significantly by outliers, potentially distorting the clusters.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Unsupervised_Learning]]
- Used in → [[Customer_Segmentation]]
- Related to → [[K_Nearest_Neighbors]]
