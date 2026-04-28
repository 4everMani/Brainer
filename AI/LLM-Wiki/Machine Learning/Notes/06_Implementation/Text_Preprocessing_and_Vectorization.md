---
id: 06-tpre-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Text Preprocessing and Vectorization

> [!ABSTRACT]
> Preparing raw text for neural networks requires standardization, tokenization, and vectorization. Keras provides the `TextVectorization` layer to automate these steps, converting sentences into sequences of word IDs or frequency-based representations like TF-IDF to focus on informative terms.

## 🧠 Intuition First
- Imagine you're translating a book into code. 
- **Standardization:** You make everything lowercase and remove exclamation marks so "Run!" and "run" are the same word. 
- **Tokenization:** You chop the sentences into individual words.
- **Vectorization:** You replace each word with its ID from a dictionary. 
- **TF-IDF:** Instead of just counting words, you give "The" a very low score (it's everywhere) and "Supernova" a very high score (it's rare and informative).

## 🎯 Why This Matters
- Problem it solves: Handles the inherent messiness of human language by providing a structured, numerical pipeline that can be embedded directly into a model.
- Real-world usage: Sentiment analysis, document classification, and as a first step for complex NLP models like Transformers.

## 🧩 Glossary
- [[Tokenization]] : Splitting a string into smaller units, typically words or subwords.
- [[Standardization]] : Removing punctuation and converting text to lowercase to ensure consistency.
- [[TF-IDF]] : Term Frequency times Inverse Document Frequency. A method to weight words by how unique they are to a document.
- [[Padding]] : Adding zeros to the end of shorter sequences so all sequences in a batch have the same length.

## ⚙️ Mechanics (First Principles)
### The 3-Step Text Pipeline:
1. **Standardize & Split:** Clean text (lowercase/punctuation) and split by whitespace.
2. **Build Vocabulary:** Learn the most frequent words from the training set.
3. **Map & Pad:** Replace words with their integer IDs. Truncate long sequences or pad short ones with 0s to reach a fixed length.

### Representation Modes:
- **`int`**: Output a sequence of integers (one per word). Best for RNNs and Transformers.
- **`multi_hot`**: Output a binary vector (1 if word is present).
- **`tf_idf`**: Output a vector where each word's count is weighted by its informative value across the whole dataset.

## 📐 Mathematical Foundations
- **TF-IDF Weighting:**
  $score = count \cdot \log(1 + \frac{total\_docs}{docs\_with\_word + 1})$

## 💻 Implementation
- Basic text vectorization for classification:
```python
text_vec = tf.keras.layers.TextVectorization(output_mode="tf_idf")
text_vec.adapt(train_sentences)

# Transform new sentences
encoded = text_vec(["Deep learning is amazing!", "Is it?"])
```

## 🧪 Experiments
1. **The Informativeness Test:** Vectorize a set of sentences using `output_mode="count"` vs `output_mode="tf_idf"`. Compare the values for common words like "the" and rare words like "learning."

## ⚠️ Constraints & Pitfalls
- **Language Limitations:** Whitespace splitting doesn't work for languages like Chinese or Japanese. Use `tf-text` for advanced tokenization.
- **Loss of Order:** `multi_hot` and `tf_idf` modes discard the order of words, which is critical for complex meaning.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Keras_Preprocessing_Layers_Categorical]]
- Used in → [[Trainable_Embeddings_Keras]]
- Related to → [[Dimensionality_Reduction_Basics]]
---
(MINIMUM 3 links)
