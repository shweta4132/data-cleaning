# data-cleaning
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Load the screentime dataset
data = pd.read_csv('screentime_analysis.csv')  

# missing values
print("Missing values per column:")
print(data.isnull().sum())

# Drop rows with many missing values
data = data.dropna(thresh=len(data.columns) - 2)



# Handle outliers using the IQR method for minutes
sns.boxplot(data=data['Usage (minutes)'])
plt.title('Outliers in Usage (minutes)')
plt.show()
Q1 = data['Usage (minutes)'].quantile(0.25)
Q3 = data['Usage (minutes)'].quantile(0.75)
IQR = Q3 - Q1
outlier_condition = (data['Usage (minutes)'] < (Q1 - 1.5 * IQR)) | (data['Usage (minutes)'] > (Q3 + 1.5 * IQR))
data = data[~outlier_condition]

# Remove duplicate rows
duplicates = data.duplicated().sum()
print(f"Number of duplicate rows: {duplicates}")
data.drop_duplicates(inplace=True)


data['Date'] = pd.to_datetime(data['Date'], errors='coerce')


data['Total Interactions'] = data['Notifications'] + data['Times Opened']

scaler = StandardScaler()
data['Scaled Usage (minutes)'] = scaler.fit_transform(data[['Usage (minutes)']])

minmax_scaler = MinMaxScaler()
data['Normalized Usage (minutes)'] = minmax_scaler.fit_transform(data[['Usage (minutes)']])


sns.histplot(data['Usage (minutes)'], kde=True)
plt.title('Distribution of Usage (minutes)')
plt.xlabel('Usage (minutes)')
plt.show()


print("Summary statistics:")
print(data.describe())


with open('screentime_cleaning_log.txt', 'w') as log_file:
    log_file.write("Screentime Data Cleaning and Processing Summary\n")
    log_file.write("Handled missing values by dropping rows with too many nulls.\n")
    log_file.write("Removed outliers in 'Usage (minutes)' based on the IQR method.\n")
    log_file.write(f"Removed {duplicates} duplicate rows.\n")
    log_file.write("Standardized date format in 'Date' column.\n")
    log_file.write("Created new feature 'Total Interactions'.\n")
    log_file.write("Applied scaling and normalization to 'Usage (minutes)'.\n")

# Save cleaned data
data.to_csv('cleaned_screentime_data.csv', index=False)

print("Data cleaning and processing complete.")
