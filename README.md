# Post-Disaster Flood Mapping using Sentinel-2 Imagery 🌊

A deep learning framework that detects and visualizes flood-affected regions from satellite imagery — combining **Attention U-Net** for water body segmentation with **SNUNet-CD** for change detection between pre-flood and post-flood images.

---

## 📄 Research Publication

Based on our published research:

**"A Deep Learning Framework for Post-Disaster Flood Mapping using Sentinel-2 Images"**

Presented at **AITA 2025, Bangalore**.

---

## 🧠 Overview

Rapid, automated flood mapping is critical for disaster response, damage estimation, and resource allocation.

This project builds an end-to-end pipeline that:

- Generates synthetic post-flood imagery from pre-flood Sentinel-2 images using **HSV color masking** and **morphological dilation**, addressing the scarcity of real post-disaster imagery.
- Segments water bodies in both pre-flood and post-flood images using an **Attention U-Net** model.
- Detects changes between the two segmentations using **SNUNet-CD**.
- Classifies every pixel as:
  - Existing Water Body
  - Newly Flooded Region
  - Non-Water Area
- Produces a clear, color-coded flood map:
  - ⚪ White = Existing Water
  - 🔴 Red = Newly Flooded Region
  - ⚫ Black = Non-Water

---

## 🏗️ Architecture

### 1. Water Body Segmentation — Attention U-Net

- Utilizes attention gates to focus on relevant spatial regions.
- Reduces background noise from urban and vegetated environments.
- Improves segmentation accuracy compared to standard U-Net.

### 2. Change Detection — SNUNet-CD

- Extracts feature representations from pre-flood and post-flood images.
- Computes a pixel-wise difference map.
- Identifies newly flooded regions with high spatial precision.

### 3. Post-Processing

- Overlays detected flood regions on the original pre-flood image.
- Generates an interpretable and visually intuitive flood map.

---

## 🔄 Pipeline Workflow

```text
Pre-Flood Image
       │
       ▼
Attention U-Net
       │
       ▼
Water Mask (Pre)
       │
       ├───────────────────────┐
       │                       │
       ▼                       ▼
Post-Flood Image      Attention U-Net
                               │
                               ▼
                      Water Mask (Post)
                               │
                               ▼
                    SNUNet-CD Change Detection
                               │
                               ▼
                     Color-Coded Flood Map
```

---

## 📊 Results

### Segmentation Performance

| Model | Accuracy (%) | IoU (%) |
|---------|---------|---------|
| U-Net | 82.92 | 60.22 |
| FCN32s | 88.30 | 68.42 |
| Attention U-Net | 94.50 | 65.65 |

### Final Test Performance

| Metric | Score |
|----------|----------|
| Accuracy | 94.22% |
| F1-Score | 85.03% |
| Precision | 86.44% |
| Recall | 84.24% |
| Dice Similarity Coefficient (DSC) | 76.71% |
| Loss | 0.1616 |

### Key Finding

The **Attention U-Net** model outperformed standard **U-Net** and **FCN32s** baselines, demonstrating that attention mechanisms significantly improve water body segmentation performance in satellite imagery.

---

## 📁 Dataset

### Source

**Satellite Images of Water Bodies (Kaggle)**

### Dataset Characteristics

- High-resolution Sentinel-2 satellite imagery.
- Binary water body masks.
- Masks generated using **NDWI (Normalized Difference Water Index)**.
- Tuned thresholding for accurate water/non-water separation.
- Covers diverse geographical environments:
  - Urban Regions
  - Rural Areas
  - Forested Landscapes

---

## ⚙️ Tech Stack

### Programming & Frameworks

- Python
- TensorFlow
- Keras

### Deep Learning Models

- Attention U-Net
- SNUNet-CD

### Image Processing

- OpenCV
  - HSV Color Masking
  - Morphological Operations

### Scientific Computing & Visualization

- NumPy
- Matplotlib

---

## 🎯 Applications

- Disaster Response Planning
- Flood Damage Assessment
- Emergency Resource Allocation
- Environmental Monitoring
- Climate Resilience Studies