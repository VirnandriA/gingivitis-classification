# Gingivitis Image Classification

An image classification project for **gingivitis screening** using **AlexNet** and **MobileNetV2**. The project evaluates the effect of image sharpening using **Unsharp Masking** and compares model performance between raw and sharpened image inputs.

> **Note:** This project is intended as a research/academic prototype for image classification and screening support, **not as a medical diagnostic tool**.

---

## 📌 Overview

Gingivitis is an inflammatory condition of the gums that can be identified through visual characteristics in intraoral images. This project explores the use of deep learning-based image classification to distinguish between **Gingivitis** and **Non-Gingivitis** from intraoral images.

Two convolutional neural network architectures are evaluated:

* **AlexNet**
* **MobileNetV2**

Each architecture is tested under two image preprocessing scenarios:

1. **Raw** — images without sharpening
2. **Sharp** — images processed using Unsharp Masking

The models are trained and evaluated using a **70:15:15 dataset split** and subsequently evaluated using external clinical images.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Develop an image classification pipeline for gingivitis screening.
* Compare the performance of **AlexNet** and **MobileNetV2**.
* Evaluate the effect of **Unsharp Masking** on classification performance.
* Measure model performance using standard classification metrics.
* Perform external validation using images outside the training dataset.

---

## 📂 Dataset

The dataset consists of **1,200 intraoral images** divided into two classes:

| Class          | Number of Images |
| -------------- | ---------------: |
| Gingivitis     |              600 |
| Non-Gingivitis |              600 |
| **Total**      |        **1,200** |

The dataset is divided into:

| Dataset    | Proportion |
| ---------- | ---------: |
| Training   |        70% |
| Validation |        15% |
| Testing    |        15% |

The test set is kept separate from the training and validation data and is used for the final model evaluation.

---

## 🔬 Methodology

The overall workflow of the project is:

```text
Dataset
   │
   ▼
Data Understanding
   │
   ▼
70% Training
15% Validation
15% Testing
   │
   ▼
Image Preprocessing
   │
   ├───────────────┐
   │               │
   ▼               ▼
Raw Image     Unsharp Masking
   │               │
   ▼               ▼
AlexNet        AlexNet
   │               │
MobileNetV2    MobileNetV2
   │               │
   └───────┬───────┘
           ▼
      Model Evaluation
           │
           ▼
 External Clinical Validation
```

---

## 🖼️ Image Preprocessing

All images are resized to:

```text
224 × 224 × 3
```

Pixel values are normalized to the range:

```text
0–1
```

by dividing pixel values by `255.0`.

Two preprocessing scenarios are evaluated.

### Raw

The original image is resized and normalized without additional sharpening.

### Unsharp Masking

For the sharpening scenario, **Unsharp Masking** is implemented using OpenCV.

The process applies Gaussian Blur and combines the original image with the blurred image:

```python
blurred = cv2.GaussianBlur(
    img,
    (5, 5),
    1.0
)

img = cv2.addWeighted(
    img,
    1.5,
    blurred,
    -0.5,
    0
)
```

This produces four experimental scenarios:

| Model             | Input           |
| ----------------- | --------------- |
| AlexNet Raw       | Raw Image       |
| AlexNet Sharp     | Unsharp Masking |
| MobileNetV2 Raw   | Raw Image       |
| MobileNetV2 Sharp | Unsharp Masking |

---

## 🧠 Models

### AlexNet

AlexNet is implemented as a custom convolutional neural network consisting of convolutional, max-pooling, flattening, dense, and dropout layers.

The model receives an input size of:

```text
224 × 224 × 3
```

and performs binary classification between:

```text
Gingivitis
Non-Gingivitis
```

### MobileNetV2

MobileNetV2 is used as the second architecture for comparison. It is evaluated using the same raw and sharpened image scenarios.

The comparison allows the performance of a lightweight architecture such as MobileNetV2 to be evaluated against the custom AlexNet implementation.

---

## ⚙️ Training Configuration

The models are trained using the following general configuration:

* Input size: **224 × 224 × 3**
* Batch size: **32**
* Epochs: **30**
* Optimizer: **AdamW**
* Random seed: **42**
* Binary classification

The validation set is used during training to monitor model performance, while the test set remains separate for final evaluation.

---

## 📊 Evaluation

Model performance is evaluated using several classification metrics:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix
* Test Loss

The project evaluates the four experimental scenarios independently:

```text
AlexNet Raw
AlexNet Sharp
MobileNetV2 Raw
MobileNetV2 Sharp
```

---

## 🧪 External Clinical Validation

In addition to evaluation using the held-out test dataset, the project includes **external clinical validation** using images outside the original dataset.

The purpose of this evaluation is to examine how the trained models perform on external intraoral images that were not part of the original dataset.

The external validation is intended to provide an additional perspective on model performance beyond the internal test set.

---

## 📈 Result

The best-performing configuration in the reported experiment was **MobileNetV2**, which achieved:

**89.44% test accuracy**

The experiment also compares the effect of Unsharp Masking by evaluating both raw and sharpened image inputs across AlexNet and MobileNetV2.

Detailed evaluation results, including Accuracy, Precision, Recall, F1-Score, and Confusion Matrix, are available in the accompanying notebook.

---

## 🛠️ Technologies

The project was developed using:

* Python
* TensorFlow / Keras
* OpenCV
* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* Google Colab

---

> Dataset files are not included in this repository because the original dataset is used for research purposes.

---

## 🚀 Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/your-username/gingivitis-classification.git
```

### 2. Open the notebook

Open:

```text
notebooks/gingivitis_.ipynb
```

using Google Colab or Jupyter Notebook.

### 3. Prepare the dataset

Place the dataset according to the directory structure expected by the notebook:

```text
DATASET_UJICOBA/
├── Gingivitis/
└── Non_Gingivitis/
```

### 4. Run the notebook

Run the notebook cells sequentially:

```text
Environment Setup
        ↓
Data Understanding
        ↓
Dataset Splitting
        ↓
Data Pipeline
        ↓
Model Building
        ↓
Model Training
        ↓
Model Evaluation
        ↓
External Validation
```

---

## ⚠️ Disclaimer

This project is developed for **research and educational purposes**. The model is not intended to replace professional dental examination, diagnosis, or clinical decision-making.

Predictions generated by the model should not be interpreted as a definitive medical diagnosis.

---

## 👨‍💻 Author

**Virnandri Andira**

Computer Science / Informatics Engineering

Interests:

* Artificial Intelligence
* Computer Vision
* Machine Learning
* Deep Learning
* AI Application Development
