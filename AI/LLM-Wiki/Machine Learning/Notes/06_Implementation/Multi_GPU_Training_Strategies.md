---
id: 06-mgpu-a1b2
tags: [agentic-ai, 06_Implementation, tensorflow]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Multi GPU Training Strategies

> [!ABSTRACT]
> Scaling training to multiple GPUs requires careful management of device placement, memory allocation, and communication between processors. TensorFlow provides high-level Distribution Strategies to automate this process, allowing for model and data parallelism that can reduce training time from days to minutes.

## 🧠 Intuition First
- Imagine you're building a massive Lego castle. 
- **Single GPU:** You're working alone. It's slow. 
- **Multi-GPU:** You have a team of 4 friends. You can either have each friend build a different wing of the castle (**Model Parallelism**) or you can give each friend the same set of instructions and a different pile of bricks to build identical sections that you then join together (**Data Parallelism**). To keep your friends from bumping into each other, you need a coordinator (Distribution Strategy) to tell them exactly which bricks to pick up and when to sync their work.

## 🎯 Why This Matters
- Problem it solves: Overcomes the hardware limits of a single machine and accelerates the R&D cycle by enabling much faster experimentation.
- Real-world usage: Training industry-standard models (like ResNet-101 or BERT) which are too large for a single consumer GPU.

## 🧩 Glossary
- [[CUDA]] : Nvidia's parallel computing platform used by TensorFlow to talk to the GPU.
- [[Logical Device]] : A virtual partition of a physical GPU, useful for simulating multi-GPU setups on a single card.
- [[Memory Growth]] : A setting that tells TensorFlow to only grab GPU RAM as needed, rather than all at once.
- [[Sync Training]] : All GPUs must finish their mini-batch and average their gradients before starting the next step.

## ⚙️ Mechanics (First Principles)
### GPU Management:
1. **Detection:** `tf.config.list_physical_devices('GPU')`.
2. **Memory Control:** Use `set_memory_growth` to allow other programs to share the GPU.
3. **Placement:** By default, TF puts everything on the first GPU. Use `with tf.device("/gpu:1"):` for manual placement.

### Distribution Options:
- **Data Parallelism:** Replicating the model and splitting the data. This is the most common and efficient approach.
- **Model Parallelism:** Splitting the model across GPUs. Only effective for specific architectures (like CNNs with small cross-connections).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Managing GPU RAM growth:
```python
gpus = tf.config.list_physical_devices('GPU')
for gpu in gpus:
    tf.config.experimental.set_memory_growth(gpu, True)
```

## 🧪 Experiments
1. **The Parallel Speedup:** Train a model on 1 GPU vs. 4 GPUs using data parallelism. Measure the time per epoch. Observe that while it is faster, there is a "communication overhead" that prevents it from being exactly 4x faster.

## ⚠️ Constraints & Pitfalls
- [[RAM Fragmentation]] : Starting and stopping many TensorFlow programs on the same GPU can lead to fragmented memory, eventually causing OOM errors even if total RAM is sufficient.
- **Inter-GPU Bandwidth:** If the connection between your GPUs is slow (e.g., PCIe Gen 3 vs NVLink), the time spent syncing gradients will cancel out the speedup from parallel processing.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[TensorFlow_Core_Basics]]
- Used in → [[Data_Parallelism_and_MirroredStrategy]]
- Related to → [[Cloud_Deployment_with_Vertex_AI]]
---
(MINIMUM 3 links)
