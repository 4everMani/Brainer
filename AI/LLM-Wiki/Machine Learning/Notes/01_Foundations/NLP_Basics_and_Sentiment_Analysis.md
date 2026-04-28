---
id: 01-nlpb-a1b2
tags: [agentic-ai, 01_Foundations, nlp]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# NLP Basics and Sentiment Analysis

> [!ABSTRACT]
> Natural Language Processing (NLP) is the task of making machines understand and generate human language. Sentiment analysis, the "Hello World" of NLP, typically uses the IMDb movie reviews dataset to classify text as positive or negative by learning dense representations of words or subwords.

## 🧠 Intuition First
- Imagine you're a judge who only speaks code. People send you handwritten movie reviews. You first standardize them (make all letters lowercase). Then you chop the reviews into individual words (tokenization). You look up each word in a specialized dictionary that assigns a "goodness" score to it. Finally , you sum up the scores to decide if the reviewer liked the movie or not.

## 🎯 Why This Matters
- Problem it solves: Automates the categorization of qualitative human feedback into quantitative data.
- Real-world usage: Customer support ticket sorting, social media brand monitoring, and content moderation.

## 🧩 Glossary
- [[Sentiment Analysis]] : Classifying text based on the underlying emotional tone.
- [[Token]] : A single unit of text (word, subword, or character) processed by the model.
- [[Vocabulary]] : The set of all unique tokens known to the model.
- [[Subword Tokenization]] : Breaking rare words into smaller frequent pieces (e.g., "smartest" $\to$ "smart" + "est").
- [[BPE]] : Byte Pair Encoding. A popular subword tokenization technique.

## ⚙️ Mechanics (First Principles)
### The NLP Pipeline:
1. **Standardization:** Lowercase, remove punctuation.
2. **Tokenization:** Split into words (whitespace) or subwords (BPE/WordPiece).
3. **Encoding:** Map tokens to integer IDs using a fixed vocabulary.
4. **Embedding:** Map IDs to dense vectors that capture semantic meaning.
5. **Pooling/RNN:** Aggregate word vectors into a single sentence-level representation.
6. **Output:** Sigmoid (binary sentiment) or Softmax (multi-class).

### Subword Advantages:
- Handles rare words (e.g., misspelled words or suffixes) by decomposing them into known components.
- Significantly reduces the vocabulary size while maintaining the ability to process any text.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Standard word-level model for IMDb:
```python
model = tf.keras.Sequential([
    tf.keras.layers.TextVectorization(max_tokens=1000),
    tf.keras.layers.Embedding(input_dim=1000, output_dim=128, mask_zero=True),
    tf.keras.layers.GRU(128),
    tf.keras.layers.Dense(1, activation="sigmoid")
])
```

## 🧪 Experiments
1. **The Vocabulary Test:** Train a model on IMDb using a vocabulary of 100 words vs. 10,000 words. Observe how the small vocabulary limits the model's ability to pick up on specific informative terms.

## ⚠️ Constraints & Pitfalls
- [[Language Bias]] : Whitespace tokenization fails for languages like Chinese, Japanese, or German. Use specialized tokenizers (e.g., `sentencepiece` or `tokenizers` library).
- **Padding Impact:** Without masking, long sequences of padding tokens at the end of a sentence can wash out the learned signal in an RNN.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Basics]]
- Used in → [[RNN_Masking_for_Variable_Sequences]]
- Related to → [[Trainable_Embeddings_Keras]]
---
(MINIMUM 3 links)
