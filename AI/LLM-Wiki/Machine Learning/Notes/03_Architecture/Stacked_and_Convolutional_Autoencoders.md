---
id: 03-stca-a1b2
tags: [agentic-ai, 03_Architecture, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Stacked and Convolutional Autoencoders

> [!ABSTRACT]
> Stacked (deep) autoencoders have multiple hidden layers, allowing them to learn more complex hierarchical features. Convolutional autoencoders are specialized for visual data, using convolutional and pooling layers in the encoder and transposed convolutional layers in the decoder to maintain and reconstruct spatial structures.

## 🧠 Intuition First
- Imagine you're describing an complex machine. 
- **Shallow AE:** You just give a 1-sentence summary. 
- **Stacked AE:** You describe the machine in terms of its systems (engine, transmission), and then describe those systems in terms of their parts (gears, pistons). The layers build a hierarchy of understanding.
- **Convolutional AE:** You describe the machine in terms of what you see through a sliding lens—edges, shapes, and silhouettes—preserving the spatial relationships between the parts.

## 🎯 Why This Matters
- Problem it solves: Captures highly non-linear patterns in complex data (like high-res images) where simple linear models or shallow networks fail.
- Real-world usage: Unsupervised pretraining for deep networks, data visualization (when followed by t-SNE), and high-quality image reconstruction.

## 🧩 Glossary
- [[Stacked AE]] : A deep autoencoder with multiple hidden layers.
- [[Convolutional AE]] : An autoencoder that uses `Conv2D` layers for the encoder and `Conv2DTranspose` for the decoder.
- [[Hierarchical Features]] : Features learned at different levels of abstraction (e.g., edges $\to$ shapes $\to$ objects).
- [[Symmetry]] : The architectural convention where the decoder's layer structure mirrors the encoder's.

## ⚙️ Mechanics (First Principles)
### Stacked AE:
- Typically has a symmetrical "sandwich" structure around a central bottleneck.
- Diminishing layer sizes in the encoder, increasing in the decoder.

### Convolutional AE:
- **Encoder:** Input $\to$ [Conv -> Pool] stacks $\to$ Global Average Pool (or small bottleneck).
- **Decoder:** Bottleneck $\to$ Dense $\to$ Reshape $\to$ [ConvTranspose] stacks $\to$ Output.
- Reduces spatial resolution while increasing depth, then reverses the process.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Building a Stacked AE in Keras:
```python
encoder = tf.keras.Sequential([
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(100, activation="relu"),
    tf.keras.layers.Dense(30, activation="relu") # 30D codings
])
decoder = tf.keras.Sequential([
    tf.keras.layers.Dense(100, activation="relu"),
    tf.keras.layers.Dense(28 * 28),
    tf.keras.layers.Reshape([28, 28])
])
stacked_ae = tf.keras.Sequential([encoder, decoder])
```

## 🧪 Experiments
1. **The Visualization Chain:** Train a stacked AE on Fashion MNIST to 30D codings. Use t-SNE to reduce the codings further to 2D. Observe how well the classes cluster compared to raw 2D PCA.

## ⚠️ Constraints & Pitfalls
- **Overpowering:** If the network is too deep/wide, it will memorize the training set perfectly without learning any useful abstractions (overfitting).
- **Training Time:** Stacked convolutional models can be very slow to train compared to shallow dense ones.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Autoencoders_Mechanics]]
- Used in → [[Tied_Weights_in_Autoencoders]]
- Related to → [[Transposed_Convolutions]]
---
(MINIMUM 3 links)
