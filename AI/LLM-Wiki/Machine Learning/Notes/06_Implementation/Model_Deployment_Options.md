---
id: 06-depl-o5p6
tags: [agentic-ai, 06_Implementation, deployment]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# Model Deployment Options

> [!ABSTRACT]
> Model Deployment is the process of integrating a trained machine learning model into a production environment where it can serve real users. The choice of deployment depends on latency requirements, privacy concerns, and available infrastructure, with three primary patterns: Server-Side, Client-Side, and Federated.

## 🧠 Intuition First
- Imagine you have a translator. 
    - **Server-Side:** You send a letter to an office, they translate it and mail it back. (Reliable, but slow).
    - **Client-Side:** You carry a pocket dictionary. (Fast and private, but limited memory).
    - **Federated:** Everyone in town updates their own dictionary and once a week you all share the new words you learned without showing each other your personal notes.

## 🎯 Why This Matters
- Problem it solves: Balancing infrastructure costs with user experience.
- Real-world usage: Google Keyboard using Federated Learning to predict the next word without uploading your private texts.

## 🧩 Glossary
- [[Batch Prediction]] : Running the model on a large group of inputs at once (usually offline).
- [[Streaming Prediction]] : Predicting results one-by-one as requests arrive (Real-time).
- [[Tensorflow Lite]] : A library designed for deploying models on mobile and IoT devices.

## ⚙️ Mechanics (First Principles)
1. **Server-Side Deployment:**
    - Model lives on a central server.
    - Advantages: Easy to update, supports large/complex models, secure.
    - Disadvantages: Higher latency, requires internet, server costs.
2. **Client-Side Deployment (Edge):**
    - Model lives on the user's device (phone, browser).
    - Advantages: Low latency (no network trip), high privacy, works offline.
    - Disadvantages: Limited by device hardware, model binary is exposed to theft.
3. **Federated Learning:**
    - Models are trained locally on devices; only weights/gradients are shared with a central server to improve a global model.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Python (Conceptual) - Flask API for Server-Side:
```python
from flask import Flask, request, jsonify
app = Flask(__name__)

@app.route('/predict', methods=['POST'])
def predict():
    data = request.json['input']
    prediction = model.predict(data)
    return jsonify({'prediction': prediction.tolist()})
```

## 🧪 Experiments
1. **Latency Benchmarking:** Measure the "Round-trip time" (RTT) of a server prediction vs. a local prediction on a mobile device.
2. **Model Quantization:** Use a tool like `tflite` to reduce a model's size (e.g., from 100MB to 10MB) and observe the impact on accuracy vs. inference speed.

## ⚠️ Constraints & Pitfalls
- **The Cold Start:** Servers may take time to "spin up" if they haven't received a request in a while.
- **Binary Bloat:** Large models can make a mobile app's download size too big for users to accept.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Baseline_Heuristics]]
- Used in → [[Model_Monitoring_And_Drift]]
- Related to → [[ML_Success_Metrics]]
