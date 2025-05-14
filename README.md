# Concentration Analysis During Online Meetings (CNN-based)

This project implements a concentration analysis system for online meetings using **Convolutional Neural Networks (CNNs)**. It detects key facial features—**eye closure**, **yawning**, and **head rotation**—to estimate a participant’s concentration level. 

---

## Project Objective

To develop a computer vision system that analyzes recorded video of online meetings and provides concentration feedback based on facial cues.

---

## Background

Maintaining concentration during online lectures or remote work meetings is crucial for productivity. This system supports that goal by:

- Monitoring visual signs of engagement or drowsiness
- Offering data-driven feedback on concentration levels
- Enabling potential real-time analysis of participant focus

---

## Methodology

### Video Processing
- Input: A recorded video (e.g. `.mp4`) at 10 FPS
- Library: `OpenCV (cv2)`
- Each frame is processed to extract facial regions using Haar Cascade classifiers.

### Feature Detection
- **Eyes**: Detected and classified as open/closed
- **Mouth (Yawn)**: Detected and classified using CNN
- **Head Rotation**: Inferred when both eyes are not visible

### CNN Architecture

#### Eye Detection CNN
- Input: Grayscale, 256x256 images
- Layers:
  - Conv2D (32) → Conv2D (64) → Conv2D (128)
  - Activation: ReLU
  - Output: Softmax (binary classification)
- Trained for 20 epochs with:
  - Loss: Categorical crossentropy
  - Optimizer: Adam

#### Yawn Detection CNN
- Added Conv2D (16) layer at input
- Same structure as above
- Trained for 50 epochs

### Data Augmentation
- `shear_range = 0.2`
- `zoom_range = 0.2`

### Concentration Level Classification

| Concentration Level | Yawns | Head Rotations | Eyes Closed |
|---------------------|-------|----------------|-------------|
| **High**            | ≤2    | ≤2             | >3 sec      |
| **Medium**          | >3    | >3             | >5 sec      |
| **Low**             | >5    | >5             | >10 sec     |

---

## Results

- **Eye Detection CNN**
  - Validation Accuracy: **97.1%**
- **Yawn Detection CNN**
  - Validation Accuracy: **96.88%**

Models were tested using personal photos and recorded videos. Eye detection was mostly accurate, while yawn detection lagged slightly due to inconsistent mouth region detection.

---

## Limitations

- **Glasses**: May interfere with eye detection
- **Occlusion**: Hands/masks may hide the mouth
- **Speech**: May be misclassified as yawning
- **Lighting**: Affects model performance in low-light videos

---

