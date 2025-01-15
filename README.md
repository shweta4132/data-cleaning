Screentime Data Analysis and Cleaning:

This project focuses on cleaning and processing a dataset related to screentime usage. The goal is to handle missing values, detect and remove outliers, manage duplicates, create new features, and apply scaling and normalization techniques to prepare the data for further analysis.

Technologies Used
Python
Pandas
NumPy
Seaborn
Matplotlib
Scikit-learn
Key Features and Steps
Data Loading:
The dataset screentime_analysis.csv is loaded using Pandas.

Handling Missing Values:

#Missing values per column are analyzed.
Rows with excessive missing data are dropped using a threshold-based approach.
Outlier Detection and Removal:

Boxplot visualization of Usage (minutes) to identify outliers.
IQR (Interquartile Range) method applied to filter out extreme values.
#Duplicate Removal:

Number of duplicate rows is calculated and removed.
#Feature Engineering:

Date column is standardized to a datetime format.
New feature Total Interactions is created by summing Notifications and Times Opened.
#Data Scaling and Normalization:

Standard scaling is applied to Usage (minutes) using StandardScaler.
Min-Max normalization is applied using MinMaxScaler.
#Data Visualization:

Histogram of Usage (minutes) to visualize its distribution.
Summary Statistics:

Descriptive statistics of the cleaned dataset are printed.
#Logging and Output:

A log of data cleaning operations is saved to screentime_cleaning_log.txt.
Cleaned data is exported to cleaned_screentime_data.csv.
Usage
Run the script to clean and process the screentime dataset:

python screentime_cleaning.py
#Output Files
cleaned_screentime_data.csv: Contains the cleaned and processed dataset.
screentime_cleaning_log.txt: Summary of data cleaning operations.
#Visualization
Outliers in Usage (minutes)
Distribution of Usage (minutes)


