# 🐾 AWS Data Analytics Platform: Animal Control Inventory Register 2024
<h2>Project Description</h2>
This project focuses on designing and implementing an AWS-based Data Analytics Platform (DAP) for analyzing Animal Control Inventory data from the City of Vancouver Open Data Portal.
The objective is to clean, transform, and analyze animal impoundment trends using AWS S3, Glue, Glue DataBrew, Athena, and CloudWatch.

<h3>Project Title</h3>
AWS Data Analytic Platform for The City of Vancouver- Animal Control Inventory 2024

<h3>Objective</h3>
✔ Analyze the distribution of animal breeds across different age categories. <br>✔ Identify the most recent impoundment date for each age category.<br>  ✔ Leverage AWS Glue, Glue DataBrew, and Athena to process and extract insights. <br>  ✔ Ensure data security, cost optimization, and monitoring with AWS services.

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
<i>Descriptive Metric</i> <br> 
• Count of animals (by breed)  <br>
• Maximum impound date (most recent impoundment date) <br>
<br>
<i>Analytical Questions </i> <br>
• What is the distribution of animal breeds across different age categories? <br>
• What is the most recent date of animal impoundments? <br>

