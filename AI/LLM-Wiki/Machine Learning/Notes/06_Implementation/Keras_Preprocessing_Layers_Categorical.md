---
id: 06-kcpr-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Keras Preprocessing Layers Categorical

> [!ABSTRACT]
> Categorical features must be mapped to numerical representations before being fed to a neural network. Keras provides `CategoryEncoding` for integer features and `StringLookup` for text features, supporting one-hot and multi-hot encoding. For large vocabularies without an adaptation phase, the `Hashing` layer implements the "hashing trick."

## 🧠 Intuition First
- Imagine you're sorting mail into different city bins. 
- **StringLookup:** You have a master list of cities (vocabulary). You see "Paris," look it up on the list, and find it's bin #1. If you see a new city not on the list, you put it in the "Unknown" bin.
- **Hashing:** You don't have a list. Instead, you have a math formula that turns the letters of the city name into a number between 1 and 10. Every time you see "Paris," the formula gives the same number. It's faster because you don't need to check a list, but occasionally two different cities might get the same number (collision).

## 🎯 Why This Matters
- Problem it solves: Automates the conversion of strings and discrete integers into the binary formats (one-hot/multi-hot) that neural networks can process.
- Real-world usage: Encoding user IDs, product categories, or country names in recommender systems and classifiers.

## 🧩 Glossary
- [[Multi-hot Encoding]] : A vector where each active category is represented by a 1 (multiple 1s allowed).
- [[Hashing Trick]] : Mapping categorical values to a fixed number of bins using a hash function to avoid maintaining a vocabulary.
- [[OOV Buckets]] : Out-of-vocabulary buckets used to pseudorandomly distribute unknown categories to reduce collisions.
- [[IntegerLookup]] : A variant of StringLookup that works with integer IDs instead of strings.

## ⚙️ Mechanics (First Principles)
### The 3 Core Layers:
1. **CategoryEncoding:** Takes integer categories. Supports `one_hot`, `multi_hot`, and `count` (sum of occurrences).
2. **StringLookup:** Maps strings to integer indices. Requires `adapt()` to build a vocabulary. Can also output one-hot vectors directly.
3. **Hashing:** Stateless layer that maps any input (string or integer) to a fixed range. Useful for very large, shifting datasets.

### Handling Unseen Data:
- `StringLookup` uses index 0 for unknown items by default.
- `num_oov_indices` allows for multiple buckets to distinguish between different unknown categories.

## 📐 Mathematical Foundations
- **Hashing Collision:** Probability of collision depends on the ratio of unique categories to the number of bins ($N$).

## 💻 Implementation
- One-hot encoding cities with OOV buckets:
```python
str_lookup = tf.keras.layers.StringLookup(num_oov_indices=5, 
                                          output_mode="one_hot")
str_lookup.adapt(training_cities)

# Predict on new cities
encoded = str_lookup([["Paris"], ["New City"]])
```

## 🧪 Experiments
1. **The Collision Test:** Use a `Hashing` layer with `num_bins=5` on 100 unique city names. Observe how many cities end up sharing the same ID.

## ⚠️ Constraints & Pitfalls
- **Sparse Expansion:** One-hot encoding high-cardinality features (e.g., 100,000 unique IDs) can create massive, sparse tensors that consume too much memory. Use **Embeddings** instead.
- **Hashing Ambiguity:** Hashing collisions are permanent and will confuse the model if too frequent.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Categorical_Encoding]]
- Used in → [[Trainable_Embeddings_Keras]]
- Related to → [[Text_Preprocessing_and_Vectorization]]
---
(MINIMUM 3 links)
