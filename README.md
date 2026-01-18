# Enhanced Lesion Segmentation for Diabetic Retinopathy Screening

## Overview

Diabetic retinopathy (DR) is one of the leading causes of vision loss worldwide, and early detection of retinal lesions such as microaneurysms, exudates, and hemorrhages is critical for timely treatment. Manual screening is time-consuming and subject to inter-observer variability, motivating the need for reliable automated systems.

This project presents EnhancedUNet, a deep learning–based framework for fine-grained retinal lesion segmentation using fundus images. The system integrates:

- A multi-scale image preprocessing pipeline to enhance lesion visibility  
- A U-Net–based architecture with lesion-specific attention mechanisms  
- Class-balanced sampling and loss functions to handle extreme class imbalance  

The model is evaluated on the DDR dataset and demonstrates substantial improvements over strong baselines such as DeepLab-v3+, particularly for small and rare lesions like microaneurysms.

---

## Key Contributions

- Multi-scale preprocessing pipeline including CLAHE contrast enhancement, vessel suppression, and unsharp masking to improve visibility of small lesions  
- EnhancedUNet architecture with dual-stage, lesion-specific attention modules focused on microaneurysm detection  
- Class-balanced training strategy using weighted sampling and a combined Cross-Entropy + Dice loss  
- Post-processing refinement using class-specific morphological operations  
- Significant performance gains on the DDR dataset:
  - Mean IoU improved from 0.179 to 0.312  
  - Mean AP improved from 0.301 to 0.367  
  - Microaneurysm AP improved from 0.020 to 0.109  

---

## Method Overview

The full pipeline consists of:

### 1. Preprocessing
- CLAHE-based contrast enhancement  
- Multi-kernel morphological vessel suppression  
- Unsharp masking of the green channel for microaneurysm sharpening  

### 2. Model Architecture
- ResNeXt-101 encoder  
- SCSE-enhanced U-Net decoder  
- Dual-stage attention modules applied to the microaneurysm channel  
- Five-class output: background, MA, EX, SE, HE  

### 3. Training Strategy
- Weighted random sampler to oversample microaneurysm-positive images  
- Combined Cross-Entropy + Dice loss with aggressive class reweighting  
- OneCycleLR scheduler, AdamW optimizer, and early stopping  

### 4. Post-processing
- Class-specific morphological filtering to clean predicted masks before evaluation  

---

## Dataset

- DDR (Diabetic Retinopathy Dataset)
- 757 fundus images with pixel-level annotations for:
  - Microaneurysms (MA)
  - Hard Exudates (EX)
  - Soft Exudates (SE)
  - Hemorrhages (HE)
- Split:
  - 50% training
  - 20% validation
  - 30% testing

---

## Results

### Overall Performance (DDR Test Set)

| Model        | mIoU  | mAP  |
|--------------|-------|-------|
| DeepLab-v3+  | 0.179 | 0.301 |
| EnhancedUNet | 0.312 | 0.367 |

### Per-Lesion Performance

| Lesion | IoU (Baseline) | IoU (Ours) | AP (Baseline) | AP (Ours) |
|--------|----------------|------------|---------------|-----------|
| MA     | 0.0325         | 0.0382     | 0.0205        | 0.1094    |
| EX     | 0.3118         | 0.2609     | 0.5634        | 0.3154    |
| SE     | 0.2295         | 0.6607     | 0.4359        | 0.6828    |
| HE     | 0.1425         | 0.2898     | 0.1842        | 0.3612    |

---

## Project Structure

Enhanced-Lesion-Segmentation-for-Diabetic-Retinopathy-Screening/
├── examples/
├── results/
├── metrics.txt
├── training_history.png
├── README.md


---

## Usage

This repository focuses on research results, visualizations, and experimental outputs associated with the EnhancedUNet project.

If you are reproducing or extending the work:
- Refer to the paper or report for full training and preprocessing details  
- Use the provided metrics and examples to validate correctness  
- Integrate the method into your own training pipeline as needed  

---

## Research Context

This project focuses on improving the clinical applicability and interpretability of deep learning–based diabetic retinopathy screening systems by enabling lesion-level segmentation rather than only image-level grading.

The approach emphasizes:
- Lesion-level interpretability  
- Robust detection of small and rare lesions  
- Practical improvements through targeted data processing and architecture design  

---

## License

This project is released for academic and research use.
