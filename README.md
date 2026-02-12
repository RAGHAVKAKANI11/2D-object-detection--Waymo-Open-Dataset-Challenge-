
# 🚗 2D Object Detection on Waymo Open Dataset challenge

**PyTorch · TensorFlow · YOLOv8 · Faster R-CNN · TensorRT**

---

## 📌 Overview

This project implements and benchmarks **state-of-the-art 2D object detection models** on the **Waymo Open Dataset** — one of the largest and most challenging autonomous driving perception datasets.

**Goal:** Develop robust, real-time capable detectors for vehicles, pedestrians, and cyclists in diverse driving conditions.

---

## 🎯 Key Results

| Model | mAP (Val) | Inference Speed | Notes |
|-------|-----------|-----------------|-------|
| **YOLOv8x** | **76.4%** | 22 FPS | Best accuracy-speed trade-off |
| Faster R-CNN (ResNet-50) | 72.1% | 8 FPS | Higher latency, stronger on small objects |
| YOLOv8l | 74.8% | 28 FPS | Lightweight alternative |

✅ **TensorRT optimized version:** 2.3x speedup, 52 FPS @ FP16

---

## 🧠 Model Architecture

### YOLOv8 (Anchor-free)
- CSPDarknet backbone
- PANet neck for feature fusion
- Decoupled head for classification + regression

### Faster R-CNN (Anchor-based)
- ResNet-50 + FPN
- RPN for region proposals
- RoIAlign + two-stage refinement

---

## 📊 Failure Case Analysis

**Challenging scenarios identified:**
- Occluded pedestrians (mAP ↓ 23%)
- Night/low-light conditions (mAP ↓ 18%)
- Distant small vehicles (mAP ↓ 15%)

**Mitigations attempted:**
- Mosaic augmentation
- Multi-scale training
- Class-aware sampling

---

## 🛠️ Reproducibility

All training configurations, model checkpoints, and evaluation scripts are version-controlled.

**To reproduce 76.4% mAP:**

```bash
git clone https://github.com/RAGHAVKAKANI11/waymo-object-detection
cd waymo-object-detection
pip install -r requirements.txt
python train.py --config configs/yolov8x_waymo.yaml
