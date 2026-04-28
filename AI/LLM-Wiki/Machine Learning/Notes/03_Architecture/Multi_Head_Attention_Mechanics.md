---
id: 03-mhat-a1b2
tags: [agentic-ai, 03_Architecture, transformers]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Multi Head Attention Mechanics

> [!ABSTRACT]
> Multi-Head Attention allows a transformer to jointly attend to information from different representation subspaces at different positions. It works by running multiple "heads" of scaled dot-product attention in parallel, each with its own learned linear projections for queries, keys, and values.

## 🧠 Intuition First
- Imagine you're looking at a piece of fruit. 
- **Single-Head Attention:** You look at the whole fruit and try to decide what it is. 
- **Multi-Head Attention:** You have 8 different specialists looking at the fruit. Specialist 1 only looks at **Color**; Specialist 2 only looks at **Texture**; Specialist 3 only looks at **Shape**. They all report their findings simultaneously. By combining their reports, you get a much deeper understanding of the fruit than if you only had one person looking at everything at once.

## 🎯 Why This Matters
- Problem it solves: Prevents a single attention head from averaging out many different types of relationships (e.g., a word being a verb AND being in the past tense AND being plural).
- Real-world usage: Capturing complex semantic and grammatical rules in large language models.

## 🧩 Glossary
- [[Scaled Dot-Product Attention]] : The base mechanism that computes similarity between Query and Key to weight the Value.
- [[Head]] : A single, independent attention operation.
- [[Query (Q)]] : What you are looking for (e.g., the current word).
- [[Key (K)]] : What you are comparing against (e.g., all other words in the sentence).
- [[Value (V)]] : The actual information you want to extract if there's a match.

## ⚙️ Mechanics (First Principles)
### The Parallel Process:
1. **Projection:** Linearly project $Q, K, V$ into $h$ different subspaces (heads) using learned weight matrices.
2. **Scaled Attention:** For each head, compute:
   $\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$
    - *Scaling:* Dividing by $\sqrt{d_k}$ prevents the dot product from growing too large and saturating the softmax.
3. **Concatenation:** Join all $h$ results along the channel dimension.
4. **Final Linear:** Apply one last weight matrix to project back to the original model dimension.

## 📐 Mathematical Foundations
- **Broadcasting Magic:** In TensorFlow/Keras, multi-head attention is implemented using 4D tensors (Batch, Heads, Time, Dims), allowing all heads and all sentences in a batch to be processed with a single matrix multiplication.

## 💻 Implementation
- Using the MultiHeadAttention layer in Keras:
```python
import tensorflow as tf

mha_layer = tf.keras.layers.MultiHeadAttention(
    num_heads=8, key_dim=512 // 8) # Total dim split across heads

# Self-attention: Q, K, V are all the same
output = mha_layer(query=Z, value=Z, key=Z)
```

## 🧪 Experiments
1. **The Head Diversity Test:** Visualize the attention weights for different heads in a translation model. Observe that Head 1 might focus on the subject-verb relationship, while Head 2 focuses on local adjectives.

## ⚠️ Constraints & Pitfalls
- [[Manual Masking]] : In some versions of Keras, `MultiHeadAttention` does not support automatic mask propagation. You must manually create and pass an `attention_mask`.
- **Causal Masking:** In the decoder, you must use a lower-triangular mask to ensure words don't "look into the future."

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Attention_Mechanisms_Bahdanau_and_Luong]]
- Used in → [[Transformer_Architecture_Fundamentals]]
- Related to → [[Positional_Encoding]]
---
(MINIMUM 3 links)
