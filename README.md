# Stock Prediction on Deutsche Börse using AWS

## 1. INTRODUCTION:
The Stock Prediction on Deutsche Börse using AWS project utilizes the Deutsche Börse Public Eurex Data Set, which consists of real-time trade data aggregated at one-minute intervals from the Eurex trading systems. The dataset provides valuable information such as the initial, lowest, highest, and final prices, as well as the trading volume for every minute of the trading day. This project aims to develop a predictive model for stock prices using AWS services like EMR, Sagemaker, Glue, and QuickSight.


## 2. DATASET DESCRIPTION:
The dataset is from the AWS Registry. It contains 45.5 million data points with 3230161 rows and 20 columns. The Deutsche Börse Public Data Set consists of real-time trade data aggregated at one-minute intervals from the Eurex trading systems. It provides the initial price, lowest price, highest price, final price, volume for every minute of the trading day, and tradable
security. The contents of the Deutsche Börse Public Dataset, from Eurex trading engines, are defined in the data dictionary. The EUREX dataset contains trade data relating to derivative security trades. Each row represents one minute of trade activity for each security, following the Open/High/Low/Close (OHLC) format, with the number of trades and traded contracts. After cleaning data, the number of columns and rows (3230161, 20), respectively. While using the Linear regression model we have chosen EUR currency data for prediction and modeling which is in data range[ date_from = "2021-01-01" date_to = "2022-01-01" ]. The EUR data consists of 87409 Data Points with which we are predicting the Start Price of EUR entries of the Deutsche Borse data; based on the current values of Start Price, the future values are predicted based on the best fitting ARCH and GARCH prediction models.

## 3. PROPOSED ARCHITECTURE: 

The project's architecture involves leveraging various AWS technologies to process and analyze the dataset effectively. The architecture diagram below illustrates the flow of data and services used:

![architecture](/pic.png)

## 4. AWS Technologies:

 1. AWS S3 Used for storing the dataset and intermediate files.
 2. AWS Glue: Employed for data extraction, data wrangling, and preprocessing tasks, transforming the dataset into a queryable format.
 3. AWS EMR: Utilized with a PySpark instance to propose and develop the predictive model. The large dataset is trained using PySpark on the EMR cluster.
 4. AWS Sagemaker: Employed for merging files, conducting exploratory data analysis, and performing time series analysis.
 5. AWS QuickSight: Connected to the Glue database to visualize and explore the data, creating an informative data analytics dashboard.

## 5. Exploratory Data Analysis (EDA): Data Extraction, Data Wrangling, Preprocessing:

The EDA phase involved several preprocessing techniques to prepare the dataset for analysis. These techniques include removing duplicate data points, dropping irrelevant columns, and converting categorical features into numerical ones using one-hot encoding. Numeric data fields, such as Strike Price, Start Price, Max Price, Min Price, and End Price, were converted from strings to floats for mathematical calculations. The dataset was filtered to a date format using the filter function, and the remaining values were stored in a data frame. Label encoding was applied to normalize labels and transform them into non-numerical labels using the fit_transform() function. Correlation analysis was performed between attributes, and correlation coefficients were calculated to measure the relationship strength between variables. The correlation results were visualized using a heatmap, where a correlation coefficient of 1.0 represents the highest correlation, and -1 indicates the least correlated value. Furthermore, bar graphs were plotted to examine the highest correlation values, such as Put or Call and Contract Generation Number, and a histogram was generated to visualize the relationship between Average and Strike Price for each Start Price. Notably, a correlation of 0.25 was observed between Start Price and Contract Generation Number, while a correlation of 0.50 was found between Start Price and Contract Generation Number.


## 6. AWS Glue Job Setup:

To handle the large amount of data in the s3 Deutsche Borse bucket, AWS Glue Crawlers and Jobs were created to clean and transform the data for querying purposes. The initial crawler was designed to send the data from the s3 bucket to a Glue database for easy querying. IAM roles were configured to allow read/write access to the s3 bucket. However, issues with column formatting and lengthy query execution time were observed when examining the resulting table. To address these issues, a Glue ETL job was created to transform the CSV files to the more efficient Parquet format. This job included configurations to map the columns to their appropriate names, improving query performance and reducing storage space compared to CSV files. The transformed Parquet files were written to a new folder for storage. Finally, another crawler was created to load the transformed Parquet files into a new table, which served as the basis for creating visualizations using AWS QuickSight.
