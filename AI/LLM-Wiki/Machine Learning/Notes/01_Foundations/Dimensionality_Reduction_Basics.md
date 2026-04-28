---
id: 01-dimr-a1b2
tags: [agentic-ai, 01_Foundations, dimensionality-reduction]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Dimensionality Reduction Basics

> [!ABSTRACT]
> Dimensionality reduction is the process of reducing the number of input features in a dataset while preserving its core information. This fights the "curse of dimensionality," speeds up training, and enables data visualization by focusing on lower-dimensional subspaces or manifolds.

## 🧠 Intuition First
- Imagine you're describing a person. You could list every single hair color, skin pore, and thread in their clothes (millions of features). Or, you could just say "Tall, brunette, wearing a blue shirt." You've reduced the dimensions significantly but still kept the important information to recognize them.

## 🎯 Why This Matters
- Problem it solves: The "Curse of Dimensionality"—high-dimensional spaces are sparse, making predictions unreliable and training extremely slow.
- Real-world usage: Compressing image data (MNIST), visualizing complex clusters in 2D/3D, and filtering out noise from sensor data.

## 🧩 Glossary
- [[Curse of Dimensionality]] : The phenomenon where many things behave counterintuitively in high-dimensional space (e.g., almost all points are near the border).
- [[Projection]] : Projecting high-dimensional points onto a lower-dimensional subspace (e.g., a 2D plane in a 3D space).
- [[Manifold Learning]] : Modeling the low-dimensional, twisted "shape" (manifold) on which the data lies (e.g., unrolling a Swiss roll).
- [[Manifold Hypothesis]] : The assumption that most real-world high-dimensional datasets lie close to a much lower-dimensional manifold.

## ⚙️ Mechanics (First Principles)
### The 2 Main Approaches:
1. **Projection:** Best when data lies close to a flat subspace. Perpendicular lines are drawn from the points to the subspace.
2. **Manifold Learning:** Best when the subspace is twisted or bent (like a Swiss roll). Unrolling the shape preserves local distances better than projection.

### Impact of Reduction:
- **Pros:** Faster training, smaller storage, visualization, noise removal.
- **Cons:** Information loss (like JPEG compression), more complex pipelines.

## 📐 Mathematical Foundations
- **High-Dimensional Sparsity:** In $10,000$ dimensions, the average distance between two random points in a unit hypercube is much larger than in 2D, making the data very spread out and hard to cluster.

## 💻 Implementation
- Not applicable (See specific algorithm notes like PCA or LLE)

## 🧪 Experiments
1. **The Visualization Test:** Take a 10-dimensional dataset and reduce it to 2 dimensions using PCA. Plot it and see if the original class clusters are still visible.

## ⚠️ Constraints & Pitfalls
- **Information Loss:** Always try training with the original data first; only use reduction if training is too slow or if you need visualization.
- **Task Complexity:** Reducing dimensions doesn't always make a classification task easier; if the manifold is twisted, the decision boundary might actually become more complex in the reduced space.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[PCA_Mechanics]]
- Related to → [[Main_Challenges_of_Machine_Learning]]
---
(MINIMUM 3 links)
