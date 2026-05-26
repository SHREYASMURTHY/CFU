# 🔬 CFU: Automated Bacterial Colony Counter & Classifier

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform: Edge & Cloud](https://img.shields.io/badge/Platform-Edge%20%26%20Cloud-success.svg)](#)
[![Hardware: Raspberry Pi](https://img.shields.io/badge/Hardware-Raspberry%20Pi-red.svg)](#)

An advanced, end-to-end deep learning system designed for automated bacterial colony detection, counting, and classification (Colony Forming Units - CFU). This platform features highly optimized models tailored for both high-performance cloud environments and resource-constrained edge devices (specifically Raspberry Pi 4/5).

---

## 🌟 Key Features

- **🎯 High-Precision Detection**: Custom-trained YOLOv8 models optimized for accurate object detection and localization of micro-colonies.
- **🏷️ Automated Classification**: Deep CNN classifiers to categorize bacterial colonies based on morphological features using the AGAR dataset.
- **⚡ Edge Optimization**: Integrated model compression pipeline featuring **channel pruning** and **INT8 quantization** via ONNX Runtime for ultra-fast, low-latency execution on Raspberry Pi.
- **📱 Hybrid Ecosystem**:
  - **React Dashboard**: Modern web interface for centralized colony analytics and dataset management.
  - **Expo Mobile App**: Cross-platform React Native app enabling researchers to capture petri dish photos and count CFUs directly in the field.

---

## 📂 Project Architecture

```text
├── core/                   # Image preprocessing, Petri dish isolation, and core utilities
├── cnn/                    # Custom CNN classifier training and evaluation
├── yolo/                   # YOLOv8 target detection and counting pipelines
├── web/                    # React web-based analytics dashboard (Frontend & Backend)
├── mobile/                 # Expo (React Native) mobile application
├── cfu-counter-backend/    # Mobile app API backend
├── scripts/                # Edge-optimization tools (Pruning, INT8 Quantization, ONNX Export)
└── requirements.txt        # Backend and ML dependencies
```

---

## 🚀 Quick Start Guide

### 1. Prerequisites & Installation

Clone the repository and install the core Python requirements:

```bash
pip install -r requirements.txt
```

### 2. Image Preprocessing

Isolate Petri dishes and normalize lighting conditions to maximize model robustness:

```python
from core.preprocessing import PreprocessingPipeline

# Instantiate the pipeline
pipeline = PreprocessingPipeline(output_dir='processed_output')

# Process a folder of raw petri dish images
pipeline.process_directory('path/to/raw_images', num_workers=4)
```

### 3. Model Training

#### Train the CNN Classifier
```bash
python cnn/cnn_train.py --data path/to/processed_data --epochs 50
```

#### Train the YOLOv8 Detector
```bash
python yolo/yolo_train.py --data yolo/data.yaml --epochs 100 --imgsz 640
```

### 4. Edge Compilation & Optimization

To deploy the models on a Raspberry Pi, run them through the optimization suite:

#### Prune redundant weights:
```bash
python scripts/prune_model.py --model path/to/model.pt --amount 0.3
```

#### Quantize to INT8 ONNX format:
```bash
python scripts/quantize_onnx.py --input model.onnx --output model_int8.onnx
```

#### Benchmark performance on target hardware:
```bash
python scripts/benchmark_pi_safe.py --model model_int8.onnx --image test.jpg
```

---

## 📊 Dataset & Citation

This project utilizes the **AGAR (Annotated Germs for Automated Recognition)** dataset developed by NeuroSYS, containing over **18,000 photos** of microbial colonies and **336,000 annotations**.

If you use this system or the AGAR dataset in your research, please cite:

```bibtex
@misc{majchrowska2021agar,
  title={AGAR a microbial colony dataset for deep learning detection},
  author={Sylwia Majchrowska and Jaros{\l}aw Paw{\l}owski and Grzegorz Gu{\l}a and Tomasz Bonus and Agata Hanas and Adam Loch and Agnieszka Pawlak and Justyna Roszkowiak and Tomasz Golan and Zuzanna Drulis-Kawa},
  year={2021},
  eprint={2108.01234},
  archivePrefix={arXiv},
  primaryClass={cs.CV}
}
```

---

## 📄 License

This repository is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.

---
*Developed & Maintained by [SHREYASMURTHY](https://github.com/SHREYASMURTHY).*
