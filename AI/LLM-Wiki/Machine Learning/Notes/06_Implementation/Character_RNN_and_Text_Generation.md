---
id: 06-crnn-a1b2
tags: [agentic-ai, 06_Implementation, nlp]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Character RNN and Text Generation

> [!ABSTRACT]
> A Character RNN (char-RNN) is a language model trained to predict the next character in a sequence. Once trained, it can generate novel text by iteratively predicting and sampling the next character. Controlling the "temperature" during sampling allows for a trade-off between rigid, high-probability text and diverse, creative output.

## 🧠 Intuition First
- Imagine you're playing a game of "complete the word." If you see "Appl", you'll almost certainly guess "e." A char-RNN does this for every single letter in a whole book. Over millions of examples, it doesn't just learn spelling; it learns grammar , style, and even punctuation. To generate text, it's like a mimic: you give it a starting phrase, and it continues in the style of its teacher (e.g., writing like Shakespeare).

## 🎯 Why This Matters
- Problem it solves: Enables the generation of original content and serves as a simple "hello world" for complex language modeling.
- Real-world usage: Code completion, automated creative writing, and data augmentation for low-resource languages.

## 🧩 Glossary
- [[Char-RNN]] : A recurrent neural network that processes text at the character level.
- [[Language Model]] : A model that learns the probability distribution of sequences of tokens.
- [[Greedy Decoding]] : Always picking the most probable next character (tends to be repetitive).
- [[Temperature Sampling]] : Rescaling the output probabilities before sampling to control diversity.

## ⚙️ Mechanics (First Principles)
### The Generation Cycle:
1. **Input:** A string of text (e.g., "To be or not to b").
2. **Predict:** The model outputs a probability distribution over all possible characters.
3. **Rescale (Temperature):** Divide the raw scores (logits) by a temperature $T$.
    - $T \to 0$: Favors highest probability (rigid).
    - $T = 1$: Standard distribution.
    - $T \to \infty$: Equal probability for all characters (random noise).
4. **Sample:** Randomly pick the next character based on the rescaled probabilities.
5. **Append:** Add the character to the text and repeat.

## 📐 Mathematical Foundations
- **Softmax with Temperature:**
  $P_i = \frac{\exp(s_i / T)}{\sum_j \exp(s_j / T)}$

## 💻 Implementation
- Sampling with temperature in TensorFlow:
```python
def next_char(text, temperature=1):
    y_proba = model.predict([text])[0, -1:]
    rescaled_logits = tf.math.log(y_proba) / temperature
    char_id = tf.random.categorical(rescaled_logits, num_samples=1)[0, 0]
    return vocab[char_id]
```

## 🧪 Experiments
1. **The Heatwave Test:** Generate text from a Shakespeare-trained model using $T=0.1, T=1.0,$ and $T=10.0$. Observe how the text goes from perfect spelling but repetition to creative prose, and finally to gibberish.

## ⚠️ Constraints & Pitfalls
- **Short-term Context:** Without stateful RNNs or LSTMs, the model will quickly forget the beginning of a paragraph, leading to incoherent long-form text.
- **Computation:** Generating text character-by-character is very slow because the model must be run for every single letter.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Recurrent_Neural_Networks_RNNs]]
- Used in → [[Stateful_vs_Stateless_RNNs]]
- Related to → [[NLP_Basics_and_Sentiment_Analysis]]
---
(MINIMUM 3 links)
