---
id: 01-semi-a1b2
tags: [agentic-ai, 01_Foundations, ml-supervision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Semi-supervised Learning

> [!ABSTRACT]
> Semi-supervised learning deals with data that is partially labeled, combining a small amount of labeled data with a large amount of unlabeled data. It typically leverages unsupervised techniques to group data and supervised techniques to propagate labels.

## 🧠 Intuition First
- Imagine a photo-hosting service like Google Photos. It first clusters photos of the same person automatically (unsupervised). Then, you provide a name for that person in just one photo (supervised). The system then "propagates" that name to all other photos in the same cluster.

## 🎯 Why This Matters
- Problem it solves: High cost and time required for manual data labeling.
- Real-world usage: Facial recognition in photo apps, web content classification, and speech recognition.

## 🧩 Glossary
- [[Label Propagation]] : The process of assigning labels to unlabeled instances based on their proximity or similarity to labeled instances.
- [[Clustering-then-labeling]] : A common semi-supervised strategy where data is first grouped, then labeled based on cluster membership.

## ⚙️ Mechanics (First Principles)
- **Hybrid Approach:** Most semi-supervised algorithms are combinations of unsupervised and supervised components.
- **Workflow:**
    1. Cluster the entire dataset (labeled + unlabeled).
    2. Identify the most representative or common labels within each cluster.
    3. Label all unlabeled instances in a cluster with the majority label.
    4. Train a supervised model on the now fully-labeled dataset.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Conceptual workflow:
```python
# 1. Unsupervised step: Cluster visitors
clusters = clustering_model.fit_predict(unlabeled_data)

# 2. Supervised step: Label a few instances
labels = {visitor1: "Teenager", visitor10: "Adult"}

# 3. Propagation: Assign labels to clusters based on labeled instances
```

## 🧪 Experiments
1. **Label Scarcity:** Train a supervised model on only 1% of a labeled dataset and compare its performance to a semi-supervised model that uses the same 1% labels plus the remaining 99% as unlabeled data.

## ⚠️ Constraints & Pitfalls
- **Cluster Quality:** If the unsupervised clustering is poor, labels will be propagated incorrectly, leading to a biased or inaccurate model.
- **Label Bias:** If the initial labeled set is not representative of the whole dataset, the propagation will be flawed.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Unsupervised_Learning]]
- Used in → [[Supervised_Learning]]
- Related to → [[Self_supervised_Learning]]
