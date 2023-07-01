# Stock Prediction on Deutsche Börse using AWS

## 1. INTRODUCTION:
The Stock Prediction on Deutsche Börse using AWS project utilizes the Deutsche Börse Public Eurex Data Set, which consists of real-time trade data aggregated at one-minute intervals from the Eurex trading systems. The dataset provides valuable information such as the initial, lowest, highest, and final prices and the trading volume for every minute of the trading day. This project aims to develop a predictive model for stock prices using AWS services like EMR, Sagemaker, Glue, and QuickSight.


## 2. DATASET DESCRIPTION:
The dataset is sourced from the AWS Registry and contains 45.5 million data points with 3,230,161 rows and 20 columns. It consists of real-time trade data aggregated at one-minute intervals from the Eurex trading systems, providing information on the initial price, lowest price, highest price, final price, volume, and tradable security for each minute of the trading day. The data follows the Open/High/Low/Close (OHLC) format and includes the number of trades and traded contracts. The dataset has been cleaned, resulting in 3,230,161 rows and 20 columns. For the purpose of this project, the EUR currency data within the date range [date_from = "2021-01-01" date_to = "2022-01-01"] has been selected for prediction and modeling. The EUR data consists of 87,409 data points, and the goal is to predict the start price of EUR entries in the Deutsche Börse data based on the best-fitting ARCH and GARCH prediction models.

## 3. PROPOSED ARCHITECTURE: 

The project's architecture leverages various AWS technologies to process and analyze the dataset effectively. The following technologies are utilized:

1. AWS S3: Used for storing the dataset and intermediate files.
2. AWS Glue: Employed for data extraction, wrangling, and preprocessing tasks, transforming the dataset into a queryable format.
3. AWS EMR: Utilized a PySpark instance to propose and develop the predictive model. The large dataset is trained using PySpark on the EMR cluster.
4. AWS Sagemaker: Employed for merging files, conducting exploratory data analysis, and performing time series analysis.
5. AWS QuickSight: Connected to the Glue database to visualize and explore the data, creating an informative data analytics dashboard.


![architecture](/pic.png)

## 4. Exploratory Data Analysis (EDA): Data Extraction, Data Wrangling, Preprocessing:

The EDA phase involved several preprocessing techniques to prepare the dataset for analysis. The techniques employed include:

- Removing duplicate data points
- Dropping irrelevant columns
- Converting categorical features into numerical ones using one-hot encoding
- Converting numeric data fields (Strike Price, Start Price, Max Price, Min Price, and End Price) from strings to floats for mathematical calculations
- Filtering the dataset to a specific date range
- Applying label encoding to normalize labels and transform them into non-numerical labels
- Performing correlation analysis between attributes and calculating correlation coefficients to measure the relationship strength between variables

The results of the correlation analysis were visualized using a heatmap, bar graphs, and histograms to explore the relationships between different attributes in the dataset. Notably, a correlation coefficient of 0.25 was observed between Start Price and Contract Generation Number, while a correlation coefficient of 0.50 was found between Start Price and Contract Generation Number.


## 5. AWS Glue Job Setup:

To handle the large amount of data in the s3 Deutsche Börse bucket, AWS Glue Crawlers and Jobs were created to clean and transform the data for querying purposes. The following steps were taken:

- A crawler was created to send the data from the s3 bucket to a Glue database for easy querying.
- IAM roles were configured to allow read/write access to the s3 bucket.
- A Glue ETL job was created to transform the CSV files to the more efficient Parquet format, addressing issues with column formatting and improving query performance.
- The transformed Parquet files were written to a new folder for storage.
- Another crawler was created to load the transformed Parquet files into a new table, which served as the basis for creating visualizations using AWS QuickSight.

With these steps, the data was prepared and transformed for further analysis and visualization using QuickSight.

## 6. Conclusion:

In conclusion, the Stock Prediction on Deutsche Börse using AWS project utilizes the Deutsche Börse Public Eurex Data Set to develop a predictive model for stock prices. Through the utilization of various AWS technologies such as S3, Glue, EMR, Sagemaker, and QuickSight, the project aims to extract, preprocess, analyze, and visualize the dataset effectively.

The dataset consists of 45.5 million data points with 20 columns, providing valuable real-time trade data from the Eurex trading systems. The data undergoes exploratory data analysis (EDA) where preprocessing techniques are applied, including duplicate removal, column dropping, and conversion of categorical features into numerical ones. Correlation analysis is performed to understand the relationship between different attributes.

AWS Glue is employed for data extraction, wrangling, and preprocessing tasks, while AWS EMR utilizes PySpark to propose and develop the predictive model. AWS Sagemaker is used for exploratory data analysis and time series analysis. The transformed data is stored in the more efficient Parquet format, resulting in improved query performance and reduced storage space. Finally, AWS QuickSight is connected to the Glue database to create an informative data analytics dashboard for visualization and exploration.

Through the project's architecture and utilization of AWS technologies, valuable insights can be gained from the dataset, leading to the development of a predictive model for stock prices on Deutsche Börse. The project demonstrates the power of AWS services in handling large datasets, performing data analysis, and creating visualizations for informed decision-making in the financial domain.
