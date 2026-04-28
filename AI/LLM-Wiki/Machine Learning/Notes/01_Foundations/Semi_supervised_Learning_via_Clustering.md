---
id: 01-semi-c1d2
tags: [agentic-ai, 01_Foundations, clustering]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Semi-supervised Learning via Clustering

> [!ABSTRACT]
> Clustering can be a powerful preprocessing step for semi-supervised learning. By identifying representative instances (centroids) and using "label propagation," we can train accurate models on mostly unlabeled data. Active learning further enhances this by iteratively requesting labels for the most informative instances.

## 🧠 Intuition First
- Imagine you have 10,000 photos of animals. You don't have time to label them all. 
- **Representative Instances:** You group them into 50 clusters. You only label the one photo that is most "central" to each group (the average animal). 
- **Label Propagation:** You assume every other photo in that cluster is the same animal. Now you have 10,000 labels for the price of 50.
- **Active Learning:** You train a model. You ask the model: "Which photo are you most confused by?" It points to one. You label it. The model gets smarter.

## 🎯 Why This Matters
- Problem it solves: Massive cost and time of manual data labeling.
- Real-world usage: Facial recognition in photo apps, medical image classification, and sentiment analysis.

## 🧩 Glossary
- [[Representative Images]] : The instances in a cluster that are closest to the centroid.
- [[Label Propagation]] : Assigning the label of a representative instance to all other instances in the same cluster.
- [[Active Learning]] : A process where the algorithm iteratively requests labels from a human for instances it is most uncertain about.
- [[Uncertainty Sampling]] : A common active learning strategy that targets instances with the lowest predicted probability.

## ⚙️ Mechanics (First Principles)
### The 3-Step Workflow:
1. **Cluster:** Run K-Means on the full unlabeled dataset.
2. **Identify & Label:** Find the $k$ instances closest to the centroids. Manually label only these representative instances.
3. **Propagate:** Assign these labels to all other members of their respective clusters. 
    - *Refinement:* Only propagate labels to the top 99% closest instances to avoid outlier contamination.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Label Propagation in Scikit-Learn:
```python
# 1. Cluster 50 representative images
kmeans = KMeans(n_clusters=50)
X_dist = kmeans.fit_transform(X_train)
representative_idx = np.argmin(X_dist, axis=0)

# 2. Manual labeling of those 50 images (y_rep)

# 3. Propagate labels to full training set
y_train_propagated = np.empty(len(X_train))
for i in range(50):
    y_train_propagated[kmeans.labels_ == i] = y_rep[i]
```

## 🧪 Experiments
1. **The Label Boost:** Train a model on 50 random labeled instances vs 50 representative instances + label propagation. Observe the significant jump in test accuracy.

## ⚠️ Constraints & Pitfalls
- **Cluster Purity:** If a cluster contains multiple classes, propagation will create many wrong labels.
- **Outlier Propagation:** If outliers aren't removed before propagation, they can bias the final model.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Clustering_Basics]]
- Used in → [[Main_Challenges_of_Machine_Learning]]
- Related to → [[Semi_supervised_Learning]]
---
(MINIMUM 3 links)
