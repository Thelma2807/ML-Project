IMU Anomaly Detection for UR3e Robotic Arm (TinyML)
Project Description
This project focuses on implementing a real-time anomaly detection system for a collaborative robotic arm (UR3e) using Inertial Measurement Unit (IMU) data. The primary objective is to enhance industrial safety by identifying external disturbances—such as collisions, simulated earthquakes, sensor failures, and payload errors—using lightweight Machine Learning models compatible with TinyML constraints.

Dataset Access
Due to the significant size of the raw sensor data, the dataset files are not hosted directly in this GitHub repository. You must download the dataset from Kaggle here: 👉 https://www.kaggle.com/datasets/hkayan/industrial-robotic-arm-imu-data-casper-1-and-2

Please unzip the downloaded files and place them in the project's root directory before running the notebook.

Installation
To replicate the environment and run the analysis, please install the necessary dependencies using the provided requirements file:
pip install -r requirements.txt

Technical Approach
The data processing pipeline handles tri-axial accelerometer, gyroscope, and magnetometer signals. A key challenge addressed in this project is sensor drift across different recording sessions, which we solved using a "Source-wise Standardization" technique.

The continuous signals are segmented into sliding windows of 50 samples with a 50% overlap. From these windows, we extract low-cost statistical features (Mean, Standard Deviation, Minimum, Maximum, and RMS) based on the Euclidean norms of the physical signals.

Models and Validation
We utilized a strict GroupShuffleSplit evaluation strategy, splitting the dataset by file rather than by random samples. This prevents temporal data leakage and ensures the model generalizes well to new recording sessions.

We established a baseline using a Random Forest model due to its interpretability and speed. To improve performance and robustness, we developed an Ensemble Learning architecture. This includes a Voting Classifier that aggregates predictions from:

A Random Forest (Baseline)

A Bagging SVM (using an RBF kernel to capture non-linearities)

Bagging Decision Trees

Results
The final Voting Classifier achieves an accuracy of approximately 98% on unseen test files. To ensure suitability for industrial environments, the system operates with a strict probability threshold (0.95), prioritizing high precision to minimize false alarms.

⚠️ Development Note
The majority of the development, testing, and model training for this project was conducted on Google Colab to leverage cloud resources. Consequently, the Git commit history in this repository may appear sparse compared to the actual development timeline.
