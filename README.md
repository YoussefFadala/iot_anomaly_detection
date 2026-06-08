# Anomaly Detection in IoT Networks
**MSc Cybersecurity FMP — Youssef Fadala (N1411761)**
Supervisor: Daniyal Haider — Nottingham Trent University

## Overview
A comparison of four anomaly-detection algorithms (Isolation Forest,
One-Class SVM, Autoencoder, Deep SAD) on the IoT-23 dataset.

## Requirements
- Python 3.11+
- See requirements.txt

## Setup
    git clone https://github.com/yourusername/iot_anomaly_detection.git
    cd iot_anomaly_detection
    python -m venv venv
    venv\Scripts\activate
    pip install -r requirements.txt

## Data
Download IoT-23 from: https://www.stratosphereips.org/datasets-iot23
Place extracted files in data/raw/. Do not commit data files.

## Running Experiments
    mlflow ui                        # Start local tracking UI
    python src/preprocess.py         # Run preprocessing
    python src/models/iforest.py     # Run a model

## Reproducing Results
All experiment parameters are logged in EXPERIMENTS.md.
All notebooks are committed with outputs cleared.
