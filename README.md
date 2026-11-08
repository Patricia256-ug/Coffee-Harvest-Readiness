# Coffee-Harvest-Readiness
Coffee cherry maturity detection and harvest readiness estimation using YOLOv8m and computer vision in Uganda.

# Coffee Harvest Readiness Estimation Using Computer Vision in Uganda

## 1. Project Overview

This project focuses on estimating coffee harvest readiness through automated coffee cherry maturity detection using computer vision and deep learning.

A fine-tuned YOLOv8m object detection model is used to identify and classify coffee cherries into four maturity categories:

- Unripe
- Ripening
- Ripe
- Spoilt

The system calculates a Harvest Readiness Index (HRI) from the detected maturity-class distribution to provide an estimated indication of coffee maturity.

## 2. Project Objectives

- Develop a computer vision model for coffee cherry maturity detection.
- Classify coffee cherries into four maturity categories.
- Fine-tune a pretrained YOLOv8m model using coffee images.
- Evaluate detection performance using standard object detection metrics.
- Implement an HRI based on predicted maturity-class counts.

## 3. Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming language |
| PyTorch | Deep learning framework |
| YOLOv8m | Object detection |
| Ultralytics | Model training and inference |
| OpenCV | Image processing |
| Pandas | Data processing and HRI results |
| Jupyter Notebook | Development environment |

## 4. Dataset

The project uses coffee images from the Coffee and Cashew Nut Dataset.

**Dataset source:**  
https://data.mendeley.com/datasets/r46c6bpfpf/1

Only the coffee images were selected for model development.

The processed dataset contains 2,947 images distributed as follows:

| Dataset split | Images |
|---|---:|
| Training | 2,063 |
| Validation | 442 |
| Testing | 442 |
| **Total** | **2,947** |

The four detection classes are Unripe, Ripening, Ripe and Spoilt. The Coffee_tree class was excluded.

## 5. Model Development

The project uses a pretrained YOLOv8m model fine-tuned on the prepared coffee dataset.

**Training configuration:**

- Model: YOLOv8m
- Input image size: 640 × 640
- Batch size: 4
- Planned epochs: 50
- Completed epochs: 27
- Training device: CPU
- Data augmentation: Applied

The best-performing checkpoint is saved as `weights/best.pt`.

## 6. Model Evaluation

The model was evaluated using 442 independent test images.

| Evaluation metric | Result |
|---|---:|
| Precision | 58.25% |
| Recall | 32.33% |
| mAP@50 | 30.52% |
| mAP@50–95 | 12.19% |

The model achieved its strongest detection performance on Unripe cherries, moderate performance on Ripe cherries, and weaker performance on Ripening cherries. Spoilt cherries were not successfully detected.

## 7. Harvest Readiness Index (HRI)

The HRI is calculated from the predicted number of cherries in each maturity category.

\[
HRI(\%) =
\frac{N_r+0.5N_{ri}}
{N_u+N_{ri}+N_r}\times100
\]

Where:

- \(N_u\): Number of detected unripe cherries.
- \(N_{ri}\): Number of detected ripening cherries.
- \(N_r\): Number of detected ripe cherries.

The weighting assigns 0 to unripe, 0.5 to ripening and 1 to ripe cherries. Spoilt cherries are counted separately and excluded from the calculation.

The HRI is a derived maturity-distribution index, not a separately trained model output. It has not yet been validated against actual field harvest readiness or harvested-weight measurements.

## 8. Repository Structure

```text
Coffee-Harvest-Readiness/
│
├── datasets/
│   └── processed/
│       └── coffee_yolo/
│           └── coffee.yaml
│
├── notebooks/
│
├── scripts/
│
├── results/
│   ├── evaluation/
│   └── predictions/
│
├── report/
│
├── weights/
│   └── best.pt
│
├── README.md
├── requirements.txt
└── .gitignore
```

## 9. Installation and Usage

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/Coffee-Harvest-Readiness.git

cd Coffee-Harvest-Readiness
```

Create a Python virtual environment:

```bash
python -m venv coffee_env
source coffee_env/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Load the trained model:

```python
from ultralytics import YOLO

model = YOLO("weights/best.pt")

results = model.predict(
    source="path/to/coffee_image.jpg",
    imgsz=640,
    conf=0.25,
    save=True
)
```

## 10. Limitations

- The dataset has an imbalance in maturity-class representation.
- Detection performance is limited for Ripening and Spoilt cherries.
- The HRI has not been validated using ground-truth harvest-readiness measurements.
- Training was conducted using CPU resources.
- Performance requires further evaluation using diverse field conditions.

## 11. Proposed Improvements

- Collect additional images for underrepresented maturity classes.
- Improve detection accuracy through further fine-tuning.
- Validate the HRI using field observations and actual harvesting data.
- Develop a user-friendly application for practical farm use.
- Evaluate performance across different coffee varieties, locations and lighting conditions.

## 12. Project Significance

The proposed system demonstrates the potential of computer vision to support coffee maturity assessment and harvesting decisions in Uganda. It provides a foundation for developing automated tools that can assist farmers, farm managers and agricultural extension officers in monitoring coffee cherry maturity.


