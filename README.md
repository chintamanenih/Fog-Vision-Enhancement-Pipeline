# Adverse Weather Dehazing & Object Detection Pipeline

> An end-to-end computer vision architecture designed for autonomous driving and vehicle sensor systems in harsh, low-visibility weather conditions (fog, haze, and low light).

---

## 🏗️ Architecture & Pipeline Overview

[ Harsh Weather Sensor Feed / Image ]
│
▼
[ Fog Detection & Density Estimation Model ] ──(Estimates Severity & Flags Visibility)
│
▼
[ Custom ResNet-Powered U-Net Deep Prior Dehazing Network ] ──(Adaptive Image Enhancement)
│
▼
[ Enhanced Clean Image ] ──> [ YOLO Object Detection Model ] ──> [ Final Bounding Boxes & Perception ]


1. **Fog & Visibility Estimation**: Initial models (`fog_detection.py`, regression models) evaluate the scene to classify fog severity and estimate atmospheric degradation.
2. **Adaptive Deep Prior Dehazing**: Uses a custom U-Net integrated with a ResNet-34 backbone (`Unet with ResNet34.ipynb`) to apply context-aware dehazing proportional to the estimated fog density.
3. **Downstream YOLO Perception**: The cleaned, high-visibility image is passed into YOLO for robust object detection, ensuring safety critical vehicle vision doesn't fail in harsh weather.

---

## 🚀 Tech Stack & Components

* **Deep Learning Frameworks**: PyTorch, Torchvision, Ultralytics YOLO
* **Backbones & Networks**: ResNet-34, Custom U-Net Deep Prior Architectures
* **Data Processing & Metrics**: OpenCV, NumPy, Scikit-learn, Custom Evaluation Metrics (`Metrics.py`)
* **DevOps**: Git, GitHub Actions CI

---

## 📂 Repository Structure

* `Integ_model.py`: End-to-end integration script linking fog estimation, dehazing, and YOLO detection.
* `Fog_detection.py`: Atmospheric visibility and fog classification module.
* `Unet with ResNet34.ipynb`: Training and architecture notebooks for the deep prior dehazing network.
* `Metrics.py`: Quantitative image enhancement and detection evaluation functions.
* `*.pkl` / `*.pth`: Pre-trained weights for fog regression and ResNet-Unet dehazing.

---


