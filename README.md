Network Intrusion Detection System (NIDS) - Real-time Detection with Random Forest
Overview
This project implements a real-time Network Intrusion Detection System (NIDS) that uses machine learning to detect malicious network traffic. The system uses a Random Forest classifier trained on the CICIDS 2018 dataset. It leverages Scapy to capture network packets and classifies them as either benign or malicious. The model is designed to handle class imbalance with the use of SMOTE (Synthetic Minority Over-sampling Technique), and it is capable of blocking malicious IP addresses using iptables.

Requirements
Libraries:
pandas: For data manipulation and analysis.
numpy: For numerical operations.
scikit-learn: For machine learning model training and evaluation.
imblearn: For handling class imbalance using SMOTE.
scapy: For packet sniffing and network traffic analysis.
joblib: For saving and loading trained models.
logging: For logging network events.
datetime: For handling timestamps.
time: For handling timing operations.
Installation:
To install the required libraries, you can use the following pip commands:

bash
Copy
pip install pandas numpy scikit-learn imbalanced-learn scapy joblib
Usage
1. Data Preprocessing & Model Training:
The first section of the code processes the CICIDS 2018 dataset and trains a RandomForestClassifier on the features.

Load the dataset: The dataset is loaded from a CSV file.
Data cleaning: Duplicates are removed, and missing values are handled.
Feature Engineering: Categorical features are label-encoded and numerical features are standardized.
SMOTE: Synthetic minority over-sampling is applied to address class imbalance.
Model Training: A RandomForestClassifier is trained on the resampled data.
Model Evaluation: The trained model is evaluated using validation and test datasets, and accuracy scores are printed.
Model Saving: The trained model is saved to a .pkl file using joblib for later use in the real-time detection system.
2. Real-Time Intrusion Detection:
Once the model is trained and saved, it is used for real-time network packet sniffing and intrusion detection.

Packet Sniffing: The scapy.sniff() function captures network packets.
Feature Extraction: Features like IP addresses, protocol, TCP flags, and packet lengths are extracted from the captured packets.
Flow Tracking: Active network flows are tracked by associating packets with unique flow identifiers.
Prediction: The model predicts whether a flow is benign or malicious based on the extracted features.
Logging: Detection results (malicious or benign) are logged to a file (nids_log.txt) and printed to the console.
Automated Response: Malicious flows trigger an action to block the source IP using iptables (commented out for safety).
Periodic Flow Cleanup: Flows are cleaned up after a set timeout period.
3. Starting the Real-time Detection:
After training and saving the model, you can start the real-time detection system using the following steps:

Ensure the trained model file (nids_model.pkl) is in the working directory.
Run the real-time detection script:
This will start sniffing network packets, extracting features, making predictions, and logging the results.
If a malicious packet is detected, it will log the event and optionally block the source IP.
Example:
To run the real-time detection:

bash
Copy
python real_time_nids.py
Configuration:
Flow Timeout: The timeout for active flows is set to 60 seconds (adjustable via FLOW_TIMEOUT).
Logging: Logs are saved in nids_log.txt and include details like detection timestamp, flow information, and whether the traffic is malicious or benign.
Automated Response: Malicious IPs can be blocked by uncommenting the iptables line in the block_ip function.
Notes:
Model File: Ensure that the model file (nids_model.pkl) is located in the same directory as the real-time detection script or provide the correct path.
System Requirements: The system requires sufficient privileges (administrator/root) to modify network firewall rules (iptables).
Real-time Traffic: Make sure you are running this script on a system that has access to the network you want to monitor.
Testing: The script uses a trained model for predictions. If no malicious traffic is detected in your network, you will see "Benign" traffic logs.
Example Output:
plaintext
Copy
Starting real-time Network Intrusion Detection System (NIDS)...
[ALERT] Detected Malicious traffic from 192.168.0.1 to 192.168.0.2 with protocol TCP
Blocking IP: 192.168.0.1
Troubleshooting:
Model Loading Issue: If the model cannot be loaded, ensure that the file path is correct and the model was saved properly.
Permissions: The block_ip function uses system-level commands (iptables) to block malicious IP addresses, so root permissions may be required to execute them.
Flow Timeout: Adjust FLOW_TIMEOUT if flows are being prematurely removed or not cleaned up properly.
Future Improvements:
Enhance feature extraction to include additional network traffic attributes.
Implement additional machine learning models for comparison.
Provide a web interface for monitoring and control of the NIDS.
