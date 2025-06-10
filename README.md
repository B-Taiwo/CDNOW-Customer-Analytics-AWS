# CDNOW Customer Analytics Pipeline on AWS

## An End-to-End AWS Project

### Project Overview
This repository contains an end-to-end data science project demonstrating a customer analytics pipeline built on Amazon Web Services (AWS) using the classic CDNOW transactional dataset.

The pipeline covers:
-   **Data Ingestion & Storage:** Utilizing AWS S3 as a scalable data lake for raw and processed data.
-   **ETL & Feature Engineering:** Implementing data cleaning, transformation, and advanced feature derivation (RFM, tenure, etc.) using AWS Glue.
-   **Customer Segmentation:** Applying K-Means clustering to identify distinct customer segments.
-   **Customer Churn Prediction:** Developing a supervised machine learning model to predict customer churn based on inactivity.

### Key Sections of the Notebook (`cdnow.ipynb`)
1.  **AWS Configuration & Raw Data Ingestion:** Setting up AWS credentials and loading raw data from S3.
2.  **Initial Data Cleaning & Type Conversion:** Preprocessing raw data for consistency.
3.  **RFM Feature Engineering:** Calculating Recency, Frequency, and Monetary metrics.
4.  **Deriving Additional Customer Features:** Calculating customer tenure, average time between purchases, etc.
5.  **Storing Processed Data to S3:** Saving the enriched data in Parquet format.
6.  **Customer Segmentation (Clustering):** Applying K-Means and interpreting customer segments.
7.  **Customer Churn Prediction:** Defining churn, training a Logistic Regression model, and evaluating performance.

### Technologies Used
* **AWS:** S3, Glue (Crawlers, ETL Jobs), Lambda (conceptual orchestration)
* **Python Libraries:** Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Boto3, s3fs, PyArrow

### Getting Started
1.  Clone this repository.
2.  Ensure you have Python 3.x and the required libraries installed (`pip install boto3 pyarrow s3fs scikit-learn matplotlib seaborn`).
3.  **AWS Setup:** You will need an AWS account. Set up your S3 buckets (raw and processed), and configure AWS Glue Crawlers/Jobs as outlined in the notebook.
4.  **Credentials:** **IMPORTANT:** Never expose your AWS credentials in public code. Set them as environment variables (e.g., `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`) in your environment.
5.  Run the `cdnow.ipynb` notebook.

### Findings & Insights
This project yielded valuable insights into customer behavior within the CDNOW dataset:

1. Customer Segmentation: Through K-Means clustering (with an optimal k=4), four distinct customer segments were identified:

  * "Churned / Lost Customers": Highly inactive, often one-time buyers with very old last purchases and low overall spend.
  * "At-Risk / Lapsing Customers": Showing signs of disengagement with moderately old last purchases and inconsistent buying patterns.
  * "High-Value Loyal / Power Users": The most valuable segment, characterized by very recent, highly frequent, and extremely high-spending behavior.
  * "Engaged / Active Customers": A larger, stable base of active customers with recent, frequent, and substantial spending. These segments provide a clear basis for targeted marketing and customer relationship management strategies.

2. Customer Churn Prediction: A Logistic Regression model was developed to predict churn (defined as Recency > 180 days). The model achieved outstanding performance (AUC-ROC: 0.999, Precision/Recall/F1-score of 0.99 for the churned class), demonstrating its high accuracy in identifying customers meeting this inactivity criterion.

  * Key Churn Drivers (Logistic Regression Feature Importance):
    *Decreasing Churn Likelihood: Higher Frequency, AvgTimeBetweenPurchases (for established buyers), TotalQuantityPurchased, and Monetary value were strongly associated with a lower probability of churn.
    *Increasing Churn Likelihood: Higher Recency (less recent purchase) was, as expected, the most significant positive indicator of churn. CustomerTenure also had a positive correlation, suggesting that older customers who hadn't recently purchased were more likely to be classified as churned within this cohort.


### Contact
Taiwo Balogun - [https://www.linkedin.com/in/abdulquadribalogun] 
