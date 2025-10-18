# Gaze Estimation

> Real-time gaze direction estimation to monitor suspicious eye movements during online exams.

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-4285F4?style=for-the-badge&logo=google&logoColor=white)

## Project Overview
This project implements an accurate gaze estimation system using an enhanced ResNet-18 architecture, designed to detect eye movements that may indicate cheating during online exams. The model monitors where examinees are looking, detecting unauthorized glances away from the screen or toward prohibited materials.

## Features
- Estimates **yaw** and **pitch** of gaze vector in degrees
- Enhanced ResNet-18 with Tanh activation for normalized gaze vectors
- Adaptive cosine loss with dynamic weighting for bias correction
- MediaPipe integration for robust eye landmark detection
- Outputs both continuous gaze angles and normalized 3D gaze vectors

## Dataset & Model

- **Base Model**: ResNet-18 (pre-trained on ImageNet)  
- **Training Data**: SynthEyes synthetic dataset 
- **Gaze Range**: Yaw ±180°, Pitch ±50°  
- **Input**: Cropped eye regions (224×224), normalized with ImageNet stats  
- **Eye Extraction**: MediaPipe identifies 16 landmarks per eye for precise cropping and alignment  
- **Bias Mitigation**:  
  - Targeted augmentations (flips, noise, brightness shifts, small rotations) for rare gaze directions  
  - Dynamic loss weighting to upweight peripheral (|yaw| > 30°) and upward (pitch > 15°) gazes

## Performance Metrics 

| Metric                    |  Value |
|---------------------------|--------|
| Best Angular Error	      | 5.06° |
| Validation Loss           |	0.0065 |
| Inference Speed	          | 24 ms/image|
| Improvement over Baseline  |	70% error reduction |
