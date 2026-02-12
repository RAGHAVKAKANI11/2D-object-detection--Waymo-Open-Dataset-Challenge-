# 🚗 2D Object Detection on Waymo Open Dataset Challenge

**PyTorch · TensorFlow · YOLOv8 · Faster R-CNN · TensorRT**

---

## 📌 Overview

This project implements and benchmarks **state-of-the-art 2D object detection models** on the **Waymo Open Dataset** — one of the largest and most challenging autonomous driving perception datasets.

**Goal:** Develop robust, real-time–capable object detectors for vehicles, pedestrians, and cyclists under diverse and challenging driving conditions.

---

## 🎯 Key Results

| Model | mAP (Val) | Inference Speed | Notes |
|------|-----------|-----------------|------|
| **YOLOv8x** | **76.4%** | 22 FPS | Best accuracy–speed trade-off |
| Faster R-CNN (ResNet-50) | 72.1% | 8 FPS | Higher latency, stronger on small objects |
| YOLOv8l | 74.8% | 28 FPS | Lightweight alternative |

**Evaluation Protocol**
- Official Waymo validation split  
- Standard **mAP@0.5:0.95** metric  

✅ **TensorRT-optimized YOLOv8 inference:**  
- **2.3× speedup**
- **52 FPS @ FP16**

---

## 📂 Dataset Details

- **Dataset:** Waymo Open Dataset (2D Detection)
- **Classes:** Vehicle, Pedestrian, Cyclist
- **Scale:** Large-scale autonomous driving dataset with **millions of annotated 2D bounding boxes**
- **Scenarios:** Urban traffic, occlusions, varying illumination, long-range objects

---

## 🧠 Model Architectures

### YOLOv8 (Anchor-free)
- CSPDarknet backbone
- PANet neck for multi-scale feature fusion
- Decoupled head for classification and bounding-box regression

### Faster R-CNN (Anchor-based)
- ResNet-50 backbone with Feature Pyramid Network (FPN)
- Region Proposal Network (RPN)
- RoIAlign and two-stage refinement for final predictions

---

## 📊 Failure Case Analysis

**Challenging scenarios identified:**
- Occluded pedestrians → **mAP ↓ 23%**
- Night / low-light conditions → **mAP ↓ 18%**
- Distant small vehicles → **mAP ↓ 15%**

**Mitigation strategies explored:**
- Mosaic and multi-scale data augmentation
- Class-aware sampling
- Resolution-aware training

---

## ⚙️ Training Setup

- **Input Resolution:** 1280 × 768  
- **Optimizer:** AdamW  
- **Batch Size:** 16  
- **Epochs:** 50  
- **Hardware:** NVIDIA GPU (CUDA-enabled)

---

## 🚀 Optimization & Deployment

- Exported trained YOLOv8 models to **TensorRT** for optimized inference
- FP16 precision used to reduce latency and increase throughput
- TensorRT optimization applied to **YOLOv8 inference pipeline** for deployment benchmarking

---

## 🛠️ Reproducibility

All training configurations, model checkpoints, and evaluation scripts are version-controlled.

### To reproduce **76.4% mAP**:

```bash
git clone https://github.com/RAGHAVKAKANI11/waymo-object-detection
cd waymo-object-detection
pip install -r requirements.txt
python train.py --config configs/yolov8x_waymo.yaml

## 🚧 Limitations & Future Work

- Extend to 3D object detection using LiDAR-camera fusion
- Improve low-light performance via temporal modeling
- Deploy optimized inference pipeline for real-time edge devices

