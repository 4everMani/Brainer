---
id: 03-vaex-a1b2
tags: [agentic-ai, 03_Architecture, generative-models]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Variational Autoencoders VAEs

> [!ABSTRACT]
> Variational Autoencoders (VAEs) are probabilistic generative models that perform variational Bayesian inference. Unlike standard autoencoders that map inputs to a single point in latent space, VAEs map inputs to a Gaussian distribution (mean and variance). This forces the latent space to be continuous and structured, allowing for the generation of new, realistic data by sampling from the learned distribution.

## 🧠 Intuition First
- Imagine you're an artist drawing faces. 
- **Standard AE:** You learn to draw 10 specific people perfectly. If you try to draw someone "halfway" between person A and person B, the result is a messy blur because you only know those exact points.
- **VAE:** You learn that a face is a collection of traits (e.g., "smile-ness," "hair-length") that follow a bell curve. Instead of memorizing one face, you learn the "range" of what a human face looks like. You can then pick any random spot in that range and draw a brand-new, realistic person who doesn't exist.

## 🎯 Why This Matters
- Problem it solves: Creates a structured, interpolatable latent space for generating synthetic data and enables fast, approximate Bayesian inference.
- Real-world usage: Image generation (faces, art), drug discovery (generating molecular structures), and anomaly detection.

## 🧩 Glossary
- [[Latent Space]] : The structured multi-dimensional space where codings are located.
- [[Reparameterization Trick]] : A technique that allows gradients to flow through a random sampling step by expressing the sample as a function of deterministic inputs and a noise term.
- [[Latent Loss]] : A penalty (KL Divergence) that pushes the latent distribution to match a standard normal distribution.
- [[Evidence Lower Bound]] : The mathematical objective (ELBO) that VAEs maximize during training.

## ⚙️ Mechanics (First Principles)
### The 3-Step Architecture:
1. **Encoder:** Produces two vectors for each input: a mean $\mu$ and a log-variance $\gamma$ (for numerical stability).
2. **Sampling:** A coding $\mathbf{z}$ is sampled using $\mathbf{z} = \mu + \exp(\gamma/2) \cdot \epsilon$, where $\epsilon$ is random Gaussian noise.
3. **Decoder:** Reconstructs the original input from the sampled coding $\mathbf{z}$.

### The Dual Loss:
- **Reconstruction Loss:** Pushes the model to be accurate.
- **Latent Loss (KL):** Pushes the latent distribution to be a simple, smooth Gaussian.

## 📐 Mathematical Foundations
- **Latent Loss Equation:**
  $\mathcal{L} = -\frac{1}{2} \sum [1 + \gamma - \exp(\gamma) - \mu^2]$

## 💻 Implementation
- Creating a Sampling layer in Keras:
```python
class Sampling(tf.keras.layers.Layer):
    def call(self, inputs):
        mean, log_var = inputs
        return tf.random.normal(tf.shape(log_var)) * tf.exp(log_var / 2) + mean
```

## 🧪 Experiments
1. **The Interpolation Test:** Pick two images (e.g., a "Shirt" and a "Dress"). Get their codings $\mathbf{z}_1$ and $\mathbf{z}_2$. Generate images for 10 points on a line between them. Observe the smooth visual transition.

## ⚠️ Constraints & Pitfalls
- [[Blurry Reconstructions]] : VAEs tend to produce slightly blurry images compared to GANs because the MSE loss favors "average" pixel values over sharp details.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Autoencoders_Mechanics]]
- Used in → [[Diffusion_Models_and_DDPMs]]
- Related to → [[Generative_Adversarial_Networks_GANs]]
---
(MINIMUM 3 links)
