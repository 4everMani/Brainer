---
id: 03-mpar-a1b2
tags: [agentic-ai, 03_Architecture, tensorflow]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Model Parallelism Mechanics

> [!ABSTRACT]
> Model parallelism involves partitioning a single neural network across multiple devices (GPUs or machines). Unlike data parallelism, each device only holds a portion of the model's parameters and is responsible for a subset of the total computation. While conceptually powerful, it is difficult to implement efficiently due to the high communication overhead between layers.

## 🧠 Intuition First
- Imagine you're building a car on an assembly line. 
- **Model Parallelism:** One person only knows how to build the engine (GPU 1), and another only knows how to build the chassis (GPU 2). The chassis builder can't do anything until the engine builder finishes and hands it over. If they have to talk back and forth a lot, they spend more time talking than building. This only works if the tasks are large enough that the "handover" time is small compared to the "build" time.

## 🎯 Why This Matters
- Problem it solves: Enables the training of "Giant Models" (e.g., massive LLMs) that are too large to fit in the VRAM of even the most powerful single GPU.
- Real-world usage: Training Foundation models with hundreds of billions of parameters.

## 🧩 Glossary
- [[Model Parallelism]] : Splitting the model's layers or operations across multiple processors.
- [[Vertical Slicing]] : Splitting a layer into parts (e.g., 50 neurons on GPU 1, 50 on GPU 2).
- [[Communication Overhead]] : The time spent transferring data between devices, which is much slower than in-memory computation.
- [[Pipeline Parallelism]] : A technique to reduce idle time by having different GPUs work on different batches at different stages of the model simultaneously.

## ⚙️ Mechanics (First Principles)
### The Challenges:
1. **Dependency:** Layer $L+1$ must wait for the output of Layer $L$. This creates "idle" time for GPUs.
2. **Cross-talk:** If a layer is sliced vertically, both halves need the output of both halves from the previous layer, leading to massive data transfer.

### When it works:
- **Partially Connected Architectures:** CNNs with independent branches can be easily split across GPUs with minimal communication.
- **Deep RNNs:** Different layers of a deep LSTM can process consecutive time steps in a "pipeline" fashion.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Manual Model Parallelism in Keras:
```python
# Place part 1 on GPU 0
with tf.device("/gpu:0"):
    layer1 = tf.keras.layers.Conv2D(...)(inputs)
    layer2 = tf.keras.layers.Conv2D(...)(layer1)

# Place part 2 on GPU 1
with tf.device("/gpu:1"):
    layer3 = tf.keras.layers.Conv2D(...)(layer2)
    outputs = tf.keras.layers.Dense(...)(layer3)
```

## 🧪 Experiments
1. **The Latency Test:** Measure the time per iteration for a model split across two distant machines vs. two GPUs on the same machine. Observe that the network latency makes model parallelism nearly impossible over standard ethernet.

## ⚠️ Constraints & Pitfalls
- [[Efficiency Trap]] : In many cases, a simple "Plain" stack running on a single GPU will be faster than a "Model Parallel" version due to the elimination of communication delays.
- **Load Balancing:** If one part of the model is much slower than the others, all other GPUs will sit idle waiting for it.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Multi_GPU_Training_Strategies]]
- Used in → [[Evolution_of_Large_Language_Models]]
- Related to → [[Data_Parallelism_and_MirroredStrategy]]
---
(MINIMUM 3 links)
