**Data Warehouse Exploration & Hadoop Integration Report**

**Objective**
This project focuses on exploring publicly available datasets from different data-
warehouse repositories and understanding how to interact with, clean, and analyze raw
data. The exercise also involves experimenting with Hadoop to process datasets efficiently.

**Technologies Used**
•	Apache Hadoop: Used for distributed storage (though primarily interacted with locally in this setup) and for executing MapReduce jobs (via MRJob).
•	Apache Spark: Employed for interactive data analysis and running SQL queries on the dataset, offering more flexibility and speed compared to traditional MapReduce for iterative analysis.
•	Python: Used for scripting, orchestrating the data processing steps, and writing the MRJob script.
•	MRJob: A Python library for writing MapReduce jobs that can run on Hadoop.
•	PySpark: The Python API for Apache Spark.

**Data Source**
Humanitarian Data Exchange (HDX)
Dataset: WFPVAM Food Prices CSV
URL: https://data.humdata.org/dataset/4fdcd4dc-5c2f-43af-a1e4-
93c9b6539a27/resource/12d7c8e3-eff9-4db0-93b7-
726825c4fe9a/download/wfpvam_foodprices.csv
Description: A global dataset capturing food prices across regions

**Step-by-Step Approach** 

The project involved the following key steps:

**1. Initial Data Exploration ("Getting a Feel")**

- Preview the raw file using Excel or a text editor.
- Check structure: Inspect column names, data types, and identify missing or malformed
data.
- Sample rows to understand the kind of information captured.
- Questions to ask:
        * Are there date columns? Are they in the correct format?
        * Are there categorical vs numerical values?
        * Are there empty or corrupted rows?

**2. Loading Dataset into Hadoop**

_- Preprocessing:_
1.	Environment Setup: Downloading and setting up Hadoop and PySpark.
2.	Data Acquisition: Downloading the `wfpvam_foodprices.csv` dataset.
3.	Data Cleaning: Convert the dataset to clean .csv (did not required).
4.	Data Loading: Loading the dataset into a suitable environment for processing. This involved using Hadoop file system commands (interacting with the local filesystem in this setup) and then loading the            data into Spark DataFrames.
5.	Data Analysis (MRJob): Implementing a MapReduce job using MRJob to calculate the average price of commodities per year.
6.	Data Analysis (PySpark):
   
       •	Loading the data into a Spark DataFrame.
       •	Performing exploratory data analysis (e.g., showing schema, sample data).
       •	Running Spark SQL queries to answer specific analytical questions, such as counting records, calculating average prices by country and commodity, and analyzing price trends for specific items in                  particular regions.
 
 **Findings & Observations**
 
Based on the execution of the data analysis steps, several key findings and observations were made regarding the data, the technologies used, and the insights gained:

•	Data Complexity: As is common with real-world datasets, the WFP food prices data exhibited typical complexities. We observed:
•	Inconsistent Values: Data might contain variations in spelling, capitalization, or formatting for country and commodity names.
•	Missing Fields: Some records may have missing price information or other relevant details.
•	Preprocessing Requirements: Handling inconsistencies and missing values would be necessary for more robust analysis. The `MRJob` script included a basic `try-except` block to skip malformed rows, demonstrating the need for data cleaning considerations.

**Importance of Schema:** 

Correctly understanding and defining the data schema was crucial, especially when loading data into Spark. While Spark's `inferSchema` option is helpful, manually specifying or verifying schema can prevent issues, particularly for ensuring numeric columns are treated correctly for calculations. For Hadoop/Hive, defining the schema correctly is fundamental for data parsing and querying.

**Performance:** 

Hadoop and Spark demonstrated their capability in handling this relatively large CSV dataset.

•	Hadoop's file system commands were efficient for basic file operations.

•	Spark's in-memory processing and optimized execution engine provided fast results for interactive queries compared to traditional disk-based MapReduce, highlighting its suitability for iterative data exploration and analysis on big data.

**Insight Discovery:** 

The analysis yielded several insights into food price dynamics:

•	Price Fluctuations Vary Significantly: Running queries to find average prices by country and commodity confirmed that price levels and their year-to-year variations are highly dependent on the specific region and the type of commodity.

•	Regional and Commodity-Specific Trends: Analyzing the price trends for a specific item like "Rice - Retail" in a particular region ("Bassas da India" in this case, based on the data's representation) revealed specific local trends that might differ from global or regional averages, indicating the influence of local logistical factors, market conditions, or economic differences.

•	Market Disparities: The observation that some markets consistently have higher prices suggests underlying logistical challenges, supply chain inefficiencies, local demand/supply imbalances, or other economic factors influencing pricing in those areas. Further analysis could delve into specific regions or commodities to understand these disparities better.

**Challenges Encountered**

•	Hadoop Configuration: Setting up and configuring Hadoop, even for a single-node local mode, requires careful attention to environment variables and configuration files.

•	Data Pathing: Correctly specifying file paths for Spark to read data from either the local filesystem (`file://`) or HDFS (`hdfs://`) was critical and a source of errors if not done precisely, as seen in the `Incomplete HDFS URI` error.

•	Data Quality: The need to handle potential errors (like `ValueError` or `IndexError` in the MRJob script) due to inconsistent data formatting underscored the importance of data cleaning in a real-world scenario.

**Conclusion**

This project successfully demonstrated the use of Hadoop and Spark for analyzing a real-world food price dataset. It highlighted the power of these big data tools for handling large volumes of data and extracting meaningful insights. The process also reinforced the practical challenges associated with real-world data quality and the importance of correct configuration and data path management in a distributed computing environment. Further work could involve more sophisticated data cleaning, feature engineering, and applying machine learning techniques using Spark's MLlib to build predictiv
