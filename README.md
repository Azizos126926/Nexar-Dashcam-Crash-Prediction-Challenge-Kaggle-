# Nexar Dashcam Crash Prediction Challenge (Kaggle)
## 🏆 Results

- **Top 40 out of 280 participants**
- **Top 17% overall**
- Worked on it only last 5 days of the 3 months period for the challenge
  
## 🏁 Competition Overview

This repository contains my solution to the [Nexar Dashcam Crash Prediction Challenge](https://www.kaggle.com/competitions/nexar-collision-prediction/overview), a Kaggle competition focused on **anticipating traffic accidents** from dashcam video footage.

The task is to **predict collisions before they occur**, classifying each video as:

- Collision
- Near-miss (treated as positive)
- Normal driving (negative)

## 📦 Dataset

The dataset consists of dashcam videos labeled with event types and timestamps.

- **Training set**: 1,500 annotated videos  
  - 400 collisions  
  - 350 near-misses  
  - 750 normal driving (no incident)  
- **Each video includes**:
  - `event type`: collision / near-miss / none
  - `event time`: time of the event (if any)
  - `alert time`: earliest time a prediction is allowed

- **Test set**: 1,344 real-world driving videos, typically trimmed to show moments before an event

## 📊 Evaluation

Submissions are scored using **Mean Average Precision (mAP)** at three anticipation thresholds:

- 500 ms before event
- 1000 ms before event
- 1500 ms before event

The objective is not only to detect a collision but to **anticipate** it as early and accurately as possible.

## 📁 Submission Format

A valid CSV submission should look like this: id, probability

Where `score ∈ [0, 1]` is the predicted probability of a (near-)collision.

## 🔧 My Approach

This solution combines both spatial and temporal modeling using a two-branch architecture:

- **Frame-level feature extraction**:
  - Extract visual features from each frame using `EfficientNetB0`

- **Branch A**:
  - Average the frame features across the video
  - Feed into a tabular model like **XGBoost** for classification

- **Branch B**:
  - Feed the sequence of frame features into an **LSTM** to model temporal dynamics

- **Ensemble**:
  - Combine predictions from both branches using a **stacking ensemble**, improving generalization over baseline models



---


