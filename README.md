# Expo AI Runtime

Provides an expo module for react native with JavaScript API to run AI/ML model inference with best GPU/NPU/TPU support across platforms.
The goal is to outperform libraries like onnx-runtime (CPU focuses on android), pytorch-executorch (also CPU based mostly).
Approach for android is to use Google LiteRT with TensorFlow Lite models and for iOS using CoreML with Apple Neural Engine (NAA).
