## Improved Detection of Fraud Cases for E-commerce and Bank Transactions

### Project Overview

This project aims to develop accurate and robust fraud detection models for both e-commerce and bank credit transactions. As a data scientist at Adey Innovations Inc., the goal is to enhance transaction security by leveraging advanced machine learning models, detailed data analysis, geolocation analysis, and transaction pattern recognition. A key focus is on balancing the trade-off between security (minimizing false negatives) and user experience (minimizing false positives).


### Progress:

This repository reflects the completion of **Task 1: Data Analysis and Preprocessing**.

#### 1. Data Cleaning and Preprocessing Steps:

* **Dataset Loading and Initial Inspection:** All three datasets (`Fraud_Data.csv`, `IpAddress_to_Country.csv`, `creditcard.csv`) were loaded and inspected for shape, data types, and missing values.
* **Data Type Conversion:**
    * For `Fraud_Data.csv`, `signup_time` and `purchase_time` columns were successfully converted to `datetime` objects.
    * `source`, `browser`, and `sex` columns in `Fraud_Data.csv` were converted to `category` dtype for efficiency.
    * `lower_bound_ip_address` in `IpAddress_to_Country.csv` was converted to `int64` for consistency.
* **Duplicate Handling:** Duplicate rows were checked and removed from all datasets. Notably, 1081 duplicate rows were removed from `creditcard.csv`.
* **IP Address to Country Mapping:** The `Fraud_Data.csv` was enriched with geographical information by mapping `ip_address` to `country` using `IpAddress_to_Country.csv`. Approximately 14.5% of transactions resulted in an 'Unknown' country.

#### 2. Key Insights and Visualizations from Exploratory Data Analysis (EDA):

Detailed EDA was performed to understand data distributions and patterns related to fraud.

* **Class Imbalance:**
    * `Fraud_Data.csv` exhibits a significant class imbalance with ~9.36% fraudulent transactions.
    * `creditcard.csv` shows an extreme class imbalance with ~0.17% fraudulent transactions. This severe imbalance is a critical consideration for model selection and evaluation.
* **Numerical Features (`Fraud_Data.csv`):**
    * Transactions with very short `time_since_signup` (immediate purchases) showed a higher incidence of fraud.
    * High `device_transaction_count` and `ip_transaction_count` were strongly associated with fraudulent activities, indicating potential bot or compromised account usage.
    * `purchase_value` and `age` showed less distinct patterns between fraudulent and non-fraudulent transactions.
    * Temporal patterns (hour of day, day of week) showed subtle variations in fraud frequency.
* **Categorical Features (`Fraud_Data.csv`):**
    * The 'Unknown' country category, along with 'China' and 'Japan', exhibited notably higher fraud rates.
    * The 'Opera' browser also showed an elevated fraud rate.
    * 'Direct' and 'SEO' sources had slightly higher fraud rates compared to 'Ads'.
    * 'Sex' did not appear to be a strong predictor of fraud.
* **Credit Card Features (`creditcard.csv`):**
    * Fraudulent transactions generally involved smaller `Amount` values compared to legitimate ones.
    * Several PCA-transformed features (`V17`, `V14`, `V12`, `V10`, `V11`, `V4`, `V2`) showed strong positive or negative correlations with the `Class` variable, indicating their high discriminative power despite their anonymized nature.

#### 3. Proposed Strategy for Handling Class Imbalance:

Given the significant to extreme class imbalance in both datasets, the primary strategy for handling this will involve:
* **Sampling Techniques:** Applying techniques such as **SMOTE (Synthetic Minority Over-sampling Technique)** on the training data *only* to generate synthetic samples for the minority class. This helps to provide the models with a more balanced view of the fraudulent class without losing information from the majority class. Random Undersampling will also be considered if SMOTE proves insufficient or computationally expensive.
* **Evaluation Metrics:** Focusing on metrics appropriate for imbalanced data, specifically **AUC-PR (Area Under the Precision-Recall Curve)** and **F1-Score**. These metrics provide a more reliable assessment of model performance on the minority class compared to overall accuracy. A detailed **Confusion Matrix** analysis will also be crucial to understand the trade-off between False Positives and False Negatives.

### Repository Structure:

* `notebooks/`: Contains Jupyter notebooks for data analysis, preprocessing, and EDA.
    * `data_loading_eda.ipynb`: The main notebook detailing Task 1.
* `data/`: Contains the raw datasets.
* `README.md`: This file, providing an overview of the project and progress.

### How to Set Up and Run the Code:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Ybtry/Adey_Innovations_Inc.git](https://github.com/Ybtry/Adey_Innovations_Inc.git)
    cd Adey_Innovations_Inc
    ```
2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    # On Windows:
    .\venv\Scripts\activate
    # On macOS/Linux:
    source venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    (Note: The `requirements.txt` file will be added in a later commit, or you can generate it now using `pip freeze > requirements.txt` after installing necessary libraries manually).
4.  **Place Data:** Ensure `Fraud_Data.csv`, `IpAddress_to_Country.csv`, and `creditcard.csv` are placed in the `data/` subdirectory. Adjust paths in the notebook if your local data directory structure differs.
5.  **Run the Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
    Open `notebooks/data_loading_eda.ipynb` in your browser and run all cells sequentially to reproduce the analysis.

