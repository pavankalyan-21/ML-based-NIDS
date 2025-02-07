Network Intrusion Detection System (NIDS) using Machine Learning

Project Overview

This project implements a Network Intrusion Detection System (NIDS) using a RandomForest-based Machine Learning model. The system is designed to operate in real-time to detect malicious network activity. It leverages the CIC-Collection dataset for training and evaluation.

Features

Real-time Intrusion Detection: Continuously analyzes network traffic to detect intrusions.

Machine Learning-based Approach: Uses a trained RandomForest model for anomaly detection.

Automated Reporting: Generates reports on identified threats for further analysis.

Scheduler Integration: Automates model execution and network scanning.

File Structure

IDS_ML_Model.ipynb - Jupyter Notebook containing the ML model training and evaluation.

NIDS.ipynb - Implementation of the real-time intrusion detection system.

Installation & Setup

Clone the Repository

git clone <repository-url>
cd NIDS-ML-Project

Install Dependencies

pip install -r requirements.txt

Run the Detection System

python NIDS.py

Dataset

The model is trained on the CIC-Collection dataset, which includes various network traffic types (normal and attack traffic). Ensure the dataset is downloaded and preprocessed before training.

Future Enhancements

Improve detection accuracy using Deep Learning.

Optimize real-time processing for large-scale networks.

Enhance user interface for better threat visualization.
