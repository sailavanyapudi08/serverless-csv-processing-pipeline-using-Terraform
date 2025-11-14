# AWS Serverless CSV Data Pipeline 🚀  
**Fully automated S3 → Lambda → Glue → S3 ETL pipeline built with Terraform**

This repository contains a complete, end-to-end **serverless data pipeline** on AWS, fully automated using **Infrastructure as Code (IaC) with Terraform**.  
It preprocesses and transforms CSV files uploaded to Amazon S3 and stores them in multiple stages for analytics and visualization.

---

## 📁 **Architecture Overview**

<img width="675" height="309" alt="Screenshot 2025-11-14 at 4 23 34 PM" src="https://github.com/user-attachments/assets/1555023b-f12e-4865-8f7e-7c3811f41799" />

---

## 🛠 **Services Used**

### **Amazon S3**
- Bucket for **raw** CSV uploads  
- Bucket for **processed** CSV files  
- Bucket for **final** ETL outputs (Parquet)  
- Event notifications triggering Lambda  

### **AWS Lambda**
- Python function for CSV preprocessing  
- Automatically triggered on S3 `.csv` uploads  
- Starts AWS Glue job after preprocessing  

### **AWS Glue**
- Glue Database  
- Glue ETL Job (PySpark)  
- Script stored automatically in S3  

### **IAM**
- Least-privilege roles for Lambda and Glue  
- Restricted S3 access  

### **Terraform**
Infrastructure provisioning:
- S3 buckets  
- IAM roles  
- Lambda packaging (no manual zip)  
- Glue job + script upload  
- S3 → Lambda event notification  

---

## 📂 **Repository Structure**
.
├── main.tf
├── variables.tf
├── outputs.tf
├── lambda/
│ └── handler.py
└── glue/
└── scripts/
└── glue_etl.py

---

## 🚀 **How It Works**

1. Upload a CSV file to the **raw S3 bucket**.
2. S3 triggers the **Lambda function**.
3. Lambda:
   - cleans/formats the CSV
   - writes output to the **processed bucket**
   - triggers the Glue ETL job
4. **Glue ETL job** reads processed CSV and writes final output as partitioned Parquet files into the **final bucket**.



