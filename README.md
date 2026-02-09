# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding 
Import Required Libraries from Python Library:
````
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt
````
Reading the file and display first five data:
````
df=pd.read_csv("Data_set.csv")
df.head()
````
Data set Information:
````
df.info()
df.describe()
````
Handling Missing values and check Null Values:
````
df.isnull()
df.isnull().sum()
````
Filling the Missing Values with 0
````
df1=df.fillna(0)
df1
````
Forward Fill using ffill()
````
df_ffill=df.ffill()
df_ffill
````
Backward fill using bfill()
````
df_bfill=df.bfill()
df_bfill
````
Filling the missing values with mean values:
````
df['rating']=df['rating'].fillna(df['rating'].mean())
df['watchers']=df['watchers'].fillna(df['watchers'].mean())
df
````
Deleting the rows which contains atleast one missing values:
````
df_dropna=df.dropna()
df_dropna
````
Save the cleaned data in new file:
````
df_dropna.to_csv('exp1 data set.csv',index=False)
````
Detecting the outliers for Data_set.csv file:
Using IQR method:
````
sns.boxplot(x=df['watchers'])
plt.show()
````
Calculate Q1 and Q3 to perform Q3-Q1
````
Q1=df['watchers'].quantile(0.25)
Q3=df['watchers'].quantile(0.75)
IQR=Q3-Q1
print(f"The IQR value is {IQR}")
````
Detecting outliers:
````
outliers=df[(df['watchers']<(Q1-1.5*IQR)) | (df['watchers']>(Q3+1.5*IQR))]
outliers
````
Removing Outliers
````
removed_outliers=df[~((df['watchers']<(Q1-1.5*IQR)) | (df['watchers']>(Q3+1.5*IQR)))]
removed_outliers
````
Calculate Outliers using Z Score Method using current_overall_rank Column
````
z_score=np.abs(stats.zscore(df['rating'].dropna()))
z_score
````
Detecting Outliers
````
threshold=3
mask = np.zeros(len(df), dtype=bool)
mask[df['rating'].dropna().index] = z_score > threshold
outliers = df[mask]
print('outliers')
print(outliers)
````
Removing Outliers
````
mask = np.ones(len(df), dtype=bool) 
mask[df['rating'].dropna().index] = z_score <= threshold 
df_cleaned = df[mask]
df_cleaned
````
# Output

<img width="1093" height="715" alt="image" src="https://github.com/user-attachments/assets/dee44ed2-f2a5-4454-a2e5-8dfea1eef167" />


<img width="1478" height="630" alt="image" src="https://github.com/user-attachments/assets/b19b2aec-ef19-43b1-87e6-fff25a77c4d3" />


<img width="1569" height="634" alt="image" src="https://github.com/user-attachments/assets/7464f5c3-4ea9-45d8-9626-d50299135d12" />


<img width="1057" height="687" alt="image" src="https://github.com/user-attachments/assets/8acdfe1c-7458-4e48-a73f-dbe9a389ee64" />


<img width="1533" height="689" alt="image" src="https://github.com/user-attachments/assets/6ec00095-3770-4336-9759-2bfd4db24125" />


# Result
Thus, The Data Cleaning process is completed successfully.
