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

## ⚙️ Getting Started

### 1. Clone & Setup
\`\`\`bash
git clone https://github.com/chintamanenih/Fog-Vision-Enhancement-Pipeline.git
cd Fog-Vision-Enhancement-Pipeline
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
\`\`\`

### 2. Run the Integrated Pipeline
\`\`\`bash
python Integ_model.py
\`\`\`
"@ | Out-File -Encoding utf8 README.md

# 3. Create the GitHub Actions CI workflow directory and file
New-Item -ItemType Directory -Force -Path ".github\workflows"
@"
name: Computer Vision CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Set up Python 3.10
      uses: actions/setup-python@v5
      with:
        python-version: '3.10'
        cache: 'pip'

    - name: Install Dependencies
-     run: |
        python -m pip install --upgrade pip
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

    - name: Run Syntax & Compile Check
      run: |
        python -m compileall .
