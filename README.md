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
## IQR DETECTION AND REMOVAL
```
import pandas as pd
import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![Screenshot 2025-03-13 160838](https://github.com/user-attachments/assets/10f004cc-2190-4ef6-af23-fcd89c877fbf)

```
# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(af)
```
![Screenshot 2025-03-13 160848](https://github.com/user-attachments/assets/52de5921-bc3c-4f3d-a129-91326dd732f6)

```
sns.scatterplot(af)
```

![Screenshot 2025-03-13 160857](https://github.com/user-attachments/assets/9129733a-188c-411e-8dbc-0b244a55a6ec)

```
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![Screenshot 2025-03-13 160908](https://github.com/user-attachments/assets/68f2b13f-eaf1-4c1e-8116-69dc381e9178)



```
import numpy as np
Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)
IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers=[x for x in age if x < lower_bound.iloc[0] or x > upper_bound.iloc[0]]
```
![Screenshot 2025-03-13 160922](https://github.com/user-attachments/assets/1c1a92d9-33d0-4070-bb12-804f0003c52f)

```
print('Q1:',Q1)
print('Q3:',Q3)
print('IQR:',IQR)
print('Lower bound:',lower_bound)
print('Upper bound:',upper_bound)
print('Outliers:',outliers)
```
![Screenshot 2025-03-13 160930](https://github.com/user-attachments/assets/a3b371df-4b7a-4389-ab22-61d5acc4ad02)

```
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
```
![Screenshot 2025-03-13 160939](https://github.com/user-attachments/assets/8e309872-e1b5-40cb-98d9-7a9c9ba41396)

```
af.dropna()
```

![Screenshot 2025-03-13 160946](https://github.com/user-attachments/assets/f0cb7d71-05a9-4e90-8ae2-8670b8089e55)

```
sns.boxplot(af)
```
![Screenshot 2025-03-13 160958](https://github.com/user-attachments/assets/7e2435f8-2b39-4ebe-807d-059f4b7ea77c)
```
sns.scatterplot(af)
```
![Screenshot 2025-03-13 161007](https://github.com/user-attachments/assets/0945349e-840e-4e56-82a3-ac2046146f01)

## Z SCORE
```
from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
import numpy as np
import pandas as pd
import seaborn as sns
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data)
```
# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(df)
```

![Screenshot 2025-03-13 161501](https://github.com/user-attachments/assets/27a4ba80-de5c-437f-a1c9-2d0e5950cacc)

```
mean=np.mean(data)
mean
std=np.std(data)
std
```

![Screenshot 2025-03-13 161520](https://github.com/user-attachments/assets/d3fca379-56ea-4b47-ad24-04b1f418badb)

```
# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
z=np.abs(stats.zscore(df))
z
```

![Screenshot 2025-03-13 161532](https://github.com/user-attachments/assets/6977b0bd-4f64-4151-b35e-5ce6d6ad2882)

```
threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)
```

![Screenshot 2025-03-13 161532](https://github.com/user-attachments/assets/601e2e2e-2448-4c8f-b579-dc551734a8e8)


```
df_cleaned = df[(z <= threshold)]
df_cleaned
```
![Screenshot 2025-03-13 161545](https://github.com/user-attachments/assets/f950a751-a494-41d6-8d0c-d5eb6ab2bbf7)

```
# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(df_cleaned)
```
![Screenshot 2025-03-13 161556](https://github.com/user-attachments/assets/ad2f60d0-454a-4554-9f35-478cbad4df83)

```
sns.scatterplot(df_cleaned)
```
![Screenshot 2025-03-13 161607](https://github.com/user-attachments/assets/d3926aa4-bde8-495c-a99d-49d5ef33a5a0)


            
# Result
         Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
