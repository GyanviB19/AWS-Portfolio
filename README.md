# 🐾 AWS Data Analytics Platform: Animal Control Inventory Register 2024
<h2>Project Description</h2>
This project focuses on designing and implementing an AWS-based Data Analytics Platform (DAP) for analyzing Animal Control Inventory data from the City of Vancouver Open Data Portal.
The objective is to clean, transform, and analyze animal impoundment trends using AWS S3, Glue, Glue DataBrew, Athena, and CloudWatch.

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
