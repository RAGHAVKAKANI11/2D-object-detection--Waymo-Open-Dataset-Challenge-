# 🚗 2D Object Detection on Waymo Open Dataset Challenge

# Waymo Open Dataset: 2D Object Detection Pipeline

## Overview
An end-to-end computer vision pipeline converting Waymo's autonomous driving dataset 
to YOLO format and training custom object detection models.

## Technical Implementation
- **Data Processing**: Parsed TFRecord files using TensorFlow, extracted 145+ camera frames 
  with OpenCV, converted bounding boxes to YOLO format
- **Model Training**: Fine-tuned YOLOv8n with custom data augmentation (mosaic, mixup, copy-paste)
- **Class Balancing**: Implemented priority-based frame selection to handle class imbalance 
  (VEHICLE: 1600+, PEDESTRIAN: 278+)
- **Hardware**: RTX 4060 GPU, achieving 20ms inference time per frame

## Results
- Successfully detected VEHICLE class with mAP50-95 of 0.052
- Identified and addressed class imbalance issues
- Built reusable pipeline for any Waymo dataset extraction

## Key Challenges Solved
1. TFRecord parsing and image decoding
2. Bounding box coordinate conversion and normalization
3. Handling class imbalance in autonomous driving datasets
4. Debugging YOLO training with empty label issues
```bash
git clone https://github.com/RAGHAVKAKANI11/waymo-object-detection
cd waymo-object-detection
pip install -r requirements.txt
python train.py --config configs/yolov8x_waymo.yaml

## 🚧 Limitations & Future Work

- Extend to 3D object detection using LiDAR-camera fusion
- Improve low-light performance via temporal modeling
- Deploy optimized inference pipeline for real-time edge devices

