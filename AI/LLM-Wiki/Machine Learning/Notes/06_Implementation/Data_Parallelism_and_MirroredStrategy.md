---
id: 06-dpar-a1b2
tags: [agentic-ai, 06_Implementation, tensorflow]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Data Parallelism and MirroredStrategy

> [!ABSTRACT]
> Data parallelism is the most widely used technique for distributed training. It replicates the model on multiple devices (workers), with each replica processing a different mini-batch. TensorFlow's `MirroredStrategy` implements synchronous data parallelism on a single machine, ensuring all replicas remain perfectly identical by using the **AllReduce** algorithm to aggregate gradients.

## 🧠 Intuition First
- Imagine you have 4 identical twins who all want to learn the same poem. 
- **The Process:** You give each twin a different page of the book. They all study their page at the same time. At the end of the hour, they all meet and shout out everything they learned. They listen to each other and update their common "memory" so that every twin now knows what was on all 4 pages. They are always in perfect sync.

## 🎯 Why This Matters
- Problem it solves: Speeds up training linearly (ideally) with the number of GPUs while maintaining the simplicity of the standard training loop.
- Real-world usage: Standard approach for scaling deep learning on multi-GPU servers.

## 🧩 Glossary
- [[MirroredStrategy]] : A distribution strategy that mirrors all variables across multiple GPUs on a single machine.
- [[Replica]] : An identical copy of the model running on a specific device.
- [[AllReduce]] : A decentralized algorithm where nodes collaborate to compute a global reduction (like a mean) and share the result with everyone simultaneously.
- [[Sync Training]] : Training where every device must finish its current step before any device can start the next one.

## ⚙️ Mechanics (First Principles)
### The Mirrored Loop:
1. **Model Replication:** Before training, the model is copied to all GPUs.
2. **Batch Splitting:** Each GPU receives a different portion of the current mini-batch.
3. **Local Gradients:** Each GPU computes gradients for its own data.
4. **AllReduce Sync:** The AllReduce algorithm efficiently calculates the mean of all gradients from all GPUs.
5. **Global Update:** Every replica applies the *same* mean gradient to its local weights, keeping them identical.

## 📐 Mathematical Foundations
- **Effective Batch Size:** If you have 8 GPUs and set batch size to 32, the effective batch size is $8 \times 32 = 256$. You must increase your learning rate accordingly (often linearly).

## 💻 Implementation
- Using `MirroredStrategy` in Keras:
```python
import tensorflow as tf

strategy = tf.distribute.MirroredStrategy()

# Everything inside this scope is distributed
with strategy.scope():
    model = tf.keras.Sequential([...])
    model.compile(loss="mse", optimizer="nadam")

# Dataset must be batched by the total desired global batch size
model.fit(train_dataset, epochs=10)
```

## 🧪 Experiments
1. **The Batch Scale Test:** Train a model on 1 GPU with batch size 32. Then train on 2 GPUs using `MirroredStrategy` and batch size 64. Observe that the number of iterations per epoch is halved, but the final accuracy remains similar.

## ⚠️ Constraints & Pitfalls
- [[Synchronous Bottleneck]] : In synchronous training, the whole system only moves as fast as the **slowest** GPU. If one card is older or overheating, it will slow down all others.
- **VRAM limit:** Every card must have enough RAM to hold the entire model (since the model is mirrored, not split).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Multi_GPU_Training_Strategies]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Model_Parallelism_Mechanics]]
---
(MINIMUM 3 links)
