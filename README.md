# ⚽ Automated Event Detection in Football: A Partial Replication Study

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![YOLOv8](https://img.shields.io/badge/YOLO-v8-green)
![Computer Vision](https://img.shields.io/badge/Computer-Vision-red)
![License](https://img.shields.io/badge/License-MIT-yellow)

## Overview
This repository contains the implementation artifacts for the **Technical Report** (Experimental Validation). 

The project performs a **Partial Replication** of the methodology proposed by *Muller et al. (2024)*, aiming to validate the performance of "tracking-by-detection" pipelines in professional football analytics. Specifically, we investigate the trade-offs of upgrading the detection architecture to **YOLOv8** while running on accessible cloud hardware (Google Colab T4 GPU).

### Objectives
1.  **Replication:** Reproduce the player tracking pipeline using state-of-the-art anchor-free models.
2.  **Validation:** Assess tracking stability (BoT-SORT) and detection density on wide-angle broadcast footage.
3.  **Benchmarking:** Measure inference latency and computational cost on non-industrial hardware.

---

## Methodology & Architecture

The pipeline consists of three main stages:
1.  **Ingestion:** Processing 1080p broadcast video frames.
2.  **Inference (YOLOv8m):** Detecting objects (Class 0: Person, Class 32: Sports Ball).
3.  **Tracking (BoT-SORT):** Associating detections across frames using Kalman Filters and visual embeddings to maintain unique Player IDs.

**Output:** The system generates a video with visualized trajectory history ("tails") and a CSV log of performance metrics.

---

## Repository Structure

- `replication_study.ipynb`: The main Jupyter Notebook containing the full experiment pipeline.
- `requirements.txt`: List of Python dependencies.
- `stats.csv`: Generated performance metrics from the experiment.
- `graph.png`: Visualization of FPS and Player Count.
- `processed.jpg`: Example output frame used for visual validation.
- `README.md`: Project documentation.

---

## How to Run (Reproducibility)

The easiest way to reproduce the results is using **Google Colab** to leverage GPU acceleration.

### Option 1: Google Colab (Recommended)
1.  Download `replication_study.ipynb` from this repository.
2.  Go to [Google Colab](https://colab.research.google.com/) and upload the notebook.
3.  **Important:** Go to `Runtime` > `Change runtime type` > Select **T4 GPU**.
4.  Run the cells sequentially.
5.  When prompted, upload a short football video clip (e.g., `sample.mp4`).
6.  The notebook will generate and download `replication_result.mp4`, `stats.csv`, and `graph.png`.

### Option 2: Local Installation
If you have a GPU-enabled local machine:

```bash
# Clone the repository
git clone [https://github.com/Raul932/KBS-Tech-Report.git](https://github.com/Raul932/KBS-Tech-Report.git)
cd KBS-Tech-Report

# Install dependencies
pip install ultralytics opencv-python pandas matplotlib

# Run the notebook
jupyter notebook replication_study.ipynb
