# Stock Prediction on Deutsche Börse using AWS

## 1. INTRODUCTION
The Deutsche Börse Public Eurex Data Set consists of real-time trade data aggregated at one-minute intervals from the Eurex trading systems. It provides the initial, lowest, highest, final price, and volume for every minute of the trading day and tradable security. The contents of the Deutsche Börse Public Dataset, from the Eurex trading engines, are defined in the data dictionary. This Eurex dataset contains trade data relating to derivative security trades. Each row represents one minute of trade activity for each security, following the Open/High/Low/Close (OHLC) format, with the number of trades and traded contracts. The EMR Cluster has been used with a PySpark instance. PySpark on the EMR cluster has been used to propose and develop a model, and this model has been trained on the large dataset. AWS Sagemaker has been used to merge files and carry out exploratory data analysis; it has also been used to perform time series analysis of data. AWS Glue has been used to store the data into the database to connect to AWS QuickSight, this is used to visualize and explore the data, and create an informative data analytics dashboard.


## 2. DATASET DESCRIPTION:
The dataset is from the AWS Registry. It contains 45.5 million data points with 3230161 rows and 20 columns. The Deutsche Börse Public Data Set consists of real-time trade data aggregated at one-minute intervals from the Eurex trading systems. It provides the initial price, lowest price, highest price, final price, volume for every minute of the trading day, and tradable
security. The contents of the Deutsche Börse Public Dataset, from Eurex trading engines, are defined in the data dictionary. The EUREX dataset contains trade data relating to derivative security trades. Each row represents one minute of trade activity for each security, following the Open/High/Low/Close (OHLC) format, with the number of trades and traded contracts. After cleaning data, the number of columns and rows (3230161, 20), respectively. While using the Linear regression model we have chosen EUR currency data for prediction and modeling which is in data range[ date_from = "2021-01-01" date_to = "2022-01-01" ]. The EUR data consists of 87409 Data Points with which we are predicting the Start Price of EUR entries of the Deutsche Borse data; based on the current values of Start Price, the future values are predicted based on the best fitting ARCH and GARCH prediction models.

## 3. PROPOSED ARCHITECTURE: 

![architecture](/images/pic.png)

## 4. AWS Technologies:
 1.  AWS S3 
 2.  AWS Glue
 3.  AWS EMR
 4. AWS Sagemaker
 5. AWS QuickSight

## 5. EDA: Data Extraction, Data Wrangling, Preprocessing

The data set used from the S3 bucket of Deutsche Borse contains features which are both Categorical and Numeric in nature. Performed various preprocessing techniques like removing duplicate data points, dropping columns that are not useful for analyzing, converting categorical into numerical with one hot encoding and so on. The dataset has all the fields as a string when read from the s3 bucket and we converted it to respective datatypes , ie. took Numerical data such as Strike Price, Start Price, Max Price, Min Price, and End Price and converted them from strings to float to perform mathematical calculations. Filtered the data frame to date format using the filter function. The remaining values were put in a data frame. Label Encoder is generally used to normalize labels and transform them to non-numerical labels; we used fit_transform() to fit label encoder and return encoded labels. Followed by performing Correlation between the attributes and calculating Correlation coefficients used to measure the strength of the relationship between two variables. Used Heatmap to visualize the correlation between in, 1.0 being the highest correlation and -1 being the least correlated value. Plotted Bar Graph between the highest correlation values (Put or Call and Contract Generation Number) & plotted histogram between Average and StrikePrice of each StartPrice. The correlation between Start Price and Contract Generation Number is 0.25. A correlation 0.50 correlation was found between Start Price and Contract Generation Number.


## 6.  GLUE JOB SETUP:
In order to be able to deal with a large amount of data in the s3 Deutsche Borse bucket, AWS Glue Crawlers and Jobs were created to send all the files from the s3 bucket to a Glue database ultimately cleaning the code so data so that it could be queried. The first crawler that was created was made to send the data that was pulled from the s3 bucket and send it to a database so that the data could be easily queried when needed. In order to fully set up this crawler, it was essential to configure IAM roles to read from/write to the s3 bucket. The crawler contained the locations of the CSV files, glue database name, and a table that would map all the values. When observing the newly created table, it was evident that there was a problem with formatting the columns, and the query took an extended amount of time. In order to rectify this, a Glue ETL job was created to transform the CSV files to parquet. Besides the advantage that parquet files provide a better query performance, they also take up much less storage than CSV files. The
 
Glue ETL job contained configurations to map the columns to their names instead of labeled as col0, col1, etc. These new parquet files were written into a new folder where all the parquet files were stored. Finally, the last crawler was created to send the newly created/formatted parquet files into a new table. This data was then used for creating the visualizations using AWS Quicksight, shown later in this report.
