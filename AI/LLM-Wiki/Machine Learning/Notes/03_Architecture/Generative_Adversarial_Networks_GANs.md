---
id: 03-gans-a1b2
tags: [agentic-ai, 03_Architecture, generative-models]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Generative Adversarial Networks GANs

> [!ABSTRACT]
> Generative Adversarial Networks (GANs) are composed of two competing neural networks: a **Generator** that tries to produce realistic synthetic data and a **Discriminator** that tries to distinguish between real and fake data. This zero-sum game drives both networks to improve until the generator produces data so realistic that the discriminator is forced to guess.

## 🧠 Intuition First
- Imagine a criminal (the Generator) trying to make counterfeit $100 bills. 
- Imagine a detective (the Discriminator) trying to catch the fakes. 
- At first, the criminal is bad and the detective catches them easily. To avoid prison, the criminal gets better at copying the ink. The detective then learns to look for the watermarks. The criminal then learns to fake watermarks. This "arms race" continues until the counterfeit bills are indistinguishable from real ones.

## 🎯 Why This Matters
- Problem it solves: Generates high-fidelity synthetic data (images, audio, text) that captures the sharp details and complex distributions of the training set.
- Real-world usage: Creating photorealistic faces, image-to-image translation (e.g., day to night), and data augmentation.

## 🧩 Glossary
- [[Generator]] : A network that takes random noise as input and outputs a synthetic instance.
- [[Discriminator]] : A binary classifier that evaluates an instance and outputs the probability that it is real.
- [[Adversarial Training]] : Training two networks in opposition to each other.
- [[Nash Equilibrium]] : A state in game theory where no player can improve their outcome by changing only their own strategy. In GANs, this is where $P(real) = 0.5$.

## ⚙️ Mechanics (First Principles)
### The 2-Phase Training Loop:
1. **Phase 1: Train Discriminator**
    - Sample real data and generate fake data from noise.
    - Label real as 1, fake as 0.
    - Update discriminator weights to maximize classification accuracy.
2. **Phase 2: Train Generator**
    - Generate fake data from noise.
    - Feed it to the (frozen) discriminator.
    - Label the fake data as 1 (real).
    - Update generator weights to minimize the discriminator's accuracy.

## 📐 Mathematical Foundations
- **Zero-Sum Objective:** The generator and discriminator optimize the same value function in opposite directions (min-max).

## 💻 Implementation
- High-level GAN structure in Keras:
```python
generator = tf.keras.Sequential([...]) # noise -> image
discriminator = tf.keras.Sequential([...]) # image -> [0, 1]

# Combined model for generator training
gan = tf.keras.Sequential([generator, discriminator])
discriminator.trainable = False # Freeze during phase 2
gan.compile(loss="binary_crossentropy", optimizer="rmsprop")
```

## 🧪 Experiments
1. **The Discriminator Lead:** Stop training the generator for 10 epochs while continuing to train the discriminator. Observe how the discriminator becomes "too smart," providing no useful gradients to the generator when it resumes training.

## ⚠️ Constraints & Pitfalls
- [[Training Instability]] : The competition can become unstable, with one network overwhelming the other or both oscillating forever.
- **Metric Difficulty:** Accuracy is not a good metric for GANs; a 100% accurate discriminator means the generator has failed.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Basics]]
- Used in → [[Deep_Convolutional_GANs_DCGANs]]
- Related to → [[Challenges_in_Training_GANs]]
---
(MINIMUM 3 links)
