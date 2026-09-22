Post-Disaster Flood Mapping using Sentinel-2 Imagery 🌊

A deep learning framework that detects and visualizes flood-affected regions from satellite imagery — combining Attention U-Net for water body segmentation with SNUNet-CD for change detection between pre-flood and post-flood images.

📄 Based on our published research: "A Deep Learning Framework for Post-Disaster Flood Mapping using Sentinel-2 Images" — presented at AITA 2025, Bangalore.

🧠 Overview

Rapid, automated flood mapping is critical for disaster response, damage estimation, and resource allocation. This project builds an end-to-end pipeline that:

Generates synthetic post-flood imagery from pre-flood Sentinel-2 images (via HSV color masking + morphological dilation), since real post-disaster imagery is often unavailable in data-scarce regions.
Segments water bodies in both pre- and post-flood images using an Attention U-Net model.
Detects changes between the two segmentations using SNUNet-CD, classifying every pixel as an existing water body, a newly flooded region, or non-water.
Overlays the results onto the original image for a clear, color-coded flood map (white = existing water, red = newly flooded, black = non-water).
🏗️ Architecture
Segmentation: Attention U-Net — uses attention gates to focus on relevant spatial regions, improving accuracy over vanilla U-Net, especially in complex urban/vegetated backgrounds.
Change Detection: SNUNet-CD — computes feature maps for pre- and post-flood images and derives a pixel-wise difference map to localize newly flooded areas.
Post-processing: Final flood map is overlaid on the original pre-flood image for interpretability.
Pre-Flood Image ──► Attention U-Net ──► Water Mask (Pre)
                                              │
Post-Flood Image ─► Attention U-Net ──► Water Mask (Post)
                                              │
                        SNUNet-CD (Change Detection)
                                              │
                              Color-Coded Flood Map
📊 Results
Model	Accuracy (%)	IoU (%)
UNet	82.92	60.22
FCN32s	88.30	68.42
UNet Attention	94.50	65.65

Final test performance:

Metric	Score
Accuracy	94.22%
F1-score	85.03%
Precision	86.44%
Recall	84.24%
Dice Similarity Coefficient (DSC)	76.71%
Loss	0.1616

The Attention U-Net model outperformed standard UNet and FCN32s baselines, confirming that attention mechanisms meaningfully improve water body segmentation in satellite imagery.

📁 Dataset
Sentinel-2 high-resolution satellite imagery paired with binary water body masks.
Masks generated using NDWI (Normalized Difference Water Index) with a tuned threshold for clean water/non-water separation.
Covers diverse landscapes: urban, rural, and forested regions.
Source: Satellite Images of Water Bodies (Kaggle)
⚙️ Tech Stack
Python, TensorFlow, Keras
Attention U-Net, SNUNet-CD
OpenCV (HSV masking, morphological operations)
NumPy, Matplotlib