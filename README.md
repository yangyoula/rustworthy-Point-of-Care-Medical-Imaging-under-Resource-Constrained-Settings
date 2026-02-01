README.md
# Trustworthy Point-of-Care Medical Imaging under Resource-Constrained Settings

This repository provides the reference implementation for the experiments in the
paper:

**"From Algorithms to Clinical Translation: Trustworthy Point-of-Care Medical Imaging under Resource-Constrained Settings"**

The code focuses on evaluating reliability, calibration, and uncertainty-aware
deployment of medical imaging models under realistic point-of-care (PoC)
degradations.

---

## Overview

Medical imaging systems deployed in point-of-care environments often suffer from
hardware limitations, operator variability, and environmental noise. This repository
implements a **post-hoc reliability evaluation framework** that analyzes:

- Performance degradation under realistic PoC corruptions
- Confidence calibration behavior under distribution shift
- Uncertainty-aware selective prediction using MC-dropout

All models are trained on **clean data only** and evaluated under degraded conditions
without retraining or adaptation.

---

## Repository Structure



.
├── data/
│ ├── raw/ # Original clean images (not included)
│ ├── processed/ # Preprocessed inputs
│
├── degradations/
│ ├── resolution.py # Low-resolution simulation
│ ├── noise.py # Gaussian noise
│ ├── jpeg.py # JPEG compression
│ ├── blur.py # Motion blur
│ ├── crop.py # Spatial cropping
│ └── combined.py # Composed PoC degradations
│
├── models/
│ ├── resnet.py
│ ├── densenet.py
│ └── utils.py
│
├── calibration/
│ ├── temperature_scaling.py
│ ├── platt_scaling.py
│ └── isotonic.py
│
├── uncertainty/
│ ├── mc_dropout.py
│ └── risk_coverage.py
│
├── evaluation/
│ ├── metrics.py # AUROC, ECE, AURC
│ └── reliability.py # Reliability diagrams
│
├── experiments/
│ ├── run_eval.py
│ └── config.yaml
│
├── figures/
│ └── *.png # Generated plots
│
├── requirements.txt
└── README.md


---

## Environment Setup

Python ≥ 3.9 is recommended.

```bash
pip install -r requirements.txt


Main dependencies include:

PyTorch

torchvision

scikit-learn

numpy

matplotlib

Data

This repository assumes access to a public chest X-ray classification dataset
with predefined train/validation/test splits.

Due to licensing and privacy constraints, datasets are not included.
Please follow the original dataset providers’ instructions for access and usage.

All experiments are conducted using:

Training: clean images only

Evaluation: clean + simulated PoC degradations

Running Experiments
1. Apply PoC Degradations
python experiments/run_eval.py --apply_degradations


Supported degradations include:

Low resolution

Gaussian noise

JPEG compression

Motion blur

Spatial cropping

Contrast / gamma shifts

Combined corruptions

2. Evaluate Reliability and Calibration
python experiments/run_eval.py --evaluate


This computes:

AUROC

Expected Calibration Error (ECE)

Risk–Coverage curves

Area Under the Risk–Coverage Curve (AURC)

3. Generate Figures
python experiments/run_eval.py --plot


Figures include:

AUROC vs. degradation severity

ECE across conditions

Risk–coverage curves

Reliability diagrams

Reproducibility Notes

All results are averaged over multiple random seeds

Calibration parameters are fit on validation data only

No model retraining or domain adaptation is performed

Evaluation scripts log configuration, seeds, and metrics

Ethical Considerations

This code is intended solely for research purposes.
It does not constitute a clinical decision-support system and should not be used
for real-world diagnosis without appropriate regulatory approval and validation.

License

This repository is released for academic research use only.
Please ensure compliance with the licenses of all third-party datasets and libraries.

Acknowledgment

This implementation accompanies a MICCAI 2026 submission on reliable and
trustworthy medical imaging under deployment constraints.
