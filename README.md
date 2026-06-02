# Indian-vehicle-number-plate-ocr

## Overview

This project presents a Deep Learning-based Automatic Number Plate Recognition (ANPR) system for Indian vehicles.

The system consists of three major tasks:

1. Vehicle Detection
2. Number Plate Detection
3. Optical Character Recognition (OCR)

Additionally, a VGG19-based classifier was developed to classify vehicle number plates into White, Yellow and Green categories.


## Project Objectives

- Detect vehicles from traffic images.
- Detect and localize number plates.
- Extract alphanumeric characters from number plates.
- Classify number plate color.
- Build a complete ANPR pipeline for Indian vehicles.
  
<img width="275" height="183" alt="rrrr" src="https://github.com/user-attachments/assets/670549d0-8b21-491d-a4f8-8bd31c219846" />

---
## Hardware and Software Setup

### Hardware

| Component | Specification |
|------------|-------------|
| CPU RAM | 12.7 GB |
| GPU | NVIDIA T4 (15 GB) |
| Disk | 107.7 GB |

### Software

- Python
- TensorFlow
- PyTorch
- OpenCV
- Ultralytics YOLOv8
- EasyOCR
- Google Colab

---
## Dataset

The project uses:

| Dataset Type | Images |
|--------------|---------|
| Synthetic Number Plates | 10000 |
| Real Number Plates | 355 |
| Detection Dataset | Kaggle Vehicle Dataset |

### Dataset Samples
<img width="300" height="80" alt="21BH0358T" src="https://github.com/user-attachments/assets/4b48abb9-d801-4727-b4b1-d86c246beb0c" />

<img width="320" height="100" alt="↑21A714323U" src="https://github.com/user-attachments/assets/1dd67103-1135-46cd-8d97-c999e57d62a5" />

<img width="300" height="80" alt="AN79XR1981" src="https://github.com/user-attachments/assets/aa4314b6-d849-46ae-a202-9dd51209df35" />

<img width="300" height="80" alt="8IOD4710" src="https://github.com/user-attachments/assets/5c11af1b-b64b-4590-93eb-bfd8588b8d93" />

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/real_dataset.png

---
# Activity 1: Number Plate Color Classification

## Objective

To classify vehicle number plates into:

- White (Private Vehicles)
- Yellow (Commercial Vehicles)
- Green (Electric Vehicles)

## Model Configuration

- VGG19 (ImageNet Pretrained)
- Input Size: 32×32×3
- Optimizer: Adam
- Loss: Sparse Categorical Crossentropy

## Results

| Metric | Value |
|----------|----------|
| Training Accuracy | 100% |
| Validation Accuracy | 100% |
| Training Loss | 3.1593e-05 |
| Validation Loss | 0 |

### Training & Validation Curves

<img width="1497" height="626" alt="vgg19_training_graph" src="https://github.com/user-attachments/assets/5bf0a1bb-a9cb-415c-b2ad-b7800435e001" />

---

# Activity 2: OCR Using CRNN

## CRNN Architecture

<img width="827" height="365" alt="Screenshot 2025-07-25 093320" src="https://github.com/user-attachments/assets/d130d8ad-73be-46ab-ac67-a629e8c44a0c" />


The OCR module combines:

- CNN layers for feature extraction
- BiLSTM layers for sequence learning
- CTC Loss for alignment-free training

---

## Experiment Comparison

| Exp | Activation | Optimizer | LR | Epochs | Train Acc | Val Acc |
|------|-----------|-----------|------|---------|----------|----------|
| 1 | SiLU | Adam | 1e-3 | 70 | 84.84% | 77.18% |
| 2 | ReLU | Adam | 1e-4 | 50 | 85% | 79% |
| 3 | ReLU | AdamW | 5e-3 | 100 | 90.90% | 90.79% |
| 4 | LeakyReLU | Adam | 5e-5 | 100 | 97.98% | 96.77% |

---

## Experiment 1 Results

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/crnn_exp1_accuracy_loss.png

---

## Experiment 2 Results

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/crnn_exp2_accuracy_loss.png

---

## Experiment 3 Results

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/crnn_exp3_accuracy_loss.png

---

## Experiment 4 Results (Best Model)

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/crnn_exp4_accuracy_loss.png

### Best Configuration

- Activation: LeakyReLU
- Optimizer: Adam
- Learning Rate: 5e-5
- Epochs: 100
- Dropout: 0.2

### Performance

| Metric | Value |
|----------|----------|
| Training Accuracy | 97.98% |
| Validation Accuracy | 96.77% |
| Training Loss | 0.0342 |
| Validation Loss | 0.0705 |

---

# Activity 3: YOLOv8 + EasyOCR Pipeline

## Pipeline

Vehicle Image
→ Vehicle Detection
→ Number Plate Detection
→ Plate Cropping
→ EasyOCR
→ Text Extraction

# Training & Validation Curves
https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/yolo_train_validation_accuracy.png

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/yolo_train_validation_loss.png

---

## Preprocessing

- Gaussian Blur
- RGB → HSV
- CLAHE
- HSV → RGB
- Grayscale Conversion
- Min-Max Normalization

---

## Hyperparameters

| Parameter | Value |
|------------|---------|
| Epochs | 100 |
| Image Size | 416×416 |
| Batch Size | 16 |
| Learning Rate | 0.0001 |
| Weight Decay | 1e-5 |

---

## Results

| Metric | Value |
|----------|----------|
| Accuracy | 91.5% |
| Box Loss | 1.1 |
| Classification Loss | 0.5106 |
| DFL Loss | 1.195 |

# Final ANPR Tool

## Tool Architecture

The final ANPR system consists of:

### Model 1

YOLOv8-n (Vehicle Detection): Identifies cars, bikes, buses, and trucks from an input image.

### Model 2

YOLOv8-n (Number Plate Detection): Crops number plates from detected vehicles.

### Model 3

CRNN OCR Module: Extracts alphanumeric text from the cropped plate images.

---

## Workflow

1. Detect Vehicles
2. Detect Number Plates
3. Crop Number Plates
4. Extract Text Using CRNN
5. Display Final Results

---

## Sample Outputs

### OCR Results

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/ocr_output.png

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/ocr_on_unlabeled_images.png

### Final Combined Output

https://github.com/rifakhan1/Indian-vehicle-number-plate-ocr/blob/main/final_output.png

---

# Limitations

- Heavy reliance on synthetic data.
- Limited real-world images.
- Performance decreases on:
  - Blur
  - Skew
  - Distortion
  - Green and Blue plates

- TrOCR could not be fine-tuned due to GPU limitations.

---

# Future Work

- Fine-tune TrOCR models.
- Increase real-world data collection.
- Add advanced augmentation.
- Implement regex-based OCR correction.
- Deploy as a web application.

---

# Applications

- Smart Traffic Monitoring
- Toll Booth Automation
- Vehicle Tracking
- Smart City Surveillance
- Parking Management

---

# Author

Rifa 

B.Tech (ECE-AI)

Indira Gandhi Delhi Technical University for Women (IGDTUW), New Delhi
