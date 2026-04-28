---
id: 03-auto-a1b2
tags: [agentic-ai, 03_Architecture, unsupervised-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Autoencoders Mechanics

> [!ABSTRACT]
> Autoencoders are artificial neural networks that learn dense, low-dimensional representations of input data without supervision. They consist of an **Encoder** that compresses input into a latent representation (codings) and a **Decoder** that reconstructs the input from these codings. By constraining the network, it is forced to discover and exploit patterns in the data to minimize reconstruction loss.

## 🧠 Intuition First
- Imagine you're a messenger who has to send long reports over a very expensive telegram line. You can't send the whole report (Bottleneck). 
- **The Encoder:** You summarize the 10-page report into a single 3-word code (Codings). 
- **The Decoder:** Your partner on the other end knows your coding system and uses those 3 words to rewrite the 10-page report. 
- To succeed, you must find the 3 most important words that capture the essence of the report. The "loss" is how many facts your partner got wrong in the reconstruction.

## 🎯 Why This Matters
- Problem it solves: Performs non-linear dimensionality reduction, acts as a feature detector for unsupervised pretraining, and serves as a foundation for generative models.
- Real-world usage: Data compression, visualization of high-dimensional data, and identifying anomalies.

## 🧩 Glossary
- [[Encoder (AE)]] : The part of the network that maps the input to the latent representation.
- [[Decoder (AE)]] : The part of the network that maps the latent representation back to the original format.
- [[Codings]] : The low-dimensional hidden state (latent representation) produced by the encoder.
- [[Reconstruction Loss]] : The cost function (typically MSE or Binary Cross-Entropy) measuring the difference between the input and the reconstructed output.
- [[Undercomplete AE]] : An autoencoder where the coding layer has fewer neurons than the input layer, preventing it from trivially copying data.

## ⚙️ Mechanics (First Principles)
### The Learning Goal:
- The network is trained to learn the **identity function** $f(\mathbf{x}) \approx \mathbf{x}$ under constraints.
- If the activations are linear and the loss is MSE, an undercomplete autoencoder performs **Principal Component Analysis (PCA)**.

### Self-Supervised Learning:
- Autoencoders are self-supervised because they automatically generate their own labels (the labels are identical to the inputs).

## 📐 Mathematical Foundations
- **PCA Equivalence:** A linear AE with one hidden layer of $d$ neurons and MSE loss finds the same $d$-dimensional subspace as PCA.

## 💻 Implementation
- Simple Linear Autoencoder for PCA in Keras:
```python
import tensorflow as tf

encoder = tf.keras.Sequential([tf.keras.layers.Dense(2)])
decoder = tf.keras.Sequential([tf.keras.layers.Dense(3)])
autoencoder = tf.keras.Sequential([encoder, decoder])

autoencoder.compile(loss="mse", optimizer="sgd")
# X_train is used for BOTH input and target
autoencoder.fit(X_train, X_train, epochs=500)
```

## 🧪 Experiments
1. **The Identity Test:** Train an AE on random noise with a large bottleneck. Observe that it can reconstruct the noise perfectly. Then, train it on structured data (MNIST) with a small bottleneck. Observe that it discards fine noise but keeps the digit's shape.

## ⚠️ Constraints & Pitfalls
- [[Power Trap]] : If the encoder/decoder are too powerful, they can learn to map each instance to a single arbitrary number without learning any meaningful features (overfitting).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[PCA_Mechanics]]
- Used in → [[Stacked_and_Convolutional_Autoencoders]]
- Related to → [[Self_supervised_Learning]]
---
(MINIMUM 3 links)
