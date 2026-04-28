---
id: 06-tgrp-a1b2
tags: [agentic-ai, 06_Implementation, model-deployment]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Model Serving via gRPC and REST

> [!ABSTRACT]
> Once a model is deployed with TF Serving, it can be queried via two primary protocols: REST (HTTP/JSON) and gRPC (HTTP/2/Protobuf). REST is simpler and more compatible with web browsers, while gRPC is significantly faster and more bandwidth-efficient, making it the preferred choice for low-latency, high-volume production systems.

## 🧠 Intuition First
- **REST:** Imagine sending a letter via standard mail. You have to write everything out in plain text (JSON). It's easy for anyone to read, but it's bulky and takes a while to arrive and be processed.
- **gRPC:** Imagine sending the same information via a high-speed fiber-optic cable using a secret, compact digital code (Protobuf). It's much faster, uses less energy (bandwidth), and was designed specifically for machines to talk to each other as fast as possible.

## 🎯 Why This Matters
- Problem it solves: Balances the trade-off between ease of integration (REST) and operational performance (gRPC).
- Real-world usage: Using REST for simple proof-of-concepts or web frontends, and gRPC for internal microservices and high-throughput mobile apps.

## 🧩 Glossary
- [[gRPC]] : A high-performance remote procedure call framework developed by Google.
- [[Protocol Buffers]] : A compact, binary serialization format used by gRPC.
- [[JSON]] : A text-based data format used by REST APIs.
- [[Payload Overhead]] : The extra data used by text formats (like JSON) to represent simple numbers, which can be 10x larger than the binary equivalent.

## ⚙️ Mechanics (First Principles)
### REST API (Port 8501):
- **Request:** HTTP POST with a JSON body containing `signature_name` and `instances`.
- **Response:** JSON dictionary with a `predictions` key.
- **Pro:** Works with standard libraries like `requests` and requires no extra dependencies.

### gRPC API (Port 8500):
- **Request:** Serialized `PredictRequest` protobuf.
- **Response:** Serialized `PredictResponse` protobuf.
- **Pro:** Compact binary format, faster serialization, and lower latency over HTTP/2.
- **Con:** Requires installing the `tensorflow-serving-api` library.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Querying via gRPC (Compact version):
```python
import grpc
from tensorflow_serving.apis import predict_pb2, prediction_service_pb2_grpc

channel = grpc.insecure_channel("localhost:8500")
stub = prediction_service_pb2_grpc.PredictionServiceStub(channel)

request = predict_pb2.PredictRequest()
request.model_spec.name = "my_model"
# Convert data to tensor protobuf
request.inputs["input"].CopyFrom(tf.make_tensor_proto(X_new))

response = stub.Predict(request, timeout=10.0)
```

## 🧪 Experiments
1. **The Size Test:** Send a batch of 100 high-res images to TF Serving via REST and then via gRPC. Measure the total data transferred in bytes. Observe that gRPC is significantly more efficient.

## ⚠️ Constraints & Pitfalls
- **Numeric Precision:** Converting large NumPy arrays to JSON strings (for REST) can lose precision or bloat the payload size enormously (e.g., a float like `0.123456789` takes many bytes in text).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Deploying_Models_with_TF_Serving]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[TFRecord_Binary_Format]]
---
(MINIMUM 3 links)
