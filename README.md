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


# Milestone 2: Exploratory Data Analysis (EDA)

🎯 Objective

The objective of this milestone is to uncover meaningful patterns and trends in the processed visa dataset to inform feature selection for the AI model developed in Milestone 3.

Python visualization libraries (Matplotlib and Seaborn) were used to analyze distributions, correlations, and temporal patterns.

🔍 Key Insights & Trends
1. Processing Time Analysis

Observation

Processing times are not uniformly distributed.

A clear average wait-time cluster exists.

Significant outliers indicate cases with extremely long processing durations.

Model Implication

The regression model must be robust to outliers.

Metrics such as Median Absolute Error (MAE) may be more appropriate than relying solely on RMSE.

2. Geographic Hotspots

Observation

A small number of states (e.g., California, Texas, New York) account for the majority of visa applications.

Trend

Processing times and denial rates vary slightly by state.

Feature Impact

EMPLOYER_STATE is identified as a high-value predictive feature.

3. Education & Skill Correlation

Observation

Certification outcomes vary by education level.

Applicants with Master’s or Doctorate degrees show different approval patterns compared to High School or Bachelor’s degree holders.

Decision

MINIMUM_EDUCATION will be retained as a critical categorical feature in the model.

4. Seasonality (Time Series Analysis)

Observation

Average processing times fluctuate across submission months.

Certain months exhibit noticeable backlogs.

Feature Engineering Confirmation

The cyclic features derived from SUBMISSION_MONTH (created in Milestone 1) are validated for modeling.

🧪 Artifacts Generated

The visa_eda.py script automatically generates the following visualizations in the output_charts/ directory:

Processing Time Distribution
Histogram of visa processing wait times

State Status Distribution
Bar chart showing Certified vs. Denied cases by top states

Education Impact
Stacked bar chart of certification probabilities by education level

Seasonal Trends
Line graph of average processing time across submission months

Wage vs. Processing Time
Scatter plot analyzing correlation between offered wage and processing speed

▶️ How to Run the Analysis
1. Ensure Dataset Availability

Make sure the following file is present in the project directory:

Processed_Visa_Dataset.csv

2. Install Required Libraries
pip install pandas matplotlib seaborn

3. Run the EDA Script
python visa_eda.py


All generated charts will be saved to the output_charts/ directory.

📌 Next Steps

Use identified high-impact features in Milestone 3 (Model Development)

Apply outlier-resistant modeling techniques

Incorporate geographic and seasonal patterns into predictive features
