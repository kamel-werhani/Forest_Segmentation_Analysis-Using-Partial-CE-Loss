# Forest Segmentation using Point Annotations

## Overview
This repository contains the implementation and analysis of a deep learning model for **forest segmentation** using **point annotations** instead of dense masks. The study investigates how **point annotation density** and **learning rate** affect model performance when trained with a custom **Partial Cross-Entropy Loss**.

## Project Structure
```
├── Kamel_Werhani_Technical_Assessement.ipynb  # Jupyter Notebook with model training
├── Kamel_Werhani_Technical_Report.pdf         # Technical report detailing methodology and results
├── README.md                                  # Project documentation (this file)
└── data/                                      # Dataset (not included)
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

## Getting Started
### Requirements
- Python 3.8+
- PyTorch
- OpenCV
- NumPy
- Matplotlib

### Installation
Clone the repository:
```sh
 git clone https://github.com/YOUR-USERNAME/Forest_Segmentation_Analysis.git
 cd Forest_Segmentation_Analysis
```

Install dependencies:
```sh
pip install -r requirements.txt  # If a requirements file is added
```

### Running the Notebook
Open the Jupyter Notebook:
```sh
jupyter notebook Kamel_Werhani_Technical_Assessement.ipynb
```

## Future Work
- Improve model robustness with adaptive learning rates.
- Explore alternative point annotation strategies.
- Deploy as a web-based interactive annotation tool.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Contact
For questions or collaborations, feel free to reach out!

---
*Happy coding! 🚀*
