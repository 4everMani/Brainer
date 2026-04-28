---
id: 02-penc-a1b2
tags: [agentic-ai, 02_Mathematics, transformers]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Positional Encoding

> [!ABSTRACT]
> Since transformers process all tokens in a sequence simultaneously, they have no inherent sense of order. Positional encoding solves this by adding a unique vector to each token's embedding that describes its absolute and relative position in the sequence. These encodings are typically generated using sine and cosine functions of different frequencies.

## 🧠 Intuition First
- Imagine you have a stack of photos from a vacation. If you just look at them as a pile, you don't know the story. **Positional Encoding** is like writing a timestamp and a "location tag" on the back of every photo. When you look at the pile, the tags tell you that the photo of the "Sunrise" happened *before* the photo of the "Lunch," allowing you to reconstruct the timeline even if the photos are physically scrambled.

## 🎯 Why This Matters
- Problem it solves: Restores the temporal/sequential information lost by removing recurrence (RNNs) and convolution (CNNs).
- Real-world usage: Essential for language understanding, where "The dog bit the man" and "The man bit the dog" have the exact same tokens but different meanings.

## 🧩 Glossary
- [[Positional Encoding]] : A vector added to word embeddings to inject order information.
- [[Absolute Position]] : The specific index of a token (e.g., word #5).
- [[Relative Position]] : The distance between two tokens (e.g., word #2 is 3 steps before word #5).
- [[Sinusoidal Encoding]] : Using sine and cosine waves to create unique, deterministic positional vectors.

## ⚙️ Mechanics (First Principles)
### Why Sines and Cosines?
- They provide a unique pattern for every position.
- The values are bounded between -1 and +1.
- They allow the model to easily learn **relative positions**, because for any fixed offset $k$, $PE_{pos+k}$ can be represented as a linear function of $PE_{pos}$.

### The Combination:
- The positional encoding vector has the same dimensionality as the word embedding.
- It is **added** to the embedding ($X_{final} = X_{embedding} + PE$).

## 📐 Mathematical Foundations
- **The Equations:**
  $PE_{(pos, 2i)} = \sin(pos / 10000^{2i/d_{model}})$
  $PE_{(pos, 2i+1)} = \cos(pos / 10000^{2i/d_{model}})$
- $pos$ is the position, $i$ is the dimension index.

## 💻 Implementation
- Creating a Positional Encoding layer in Keras:
```python
class PositionalEncoding(tf.keras.layers.Layer):
    def __init__(self, max_length, embed_size, **kwargs):
        super().__init__(**kwargs)
        # 1. Create meshgrid of pos and i
        # 2. Compute sin/cos values
        # 3. Store as constant tensor
        self.pos_encodings = tf.constant(pos_emb)

    def call(self, inputs):
        # inputs are embeddings [batch, seq_len, embed_size]
        return inputs + self.pos_encodings[:, :tf.shape(inputs)[1]]
```

## 🧪 Experiments
1. **The Unique Pattern Test:** Visualize a positional encoding matrix as a heatmap. Observe the wavy patterns and verify that every row (position) has a unique "barcode" of values.

## ⚠️ Constraints & Pitfalls
- **Maximum Length:** Fixed sinusoidal encodings must be generated for a specific maximum sequence length (e.g., 512). If your sequence is longer, you must regenerate the matrix.
- **Signal Overlap:** If the positional values are too large compared to the embeddings, they might "drown out" the semantic information.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Trainable_Embeddings_Keras]]
- Used in → [[Transformer_Architecture_Fundamentals]]
- Related to → [[Multi_Head_Attention_Mechanics]]
---
(MINIMUM 3 links)
