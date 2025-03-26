# Project 1🐾 Descriptive Analysis
# AWS Data Analytics Platform: Animal Control Inventory Register 2024
<h2>Project Description</h2>
This project focuses on designing and implementing an AWS-based Data Analytics Platform (DAP) for analyzing Animal Control Inventory data from the City of Vancouver Open Data Portal.
The objective is to clean, transform, and analyze animal impoundment trends using AWS S3, Glue, Glue DataBrew, and Athena.

<h3>Project Title</h3>
AWS Data Analytic Platform for The City of Vancouver- Animal Control Inventory 2024

<h3>Objective</h3>
✔ Identify the distribution of animal breeds across different age categories <br>✔ Determine the most recent impound date to support strategic decision-making for animal control operations.<br>  ✔ Leverage AWS Glue, Glue DataBrew, and Athena to process and extract insights. <br>  ✔ Ensure data security, cost optimization, and monitoring with AWS services.
<br> 

![image](https://github.com/user-attachments/assets/bce214b9-cadd-42c8-98af-06e8553e4116)

<h3>Dataset</h3> 
<table border="0">
  <thead>
    <tr>
      <th>Dataset Name</th>
      <th>Animal Control Inventory Register (2024)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Source</td>
      <td><a href="https://opendata.vancouver.ca/explore/dataset/animal-control-inventory-register/information/?sort=dateimpounded&refine.dateimpounded=2024">City of Vancouver Open Data Portal</a></td>
    </tr>
    <tr>
      <td>Size</td>
      <td>510 Rows, 18 Columns</td>
    </tr>
    <tr>
      <td>Format</td>
      <td>CSV</td>
    </tr>
    <tr>
      <td>Key Attributes</td>
      <td>AnimalID, DateImpounded, Breed, AgeCategory</td>
    </tr>
  </tbody>
</table>

<h2>Methodology</h2>
<h3>Descriptive Analysis</h3>
This dataset provides a comprehensive list of all the animals that have been reported to the City of Vancouver Animal Control Department and have been taken into their custody. It is one of the three interlinked datasets about animal reporting in Vancouver. 
 <br>
<i><b>Descriptive Metric</i></b> <br> 
• Count of animals (by breed)  <br>
• Maximum impound date (most recent impoundment date) <br>
<br>
<i><b>Analytical Questions </i> </b><br>
• What is the distribution of animal breeds across different age categories? <br>
• What is the most recent date of animal impoundments? <br>

<h3>Data Ingestion</h3>
• The dataset was extracted from the City of Vancouver Open Data Portal and stored in an AWS S3 bucket named <i>animal-control-inventory-raw</i>.

• Data was ingested as a CSV file and stored in a structured folder <i>(animal-control/)</i> in the raw zone, maintaining a daily ingestion rate.

![image](https://github.com/user-attachments/assets/7a3cdd3d-0989-48f4-8f69-4626d1c89f6f)

<h3>Data Profiling and Cleaning</h3>
Data profiling is a crucial step as it helps us to understand the structure and identify various possible issues with the dataset. Data cleaning is very important to clean and prepare the raw data for analysis. It handles all errors in the dataset such as missing values, duplicate values, outdated values, etc. All 17 issues are taken care of using AWS DataBrew cleaning techniques by creating a cleaning job named <i>‘animal-control-cln’</i>. 
<br> 
• Created a transformed S3 bucket <i>(animal-control-inventory-trf)</i> with two subfolders:

  1. user/ (CSV output for readability)

  2. system/ (Snappy files optimized for system processing)

• AWS Glue DataBrew was used for profiling and cleaning, with 24 recipe steps, including:

-Removing null values, duplicate records, and special characters

-Formatting timestamps and adjusting column names

-Filling missing values with "unidentified"

-Normalizing Breed names using regex

![image](https://github.com/user-attachments/assets/5a423d72-9c7b-4d80-bc5e-e45b019d71c1)

<h3>ETL Pipeline Design</h3>
The pipeline is designed to perform the ETL (Extract, Transform, and Load) process, which facilitates the efficient movement and transformation of data to its final destination. The output generated through this process is referred to as analytical data. 

• Built an ETL job <i>(animal-control-inventory)</i> using AWS Glue to transform the dataset:

-Dropped unnecessary columns

-Filtered based on age category (young, senior, puppy, adult)

• Aggregated key metrics:

✅Breed Count per age category

✅Max (latest) impound date

• Data stored in the curated S3 bucket <i>(animal-control-inventory-cur)</i>, partitioned by report_date and age_category.
![Screenshot 2025-03-24 205221](https://github.com/user-attachments/assets/13779c2a-4a04-4a41-b678-43eeab1bde57)
![Screenshot 2025-03-24 205245](https://github.com/user-attachments/assets/509cc96f-f29f-4c7f-9489-9520e42b73e2)
![Screenshot 2025-03-24 204424](https://github.com/user-attachments/assets/342587f2-6725-42d5-9115-2eae85f7c98c)

<h3>Data Analysis</h3>
The data analysis was performed using AWS Athena. After cleaning the dataset with AWS Glue, only necessary columns (date impounded, breed, and age category) were retained to reduce data scanning costs. 

SQL queries executed to answer the business questions are:
<br>
<i>SQL Code 1:</i>

     select max(dateimpounded) as Impound_Date, age category
     from 'animal_control_trfsystem'
     group by agecategory;

![image](https://github.com/user-attachments/assets/b843796d-f6f5-4f1f-8e36-d6d3d29824e5)


<i>SQL Code 2:</i>

     select count(breed) as Distinct_Breed, age category
     from 'animal_control_trfsystem'
     group by agecategory;
     
![image](https://github.com/user-attachments/assets/bc02fdcb-f3a9-46d9-8544-64d08138ef5c)

<h2> Tools & Technologies</h2>
<br>
<b>Amazon S3:</b>Used for storing datasets at various stages—Landing, Raw, and Curated. <br>
<b>AWS Glue:</b> Employed to build ETL pipelines for cleaning, transforming, and structuring the data. <br>
<b>AWS Glue DataBrew:</b> Simplified the data cleaning process with its visual interface. <br>
<b>Amazon Athena:</b> SQL queries were executed on the cleaned data stored in S3 for analysis. 
<br>

<h3>Deliverables</h3>
<h4>Project Documentation </h4> 
•<b>Project Overview:</b> Explanation of project objectives, methodologies, and AWS services used. <br>
•<b>Data Sources:</b> Information about the dataset used, including its source, format, and key attributes (AnimalID, DateImpounded, Breed, AgeCategory).<br>
•<b>Business Questions:</b> Description of the analytical questions to be addressed (breed distribution, recent impound date).<br>

<h4>Data Ingestion and Storage</h4>
S3 Buckets: <br>
• Raw Zone: The original dataset stored in a structured folder within S3 (animal-control-inventory-raw).<br>
• Transformed Zone: Cleaned data stored in a separate bucket (animal-control-inventory-trf) with subfolders for readable (CSV) and optimized (Snappy) formats.<br>
• Curated Zone: Final processed data stored in a curated bucket (animal-control-inventory-cur), partitioned by report date and age category.<br>

<h4>Data Profiling and Cleaning</h4>
• Profiling Report: Summary of the data profiling process using AWS Glue DataBrew, identifying 17 issues.<br>
• Cleaning Report: Documentation of the 24 cleaning steps performed using DataBrew, such as removing nulls, handling duplicates, formatting timestamps, and normalizing breed names.<br>

<h4>ETL Pipeline Design</h4>
• ETL Process Documentation: Description of the AWS Glue ETL job created to transform the dataset.<br>
• Pipeline Architecture: Diagram or description of the ETL flow, detailing the extract, transform, and load phases.<br>
• Aggregated Metrics: Report showing key metrics such as breed count by age category and the most recent impound date.<br>
• S3 Bucket Outputs: Structured outputs in the curated zone.<br>

<h4>Data Analysis</h4>
Athena Queries: SQL scripts used to answer the business questions:<br>
  • Query 1: Recent impound date by age category.<br>
  • Query 2: Breed distribution by age category.<br>



# Project 2 💊🚫 AWS Data Governance Framework
# UCW Substance Use Policy: Data Protection, Governance, and Monitoring System

<h2>Project Description</h2>
This project aimed to create a robust data protection, governance, and monitoring system using AWS services for UCW HR Substance Use policy. It was designed to handle sensitive data across multiple environments, enforce access controls, and ensure compliance with organizational security requirements. Through the use of AWS KMS, AWS Glue, AWS CloudWatch, and AWS CloudTrail, I implemented security protocols, established data governance processes, and monitored both resource usage and user activities effectively.

![Screenshot 2025-03-25 204800](https://github.com/user-attachments/assets/a713bcf0-12b3-4aeb-8b14-2604cf00d0ac)

<h2>Project Overview</h2>
The project was divided into three key phases: <br>
<b>•Data Protection:</b> Implementing encryption, access control policies, and security measures to safeguard data.<br>
<b>•Data Governance:</b> Establishing rules and automation to ensure data quality, compliance, and proper handling of sensitive information.<br>
<b>•Data Monitoring:</b> Continuous tracking of resource usage and user activities to detect anomalies and ensure accountability.<br>
Each phase leveraged a combination of AWS services, ensuring data encryption, fine-grained access control, detailed user activity tracking, and assurance of data quality across the system.

<h2>Project Title</h2>
UCW Substance Use Policy: Data Protection, Governance, and Monitoring System

<h2> Project Objective</h2>
The primary objective was to develop an AWS-based system that ensures:<br>
 • Data Protection: Strong encryption and access management for sensitive Substance Use data in University Canada West.<br>
 • Data Governance: Rigorous control of data quality, handling sensitive data like substance use incident data, and enforcing data management rules through automation.<br>
 • Data Monitoring: Continuous monitoring of resource usage, billing, and user activities to detect anomalies and ensure accountability.<br>

<h3>Dataset</h3>
The datasets used in this project included: <br> 
• CSV files containing worker list, supervisor list and substance test list stored in S3 buckets, representing raw and processed data. These datasets were used to test encryption, data governance, and data quality evaluation in the AWS Glue pipeline. <br>
• Log data generated by AWS CloudTrail to monitor user activities such as log-ins, resource modifications, and API calls.<br>
<br>
The S3 buckets were divided into zones: <br>
1. Raw Zone: Storage for unprocessed datasets of workers information. <br>
2. Transformed Zone: Storage for processed data. <br> 
3. Curated Zone: Storage for validated, cleaned data after processing. <br>
4. Backup Bucket: A secondary S3 bucket used for replication and versioning to ensure data redundancy and disaster recovery. <br>

<h2>Methodology</h2>
  <b>1. Data Protection</b> <br>
AWS IAM was used to define fine-grained access controls through roles, policies, and user groups. The root user had full administrative access, while lab roles were assigned to manage access to S3 and KMS resources. <br>
<i></i>IAM Role Configuration AWS S3 Buckets</i>

![Screenshot 2025-03-25 210850](https://github.com/user-attachments/assets/b990eac4-9186-4a00-bb3e-f4e710f3e4ac)

AWS KMS was implemented to generate symmetric encryption keys. These keys were used for encrypting and decrypting sensitive data stored in S3 buckets. Permissions for key management (create, delete, use) were carefully assigned using IAM roles. <br>

![image](https://github.com/user-attachments/assets/c3c088cd-e82a-4224-8c17-2e597edd45e9)

 <b>2. Data Governance</b> <br>
AWS Glue was used to build an ETL pipeline to detect sensitive data and enforce governance policies. The ETL pipeline started by loading raw data from the S3 bucket’s raw zone, then transforming and evaluating the data for sensitive information about substance use incidents in UCW. <br>

<i>AWS Glue ETL Data Quality Evaluation</i>

![Screenshot 2025-03-25 211720](https://github.com/user-attachments/assets/3956b58f-c1e6-4909-b984-bf7508e9464c)


Data quality checks were enforced by setting thresholds for rules like completeness, uniqueness and freshness. These rules helped validate the quality of data, ensuring it met the required standards before being stored in the trusted zone. <br>
Replication rules were applied to ensure that data from the primary S3 bucket was automatically replicated to a secondary backup bucket. Versioning was enabled to maintain multiple versions of files for disaster recovery. <br>

<i>S3 Replication Configuration Bucket Encryption Settings</i>

![image](https://github.com/user-attachments/assets/6c92b7cf-a6e2-4358-be3f-4ce9dcbc2d8b)
![image](https://github.com/user-attachments/assets/fb04ee30-ae49-4229-a3bd-7f515c68c7ed)
![image](https://github.com/user-attachments/assets/4a639f80-7467-475a-9ef0-e432f8e55369)
![image](https://github.com/user-attachments/assets/fc3ecf5c-7ec9-4428-873e-b3742f7e1250)
![image](https://github.com/user-attachments/assets/9b39c0cc-a819-4eb9-bbc9-0744f8e6dfc1)
![image](https://github.com/user-attachments/assets/feee0e19-5fac-407e-a4ef-671399235c91)
![image](https://github.com/user-attachments/assets/1c31ab2f-6f88-4c83-8b76-3e8443c8f4d4)

  <b>3. Data Monitoring</b> <br>
AWS CloudWatch was used to set up a monitoring dashboard. This dashboard displayed key metrics related to S3 usage (e.g., number of objects, storage capacity) and billing metrics to track costs.
<i>Custom CloudWatch Dashboard for Monitoring</i>

![image](https://github.com/user-attachments/assets/2373a08a-ebae-40d2-9354-8d2d0732142f)

CloudWatch Alarms were created to send email notifications if certain thresholds were exceeded. Alarms were configured to monitor resource utilization and trigger appropriate actions if necessary.

AWS CloudTrail was used to track user activities, providing a detailed log of events such as API calls, user log-ins, and resource modifications. Logs were stored securely in an S3 bucket, with additional encryption applied to ensure data protection. CloudTrail was essential for maintaining accountability and transparency in the AWS environment.

<i>CloudTrail Configuration</i>
![image](https://github.com/user-attachments/assets/8dafa169-548b-481c-88ed-749852ea1f9d)

<h3>Tools and Technologies</h3>
AWS KMS: Utilized to generate and manage encryption keys for securing sensitive data. <br>
AWS S3: Primary storage for raw, processed, and log datasets. S3 was used in conjunction with replication and versioning for data protection and disaster recovery.<br>
AWS Glue: Built an ETL pipeline for detecting sensitive data, managing data governance policies, and ensuring data quality. <br>
AWS CloudWatch: Set up dashboards and alarms to monitor resource usage and billing metrics. <br>
AWS CloudTrail: Recorded user activity and API calls, providing logs for security and compliance. <br> 

<h3>Deliverables</h3>
<b>1. Data Protection System:</b> <br>
•Created IAM roles and policies for secure access control.<br>
•Implemented encryption with KMS keys for sensitive data in S3.<br>
•Applied replication and versioning in S3 to ensure data redundancy and disaster recovery.<br>
  
<b>2. Data Governance Pipeline:</b> <br>
•Designed an ETL pipeline in AWS Glue to detect sensitive data and evaluate data quality.<br>
•Set up automated workflows for data processing, including checks for completeness and uniqueness.<br>
•Enabled replication rules and versioning in S3 for backups and data recovery.<br>

<b>3. Data Monitoring System:</b> <br>
•Built a CloudWatch dashboard to monitor S3 usage, billing metrics, and other key performance indicators.
•Configured CloudWatch alarms to notify when certain thresholds (e.g., bucket size bytes) were reached.
•Set up CloudTrail to record user activity. 
•Stored logs in an encrypted S3 bucket with versioning enabled to maintain secure records of user actions.
