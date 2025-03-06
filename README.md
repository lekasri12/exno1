# EXNO:1
Data Cleaning Process
## REGISTER NUMBER: 212223100025

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

# Coding and Output:
```
from google.colab import drive
drive.mount('/content/drive')
import pandas as pd
import numpy as np
path='/content/drive/My Drive/Data_set.csv'
df=pd.read_csv(path)
df
```
![Screenshot 2025-03-06 130300](https://github.com/user-attachments/assets/c03695fb-5b9e-4d8d-a7ab-efa3e1be63d3)

```
#DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
df.isnull()
```
![Screenshot 2025-03-06 130323](https://github.com/user-attachments/assets/97168168-124b-4105-8ee8-1e72e8b325ce)


```
df.notnull()
```
![Screenshot 2025-03-06 130338](https://github.com/user-attachments/assets/4e925f07-5332-4cae-9508-7c77651c272b)

```
#DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df.isnull().sum()
```
![Screenshot 2025-03-06 130350](https://github.com/user-attachments/assets/e64e31e3-ce0e-4cea-9533-976fb61d56c4)

```
#DROP NULL VALUES
df.dropna()
```
![Screenshot 2025-03-06 130406](https://github.com/user-attachments/assets/64e932fc-e0f6-49d5-a700-aa7615cbceb3)

```
#FILL NULL VALUES WITH CONSTANT VALUE "O"
df.fillna(0)
```
![Screenshot 2025-03-06 130423](https://github.com/user-attachments/assets/75da5fa4-2363-4768-af0e-8f16bc37dbed)

```
#FILL NULL VALUES WITH ffill or bfill METHOD
df.ffill()
```
![Screenshot 2025-03-06 130441](https://github.com/user-attachments/assets/7661bedf-9f97-4a5d-a71f-876ca8f37c2a)

```
df.bfill()
```
![Screenshot 2025-03-06 130503](https://github.com/user-attachments/assets/79a91192-c65b-4847-9303-e78abd7392c9)

```
#CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
df['rating'].fillna(value=df['rating'].mean())
```
![Screenshot 2025-03-06 130518](https://github.com/user-attachments/assets/ed7b1d21-79db-454d-b8bc-2625bd4a7751)

```
df['current_overall_rank'].fillna(value=df['current_overall_rank'].mean())
```
![Screenshot 2025-03-06 130535](https://github.com/user-attachments/assets/49043e67-7013-4f5a-81ee-5d0e055506c3)

```
df['watchers'].fillna(value=df['watchers'].mean())
```
![Screenshot 2025-03-06 130551](https://github.com/user-attachments/assets/4897f0a4-95ae-4019-ab9e-b7cbc4e091ad)

```

```

            
# Result
          <<include your Result here>>
