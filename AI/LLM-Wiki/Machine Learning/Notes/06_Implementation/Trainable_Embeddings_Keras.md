---
id: 06-temb-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Trainable Embeddings Keras

> [!ABSTRACT]
> Embeddings are dense, low-dimensional vector representations of categorical data. Unlike one-hot encoding, which is sparse and high-dimensional, embeddings are trainable parameters that the model learns through gradient descent. This allows the network to discover meaningful relationships between categories automatically.

## 🧠 Intuition First
- Imagine you're assigning GPS coordinates to different foods. 
- **One-hot Encoding:** Every food is at the end of its own private, infinitely long road that never crosses any other road. There is no way to say "Apple" is closer to "Orange" than to "Pizza."
- **Embeddings:** Every food gets a coordinate on a 2D map. At first, the coordinates are random. But during training, the model realizes that whenever "Apple" is the answer, "Fruit-like" ingredients are present. It moves "Apple" and "Orange" closer together on the map and moves "Pizza" far away. The model builds its own internal "map of meaning."

## 🎯 Why This Matters
- Problem it solves: Handles high-cardinality features (e.g., 50,000 words or 1,000,000 user IDs) efficiently without the memory explosion of one-hot encoding, while capturing semantic similarity.
- Real-world usage: Recommendation systems, natural language processing (word embeddings), and customer behavioral modeling.

## 🧩 Glossary
- [[Embedding]] : A dense vector of floating-point values representing a category.
- [[Embedding Layer]] : A lookup table that maps integer indices to these dense vectors.
- [[Representation Learning]] : The process where a model learns useful features (like embeddings) automatically during training.
- [[Vocabulary Size]] : The total number of unique categories plus OOV buckets.

## ⚙️ Mechanics (First Principles)
### The Process:
1. **Integer Mapping:** Convert text categories to unique integers (e.g., using `StringLookup`).
2. **Lookup:** For each integer index, the Embedding layer retrieves a corresponding row from its internal weight matrix.
3. **Training:** The values in this matrix are updated by backpropagation, just like standard neural network weights.
- **Rule of Thumb:** Embedding dimensions typically range from 10 to 300, depending on the task and data size.

## 📐 Mathematical Foundations
- **Equivalence:** An Embedding layer is mathematically equivalent to a One-hot encoding followed by a Dense layer (with no bias/activation). However, it is much more computationally efficient because it uses direct indexing instead of matrix multiplication by zeros.

## 💻 Implementation
- Creating a lookup and embedding pipeline:
```python
embedding_layer = tf.keras.layers.Embedding(input_dim=1000, # vocab size
                                            output_dim=50) # embedding dim

# Usage in a model
model = tf.keras.Sequential([
    tf.keras.layers.Input(shape=[], dtype=tf.string),
    str_lookup_layer, # Maps string to int
    embedding_layer,  # Maps int to 50D vector
    tf.keras.layers.Dense(1)
])
```

## 🧪 Experiments
1. **The Vector Math Test:** In a word embedding space, compute `King - Man + Woman`. Observe if the result is closer to the `Queen` vector than to any other word. This demonstrates that the model has learned the concept of "gender."

## ⚠️ Constraints & Pitfalls
- **Overfitting:** For small datasets, large embeddings can easily overfit the training data.
- **Random Initialization:** An Embedding layer MUST be part of a model to be useful, as it starts with random noise and only becomes meaningful through training (unless using pretrained weights).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Keras_Preprocessing_Layers_Categorical]]
- Used in → [[RNN_Mechanics]]
- Related to → [[Dimensionality_Reduction_Basics]]
---
(MINIMUM 3 links)
