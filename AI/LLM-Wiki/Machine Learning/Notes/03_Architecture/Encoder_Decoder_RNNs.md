---
id: 03-edrn-a1b2
tags: [agentic-ai, 03_Architecture, sequential-data]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Encoder Decoder RNNs

> [!ABSTRACT]
> An Encoder-Decoder (or Sequence-to-Sequence) architecture is designed for tasks where both inputs and outputs are sequences, possibly of different lengths. It consists of an **Encoder** RNN that processes the input sequence into a fixed-size context vector, and a **Decoder** RNN that uses this vector to generate the output sequence.

## 🧠 Intuition First
- Imagine you're translating a sentence from English to French. 
- **The Problem:** You can't start translating the first word of the English sentence until you've heard the *whole* sentence, because the last word might change the gender or tense of the first French word.
- **The Solution:** The **Encoder** is a listener who hears the whole English sentence and writes a one-page summary (Context Vector). The **Decoder** is a speaker who takes that summary and writes the French version.

## 🎯 Why This Matters
- Problem it solves: Decouples the length of the input and output sequences, allowing for flexible mapping between domains of different structures.
- Real-world usage: Neural Machine Translation (NMT), text summarization, and speech-to-text.

## 🧩 Glossary
- [[Encoder]] : An RNN that takes a sequence and outputs its final hidden state as a representation of the whole sequence.
- [[Decoder]] : An RNN that takes the encoder's final state and generates a sequence one step at a time.
- [[Context Vector]] : The fixed-size vector (the hidden state) that carries the distilled meaning of the input sequence from the encoder to the decoder.
- [[Teacher Forcing]] : A training technique where the ground truth from the previous time step is fed to the decoder as input, instead of the decoder's own (potentially wrong) prediction.

## ⚙️ Mechanics (First Principles)
### The 2-Step Process:
1. **Encoding:** The encoder processes input $\mathbf{x}_1, \dots, \mathbf{x}_n$. The final hidden state $\mathbf{h}_n$ becomes the initial state of the decoder.
2. **Decoding:**
    - The decoder receives a "Start of Sequence" (<SOS>) token.
    - At each step $t$, it predicts the next token based on its current state and the previous token.
    - Training uses **Teacher Forcing** to speed up convergence.
    - Inference uses the decoder's own previous prediction.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- High-level architecture in Keras (Functional API):
```python
# Encoder
encoder_inputs = tf.keras.layers.Input(shape=[None], dtype=tf.int32)
encoder_embeddings = tf.keras.layers.Embedding(vocab_size, 128)(encoder_inputs)
_, state_h, state_c = tf.keras.layers.LSTM(256, return_state=True)(encoder_embeddings)
encoder_state = [state_h, state_c]

# Decoder
decoder_inputs = tf.keras.layers.Input(shape=[None], dtype=tf.int32)
decoder_embeddings = tf.keras.layers.Embedding(vocab_size, 128)(decoder_inputs)
decoder_lstm = tf.keras.layers.LSTM(256, return_sequences=True)(
    decoder_embeddings, initial_state=encoder_state)
output = tf.keras.layers.Dense(vocab_size, activation="softmax")(decoder_lstm)
```

## 🧪 Experiments
1. **The Bottleneck Test:** Try to translate a 50-word sentence using an encoder with only 10 hidden units. Observe how the model fails because the context vector is too small to hold the meaning (the "Dory" problem).

## ⚠️ Constraints & Pitfalls
- **Fixed-length Bottleneck:** The context vector is a fixed size. For very long sentences, the encoder "forgets" the beginning before it reaches the end. This is solved by **Attention**.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Recurrent_Neural_Networks_RNNs]]
- Used in → [[Attention_Mechanisms_Bahdanau_and_Luong]]
- Related to → [[Transformer_Architecture_Fundamentals]]
---
(MINIMUM 3 links)
