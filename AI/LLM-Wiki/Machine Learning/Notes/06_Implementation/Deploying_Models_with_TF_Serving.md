---
id: 06-tfsr-a1b2
tags: [agentic-ai, 06_Implementation, model-deployment]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Deploying Models with TF Serving

> [!ABSTRACT]
> TensorFlow Serving (TF Serving) is a high-performance system for serving machine learning models in production environments. It is designed for industrial use, providing features like zero-downtime model versioning, automatic batching, and high-throughput communication via gRPC and REST APIs.

## 🧠 Intuition First
- Imagine you've built a world-class translation engine. If you just run it on your laptop, only you can use it. **TF Serving** is like a massive, automated multilingual post office. You put your model into a "delivery box" (SavedModel) and hand it to the post office (Docker container). The post office then provides a 24/7 window where anyone in the world can send a letter (input) and get a translation (prediction) instantly, without you needing to do anything.

## 🎯 Why This Matters
- Problem it solves: Handles the operational complexities of productionizing ML, including scaling to high request volumes, managing multiple model versions, and ensuring low-latency predictions.
- Real-world usage: Powering the inference engines behind Google, Airbnb, and other large-scale web services.

## 🧩 Glossary
- [[TF Serving]] : A dedicated model server that executes TensorFlow SavedModels.
- [[SavedModel]] : A directory containing the full model (architecture, weights, and graph).
- [[Docker]] : A platform that allows you to package and run the model server in a consistent, isolated environment.
- [[Model Versioning]] : The ability of TF Serving to automatically load a new version of a model when it appears in the directory without stopping the service.

## ⚙️ Mechanics (First Principles)
### The 3-Step Deployment:
1. **Export:** Save your trained Keras model using `model.save(path)`. Ensure it includes all necessary preprocessing layers.
2. **Setup Server:** Use Docker to pull the `tensorflow/serving` image.
3. **Run:** Start the container, mapping your local model directory to the container's internal model directory and exposing the API ports (8500 for gRPC, 8501 for REST).

### Key Features:
- **Versioning:** TF Serving monitors its directories and automatically switches to the latest version found.
- **Rollback:** To revert, just delete the new version's folder.
- **Batching:** Can combine multiple individual requests into one large batch for GPU acceleration (enabled via flags).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Starting TF Serving with Docker:
```bash
docker run -p 8500:8500 -p 8501:8501 \
  --mount type=bind,source=/path/to/my_model,target=/models/my_model \
  -e MODEL_NAME=my_model -t tensorflow/serving
```

## 🧪 Experiments
1. **The Version Switch:** Start a server with Version 1 of a model. While the server is running, drop a Version 2 folder into the directory. Watch the server logs to see it detect and load the new version automatically.

## ⚠️ Constraints & Pitfalls
- [[Preprocessing Bundling]] : If you don't include preprocessing layers in the SavedModel, the client must perform the exact same cleaning/scaling, which often leads to errors in production.
- **Python-Only Ops:** TF Serving cannot execute custom Python code (like `tf.py_function`). The model must consist entirely of standard TensorFlow operations.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Keras_Model_Persistence]]
- Used in → [[Model_Serving_via_gRPC_and_REST]]
- Related to → [[MLOps_Fundamentals]]
---
(MINIMUM 3 links)
