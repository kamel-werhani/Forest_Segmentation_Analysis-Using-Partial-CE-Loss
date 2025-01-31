# Forest Segmentation using Point Annotations and Partial-CE-Loss

## Overview
This repository contains the implementation and analysis of a deep learning model for **forest segmentation** using **point annotations** instead of dense masks. The study investigates how **point annotation density** and **learning rate** affect model performance when trained with a custom **Partial Cross-Entropy Loss**.

## Project Structure
```
├── Forest_Segmentation_Analysis-Using-Partial-CE-Loss.ipynb  # Jupyter Notebook with model training
└── README.md                                  # Project documentation
```

## Methodology
### 1. Partial Cross-Entropy Loss
A custom **Partial Cross-Entropy Loss** function is implemented with a **Focal Loss component** to handle class imbalance in remote sensing data.

### 2. Model Architecture
- **Base Model**: Pre-trained **ResNet50** modified for segmentation.
- **Adjustments**:
  - Replaced `conv1` layer to adapt to input images.
  - Fully connected layer changed to output binary classification.

### 3. Data Preparation
- **Dataset**: RGB aerial images + segmentation masks.
- **Processing**:
  - Images resized to **256x256 pixels**.
  - Normalized using **ImageNet mean & standard deviation**.
  - **Point annotations** simulated from segmentation masks.

### 4. Training Details
- **Optimizer**: Adam (`momentum=0.9`, `weight_decay=1e-3`)
- **Batch Size**: 16
- **Epochs**: 10
- **Loss Function**: Custom Partial Cross-Entropy Loss
- **Experiments**:
  - **Point Sampling**: Tested 10, 50, 100, 200 points per image.
  - **Learning Rate Study**: Compared `1e-3`, `1e-4`, and `1e-5`.

## Key Findings
- **Best annotation density**: **50 points per image** (balance of accuracy & annotation effort).
- **Optimal learning rate**: **1e-4** (best stability and convergence).

## Results
The experiments showed:
- **50 points per image** achieved the best balance between accuracy and annotation effort.
- **Higher annotation densities (100+ points)** led to diminishing returns in performance improvement.
- **Learning rate 1e-4** provided the best trade-off between stability and convergence speed.
- **Higher learning rates (1e-3)** caused instability, while **lower learning rates (1e-5)** required significantly more epochs to converge.

## Getting Started
### Requirements
- You can run the notebook on kaggle notebook or colab
- All the requirements are mentioned in the notebook.

### Installation
Clone the repository:
```sh
 git clone https://github.com/kamel-werhani/Forest_Segmentation_Analysis-Using-Partial-CE-Loss.git
```


### Running the Notebook
Open the Jupyter Notebook:
```sh
Forest_Segmentation_Analysis-Using-Partial-CE-Loss.ipynb
```

## License
This project is licensed under the MIT License - see the LICENSE file for details.

