# Nuclei Segmentation in Microscopy Images

A classical image processing pipeline for detecting and segmenting cell nuclei from 16-bit grayscale microscopy images (U2OS cells, DAPI-stained), built using Python's scientific imaging stack.

## Overview

This project implements a 5-stage image segmentation pipeline to identify individual cell nuclei from raw microscopy scans, then evaluates the results against ground-truth instance label maps using standard segmentation metrics.

**Pipeline stages:**
1. **Normalisation** — scaling raw 16-bit images to a [0, 1] range
2. **Gaussian Blur** (σ = 2) — noise reduction
3. **Otsu Thresholding** — automatic binary segmentation
4. **Morphological Operations** — cleanup of binary mask
5. **Watershed Segmentation** — separating touching/overlapping nuclei into distinct instances

## Tech Stack

- **Python 3**
- **scikit-image** — filtering, morphology, watershed segmentation, feature extraction
- **scipy** (ndimage) — image processing utilities
- **NumPy** — array operations
- **Matplotlib** — visualisation
- **Pillow (PIL)** — image I/O

## Dataset

- `Microscopy_Data/im/` — 16-bit grayscale TIFF microscopy images
- `Microscopy_Data/gt/` — Ground-truth instance label maps (PNG, RGBA), where the R channel encodes per-pixel nucleus instance IDs

## Evaluation

Predicted segmentation masks are compared against ground truth using pixel-level metrics:
- **IoU (Intersection over Union)**
- **Dice Coefficient**
- **Sensitivity / Specificity**
- **Precision / Accuracy**

Mean, min, max, and standard deviation are reported across all test images, with **mIoU** as the primary evaluation metric.

## Visualisations

The notebook includes:
- Side-by-side comparison of raw images vs. ground truth masks
- Intermediate pipeline stage visualisation (normalisation → blur → threshold → morphology → watershed)
- Prediction vs. ground truth overlay with error maps (true positive / false positive / false negative)
- Bar chart, line chart, and radar chart summarising metric performance across all images

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook nuclei_segmentation.ipynb
```

## Future Improvements

- Compare against a deep learning approach (e.g. U-Net) for benchmarking
- Add data augmentation to test pipeline robustness across varied imaging conditions
- Extend evaluation to a larger, more diverse dataset

---
*Built as part of my ongoing learning in image processing and computer vision.*
