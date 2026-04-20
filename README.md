# 🚗 Motion Deblurring of License Plate Images

> **Computer Vision Final Project** — Group **BufferOverflow** (Methqphore)

A complete pipeline for simulating, restoring, enhancing, and evaluating motion-blurred license plate images using classical frequency-domain techniques.

---

## 📋 Overview

Motion blur is a common degradation in traffic surveillance systems, making license plate recognition difficult. This project implements a **full deblurring pipeline**:

1. **Simulate** realistic motion blur on 50 real license plate images using parametric PSF kernels.
2. **Restore** degraded images using **Inverse Filtering** and **Wiener Filtering** in the frequency domain.
3. **Enhance** restored images with **CLAHE**, **Unsharp Masking**, and **Adaptive Binarization**.
4. **Evaluate** quality using **PSNR** and **SSIM** metrics, with visual comparison panels and statistical analysis.

---

## 📁 Repository Structure

```
├── data/
│   ├── original/              ← 50 input license plate images
│   └── README.txt             ← Dataset description and source attribution
│
├── code/
│   └── motion_deblurring.ipynb  ← Main notebook (clean, modular, fully runnable)
│
├── report.pdf                 ← project report
├── .gitignore
└── README.md                  ← This file
```

### Generated folders (created by running the notebook)

| Folder | Description |
|--------|-------------|
| `data/blurred/` | Synthetically motion-blurred images (4 lengths × 4 angles × 50 images = 800) |
| `data/kernels/` | Visualizations of the motion blur PSF kernels |
| `data/restored_inverse/` | Images restored using naive inverse filtering |
| `data/restored_wiener/` | Images restored using Wiener filtering |
| `data/enhanced/` | Post-processed images (CLAHE + sharpening applied to Wiener results) |
| `data/thresholded/` | Binarized images via adaptive Gaussian thresholding |
| `data/comparisons/` | Side-by-side panels: Original \| Blurred \| Inverse \| Wiener |
| `data/enhanced_comparisons/` | Enhancement pipeline panels: Wiener \| CLAHE \| Sharpened \| Thresholded |
| `data/metrics/` | CSV files with per-image PSNR/SSIM scores and summary statistics |

---

## 🚀 How to Run

### Prerequisites

```bash
pip install numpy opencv-python matplotlib pandas scikit-image
```

### Run the notebook

```bash
cd code/
jupyter notebook motion_deblurring.ipynb
```

Run all cells from top to bottom. The notebook is self-contained and will:
- Read images from `data/original/`
- Generate all intermediate and output files
- Display inline visualizations and metrics

---

## 🔬 Key Concepts & Course References

| Concept | Application in Project |
|---------|----------------------|
| **Convolution** | Motion blur applied via 2D kernel convolution |
| **Fourier Transform (DFT)** | Image and kernel transformed to frequency domain for filtering |
| **PSF / OTF** | Point Spread Function modeled as a rotated line; converted to OTF via FFT |
| **Inverse Filtering** | Direct deconvolution: F̂ = G / H (sensitive to noise) |
| **Wiener Filtering** | Regularized restoration: F̂ = (H* / (\|H\|² + K)) · G |
| **CLAHE** | Contrast-Limited Adaptive Histogram Equalization for local contrast |
| **Unsharp Masking** | Edge sharpening via high-frequency emphasis |
| **Adaptive Thresholding** | Binarization for character segmentation |
| **PSNR / SSIM** | Quantitative image quality assessment metrics |

---

## 📊 Sample Results

| Metric | Blurred | Inverse Filter | Wiener Filter |
|--------|---------|----------------|---------------|
| Mean PSNR | 24.65 dB | 9.69 dB | 22.21 dB |
| Mean SSIM | 0.739 | 0.121 | 0.730 |

> Wiener filtering significantly outperforms naive inverse filtering, which amplifies noise and produces severe ringing artifacts.

---

## 📄 Dataset

**Source:** [Azerbaijan License Plates (Cropped)](https://www.kaggle.com/datasets/bariscelikw/azerbajian-license-plates-cropped)  
**Count:** 50 cropped license plate images  
**Format:** JPEG, resized to 256×128 grayscale during processing  

See [`data/README.txt`](data/README.txt) for full details.

---

## 👥 Authors

- **Methqphore** — Group **BufferOverflow**

---

*Computer Vision — S8 Final Project*
