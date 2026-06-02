# Indian-vehicle-number-plate-ocr
Machine learning-based OCR system for extracting text characters from Indian vehicle number plates.

## Project Objective

To develop a machine learning-based model capable of accurately detecting and extracting alphanumeric characters from Indian vehicle number plates, enabling efficient and automated number plate recognition.
<img width="275" height="183" alt="rrrr" src="https://github.com/user-attachments/assets/670549d0-8b21-491d-a4f8-8bd31c219846" />

---

## Overview

This project explores Automatic Number Plate Recognition (ANPR) using deep learning and computer vision techniques. Two approaches were implemented and evaluated:

1. CRNN (Convolutional Recurrent Neural Network)
2. YOLOv8 + EasyOCR Pipeline

---

## Approach 1: CRNN Model
<img width="753" height="323" alt="Screenshot 2026-06-02 180527" src="https://github.com/user-attachments/assets/24cf08d0-1d21-4956-a854-41836bc930cc" />

### Configuration

- Activation Function: LeakyReLU
- Optimizer: Adam
- Learning Rate: 5e-5

### Dataset

- 8000 Synthetic Images
- 355 Real Vehicle Number Plate Images

### Results
<img width="308" height="90" alt="Screenshot 2025-07-22 102539" src="https://github.com/user-attachments/assets/57976717-5522-4c05-a3d8-372f4fb9f5dc" />

<img width="314" height="54" alt="Screenshot 2025-07-24 142654" src="https://github.com/user-attachments/assets/e96d7795-5644-4339-88d2-fbb4b185680c" />

| Metric | Value |
|----------|----------|
| Training Accuracy | 97.98% |
| Validation Accuracy | 96.77% |
| Training Loss | 0.0342 |
| Validation Loss | 0.0705 |

### Observations

The model achieved high accuracy on validation data. However, performance on real-world images was limited due to heavy reliance on synthetic training data.

---

## Approach 2: YOLOv8 + EasyOCR Pipeline

### Pipeline

Vehicle Image → YOLOv8 Detection → Plate Cropping → EasyOCR → Text Extraction

### Configuration

- Detection Model: YOLOv8
- OCR Engine: EasyOCR
- Activation Function: SiLU
- Optimizer: Adam
- Learning Rate: 0.0001

### Results
<img width="332" height="194" alt="Screenshot 2025-07-24 142755" src="https://github.com/user-attachments/assets/c946019b-0b81-40d4-9c78-89aef3618b76" />


| Metric | Value |
|----------|----------|
| Detection Accuracy | 91.5% |

### Observations

The pipeline successfully detected vehicle number plates and extracted text, though real-world variability affected OCR performance.

---

## Training Environment

- Google Colab
- 15GB GPU
- Python
- TensorFlow
- OpenCV
- EasyOCR
- YOLOv8

---

## Limitations

- TrOCR could not be fine-tuned due to GPU limitations.
- Heavy dependence on synthetic training data.
- Reduced performance on skewed, blurred, tilted, green, and blue number plates.
- Domain shift between synthetic and real-world images.

---

## Future Improvements

- Fine-tune transformer-based OCR models such as TrOCR.
- Collect more real-world vehicle images.
- Apply data augmentation techniques.
- Implement OCR post-processing using Regex validation.

---

## Applications

- Smart Traffic Monitoring
- Automated Toll Collection
- Vehicle Tracking Systems
- Parking Management Systems

---

## Author

Rifa

B.Tech (ECE-AI), IGDTUW
