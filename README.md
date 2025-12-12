# AI Enabled Visa Status Prediction and Processing Time Estimator
Visa applicants often face long waiting times and uncertainty regarding the progress of their applications. This project aims to develop a predictive analytics system that estimates visa processing times based on historical data.

## Milestone 1: Data Collection & Preprocessing Module

This repository contains the first milestone of the AI-driven system designed to predict visa case outcomes and estimate processing times.
Milestone 1 focuses on building a robust data preprocessing pipeline that transforms raw administrative visa records into a machine-learning-ready dataset.

📁 Dataset Source
PERM Disclosure Data (FY2025 Q3)

Publicly available historical records of permanent labor certification applications, containing employer information, job characteristics, and adjudication results.

🔄 Data Processing Pipeline

The core preprocessing workflow is implemented in visa_processor.py, which performs cleaning, anonymization, feature engineering, and target variable preparation.

### 1. Data Cleaning & Anonymization

Key steps:

PII Removal
Removed personally identifiable information such as employer contact names, detailed addresses, and case numbers.

High-Cardinality Reduction
Dropped verbose text fields (e.g., JOB_TITLE, SPECIFIC_SKILLS) and replaced them with standardized occupational codes (SOC_CODE).

Missing Value Imputation
Filled missing categorical fields such as MINIMUM_EDUCATION and SKILL_LEVEL with "Unknown".

2. Feature Engineering
Derived features to enhance model learning capability:

Processing Time (Regression Target)
Difference in days between RECEIVED_DATE and DECISION_DATE.
Negative-duration records (errors) were removed.

Seasonality Features
Extracted:
I) SUBMISSION_MONTH
II) SUBMISSION_YEAR
     -> Useful for identifying workload peaks and bottlenecks.

Job Standardization
Created
SOC_MAJOR_GROUP → first two digits of SOC code
Groups job roles into broader categories (e.g., Computer & Mathematical Occupations).
Wage Normalization
Cleaned PW_WAGE field by removing currency symbols and formatting inconsistencies, converting all entries into numeric floats.

3. Target Variables
The processed dataset includes two supervised learning targets:
I) Regression Target:
PROCESSING_TIME_DAYS
→ Number of days from application to decision.
II) Classification Target:
CASE_STATUS
→ Predicts Certified vs. Denied outcomes.

📦 Files Included
File	Description
PERM_Disclosure_Data_FY2025_Q3_Final.csv	Raw dataset (excluded if too large)
visa_processor.py	Main ETL preprocessing script
Processed_Visa_Dataset.csv	Final cleaned dataset with 1,171 transformed records

# ▶️ How to Run
1. Place the Raw Input File
Ensure the raw CSV (PERM_Disclosure_Data_FY2025_Q3_Final.csv) is in the same directory as visa_processor.py.
2. Install Dependencies
pip install pandas numpy
3. Execute the Processing Script
python visa_processor.py

# Output:
The script generates:
Processed_Visa_Dataset.csv

🧰 Requirements

-> Python 3.x
-> Pandas
-> NumPy
