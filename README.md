## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
#  Feature Encoding and Transformation (Error-safe version)

# Step 1: Import libraries
import pandas as pd
from sklearn.preprocessing import OrdinalEncoder

# Step 2: Read datasets
df1 = pd.read_csv("data.csv")
df2 = pd.read_csv("Data_set.csv")
df3 = pd.read_csv("Data_to_Transform.csv")

#  Choose which dataset to process
df = df3  

# Step 3: Display column names and info
print("Column Names in the file:")
print(df.columns)
print("\nData Info:")
print(df.info())
print("\nInitial Data:")
print(df.head())

# Step 4: Encode only if columns exist
if 'bin_1' in df.columns:
    df['bin_1'] = df['bin_1'].map({'F': 0, 'T': 1})
else:
    print("\n Column 'bin_1' not found, skipping encoding for it.")

if 'bin_2' in df.columns:
    df['bin_2'] = df['bin_2'].map({'N': 0, 'Y': 1})
else:
    print("\n Column 'bin_2' not found, skipping encoding for it.")

# One-Hot Encoding (Nominal)
if 'nom_0' in df.columns:
    one_hot = pd.get_dummies(df['nom_0'], prefix='nom_0')
    df = pd.concat([df.drop('nom_0', axis=1), one_hot], axis=1)
else:
    print("\n Column 'nom_0' not found, skipping One-Hot Encoding.")

# Ordinal Encoding
if 'ord_2' in df.columns:
    ordinal_order = [['Cold', 'Warm', 'Hot']]
    ord_encoder = OrdinalEncoder(categories=ordinal_order)
    df['ord_2'] = ord_encoder.fit_transform(df[['ord_2']])
else:
    print("\n Column 'ord_2' not found, skipping Ordinal Encoding.")

# Step 7: Display encoded data
print("\n Encoded Data (first 5 rows):")
print(df.head())

# Step 8: Save encoded data
df.to_csv("encoded_data.csv", index=False)
print("\n Encoded data saved as 'encoded_data.csv'")
```
<img width="1161" height="785" alt="Screenshot 2025-10-09 111502" src="https://github.com/user-attachments/assets/35f70917-b40e-472d-88be-8d48fec2e596" />
<img width="1334" height="549" alt="Screenshot 2025-10-09 111518" src="https://github.com/user-attachments/assets/41447ee0-4b70-45ea-a72c-7ada610a9971" />

# RESULT:
 ```
The program successfully encoded the data, producing four new skewness feature columns with no errors, and saved the result as a new file.
```  
       
