---
id: 01-vect-y5z6
tags: [agentic-ai, 01_Foundations, preprocessing]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# Data Vectorization

> [!ABSTRACT]
> Data vectorization is the process of converting raw data (text, images, or categorical variables) into a numerical format that machine learning algorithms can process. It is a critical step in the ML pipeline that transforms human-readable information into mathematical tensors.

## 🧠 Intuition First
- Imagine you are trying to explain a movie to a calculator. You can't just type "it's a scary movie about a shark." You have to turn it into numbers: maybe a 1 for "scary," a 0 for "funny," and a number representing the duration. This "translation" from concepts to numbers is vectorization.

## 🎯 Why This Matters
- Problem it solves: Models cannot "read" text or "see" images directly; they perform operations on matrices and vectors.
- Real-world usage: Converting a user's search query into a vector to find similar products in an e-commerce database.

## 🧩 Glossary
- [[Tensor]] : A multi-dimensional array of numbers (the generalized form of vectors and matrices).
- [[One-Hot Encoding]] : A method for representing categorical data as binary vectors.
- [[TF-IDF]] : Term Frequency-Inverse Document Frequency, a technique to weight word importance in text.

## ⚙️ Mechanics (First Principles)
- **Tabular Data:** Continuous features are normalized (e.g., scaling to 0-1). Categorical features are converted using one-hot encoding or embeddings.
- **Text Data:**
    1. **Tokenization:** Splitting text into individual words or sub-words.
    2. **Counting:** Counting occurrences (Bag-of-Words).
    3. **Weighting:** Applying TF-IDF to emphasize rare, meaningful words.
    4. **Embeddings:** Using pre-trained models (like Word2Vec or BERT) to map words to dense vectors that capture semantic meaning.
- **Image Data:** Images are represented as 3D tensors (Height x Width x Color Channels). Pre-trained neural networks can extract "feature vectors" from the penultimate layer of the model.

## 📐 Mathematical Foundations
- **One-Hot Encoding:** For a category $c$ in a set of $N$ categories, the vector $v$ is all zeros except at index $i$ corresponding to $c$, where $v_i = 1$.
- **TF-IDF Calculation:**
  $w_{i,j} = tf_{i,j} \times \log(\frac{N}{df_i})$
  where $tf_{i,j}$ is frequency of term $i$ in document $j$, and $df_i$ is the number of documents containing term $i$.

## 💻 Implementation
- Text Vectorization using Scikit-Learn:
```python
from sklearn.feature_extraction.text import TfidfVectorizer

corpus = ["Machine learning is great", "Learning from data is key"]
vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(corpus)

print(vectorizer.get_feature_names_out())
print(X.toarray())
```

## 🧪 Experiments
1. **Distance Comparison:** Vectorize three sentences (two similar, one different) and calculate the Euclidean distance between their vectors.
2. **Feature Scaling:** Compare the performance of a simple model (like KNN) on a dataset with and without feature normalization.

## ⚠️ Constraints & Pitfalls
- **High Dimensionality:** Vectorizing large vocabularies can lead to extremely sparse matrices, increasing memory usage and computation time.
- **Out-of-Vocabulary (OOV):** Simple vectorizers may fail when encountering words not seen during training.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[ML_Framing]]
- Used in → [[Artificial_Neural_Networks]]
- Related to → [[Data_Exploration_Clustering]]
