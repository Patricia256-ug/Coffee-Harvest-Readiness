# Coffee Harvest Readiness Estimation Using Computer Vision

## Project overview
This project uses a fine-tuned YOLOv8m object detection model
to identify coffee cherries by maturity stage:

- Unripe
- Ripening
- Ripe
- Spoilt

A Harvest Readiness Index (HRI) is calculated from predicted
maturity-class counts.

## Dataset
The project uses the coffee images from the Coffee and Cashew
Nut Dataset.

Dataset source:
https://data.mendeley.com/datasets/r46c6bpfpf/1

The dataset images are not included in this repository.

## Model
Architecture: YOLOv8m
Training device: CPU
Training completed: 27 epochs
Input image size: 640 x 640

The trained model weights are not included in this repository.
Place the best.pt checkpoint in the project weights folder
before running inference.

## HRI calculation

HRI (%) = ((N_r + 0.5*N_ri) /
           (N_u + N_ri + N_r)) * 100

Spoilt cherries are excluded from the HRI calculation.

The HRI is an estimated maturity-distribution index and has
not been validated against actual field harvest readiness.

## Evaluation
The model was evaluated on 442 test images.

Overall results:
- Precision: 58.25%
- Recall: 32.33%
- mAP@50: 30.52%
- mAP@50-95: 12.19%

## Project contents
- scripts/: project scripts
- notebooks/: Jupyter notebooks
- datasets/: dataset configuration only
- results/evaluation/: evaluation plots and results
- results/predictions/: sample predictions and HRI results
- report/: available report documents and LaTeX files

## Reproduction
Install the dependencies listed in requirements.txt.
Download the dataset and model checkpoint separately.
Update the paths in the configuration files if necessary.
