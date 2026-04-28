---
id: 03-attn-a1b2
tags: [agentic-ai, 03_Architecture, sequential-data]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Attention Mechanisms Bahdanau and Luong

> [!ABSTRACT]
> Attention mechanisms allow the decoder to dynamically focus on relevant parts of the encoder's output at each time step, rather than relying on a single fixed-size context vector. This eliminates the information bottleneck for long sequences and provides an alignment score that measures the similarity between encoder and decoder states.

## 🧠 Intuition First
- Imagine the Encoder is a student who has read a whole textbook and the Decoder is a student answering an exam question.
- **Fixed Context:** The student tries to memorize the whole book and then takes the exam from memory (Bottleneck).
- **Attention:** The student is allowed to keep the book open during the exam. For every question, they "attend" to (look at) the specific page or paragraph that contains the answer. They focus their eyes on just the right spot at the right time.

## 🎯 Why This Matters
- Problem it solves: information loss in long sequences and provides "Explainability" by showing which input words contributed to each output word.
- Real-world usage: High-accuracy translation, image captioning (focusing on parts of the image), and document summarization.

## 🧩 Glossary
- [[Alignment Score]] : A scalar measuring how well the input at time $i$ matches the output at time $t$.
- [[Context Vector (Attention)]] : A weighted sum of all encoder hidden states, where weights are determined by alignment scores.
- [[Bahdanau Attention]] : (Concatenative) Learned similarity between previous decoder state and encoder hidden states.
- [[Luong Attention]] : (Dot-product) Similarity between current decoder state and encoder hidden states. Often faster.

## ⚙️ Mechanics (First Principles)
### The 3-Step Cycle:
1. **Score:** At each decoder step $t$, compare the decoder's current hidden state with all encoder hidden states $\mathbf{h}_i$ to get scores $e_{t,i}$.
2. **Normalize:** Pass the scores through a Softmax to get attention weights $\alpha_{t,i}$ (sum to 1).
3. **Blend:** Compute the context vector $\mathbf{c}_t = \sum \alpha_{t,i} \mathbf{h}_i$.
4. **Predict:** Concatenate $\mathbf{c}_t$ with the decoder's state to predict the next word.

## 📐 Mathematical Foundations
- **Luong Attention (Dot-Product):** $score(\mathbf{s}_t, \mathbf{h}_i) = \mathbf{s}_t^T \mathbf{W}_a \mathbf{h}_i$
- **Scaled Dot-Product:** Luong attention scaled by $1 / \sqrt{d}$ to prevent large values from saturating the softmax.

## 💻 Implementation
- Using the Keras Attention layer:
```python
import tensorflow as tf

attention_layer = tf.keras.layers.Attention()
# Inputs: [query, value, key]
# In Luong-style: query is decoder state, value/key are encoder states
context_vector = attention_layer([decoder_state, encoder_outputs])
```

## 🧪 Experiments
1. **The Alignment Visualization:** Plot the attention weights as a heatmap (rows=input words, columns=output words). In a translation task, observe the diagonal line of high weights, which reveals the word-for-word alignment.

## ⚠️ Constraints & Pitfalls
- **Computation:** Attention requires a dot product between every input and output step ($O(N \times M)$), which is expensive for very long documents.
- **Explainability Bias:** While attention maps are useful, they don't always perfectly represent the model's internal causal reasoning.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Encoder_Decoder_RNNs]]
- Used in → [[Transformer_Architecture_Fundamentals]]
- Related to → [[Multi_Head_Attention_Mechanics]]
---
(MINIMUM 3 links)
