#### Introduction

Credit card fraud is a major problem for the financial industry, especially in Europe where electronic payments are widespread. Fraudsters are becoming more skilled, and their tactics are changing, thus it's essential to develop effective and adaptable systems to stop them.

This project tackles the persistent problem of credit card fraud in Europe using data science and machine learning models. The main objective is to create a robust fraud detection system that analyzes transaction data, pinpoints unusual patterns, and flags potential fraud.

By implementing this system, the project intends to strengthen the security of credit card transactions, protect consumers' financial well-being, and minimize the financial risks faced by banks.

A large dataset of credit card transactions from Kaggle is used, specifically from European cardholders in 2023. By studying different parts of each transaction, like the amount, time, location, and coded credit card details, the goal is to find unique traits that set apart real transactions from fraudulent ones.

### Data Collection

This project utilizes the "Credit Card Fraud Detection Dataset 2023" from Kaggle, which provides over 550,000 European credit card transactions recorded in 2023. The dataset encompasses transaction details like amount, attributes (time, location), and a label indicating fraudulent activity. Moreover, it includes anonymized credit card information. By analyzing this extensive dataset, the project seeks to uncover valuable insights.

In this part of the code, necessary libraries should be imported, specifically Pandas, which is a powerful data manipulation tool in Python.

Next, the dataset is loaded into a Pandas DataFrame using the pd.read_csv() function. The dataset, named "creditcard_2023.csv", is located at the specified file path.

```python
import pandas as pd

# Load the dataset
df = pd.read_csv("C:/Users/TECHCOM/Desktop/Data Science Capstone Project/creditcard_2023.csv")
```
After loading the dataset, information about the DataFrame using df.info() and statistical summary using df.describe() is printed out.

```python
print(df.info())
print(df.describe())
df.columns
```
```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 568630 entries, 0 to 568629
Data columns (total 31 columns):
 #   Column  Non-Null Count   Dtype  
---  ------  --------------   -----  
 0   id      568630 non-null  int64  
 1   V1      568630 non-null  float64
 2   V2      568630 non-null  float64
 3   V3      568630 non-null  float64
 4   V4      568630 non-null  float64
 5   V5      568630 non-null  float64
 6   V6      568630 non-null  float64
 7   V7      568630 non-null  float64
 8   V8      568630 non-null  float64
 9   V9      568630 non-null  float64
 10  V10     568630 non-null  float64
 11  V11     568630 non-null  float64
 12  V12     568630 non-null  float64
 13  V13     568630 non-null  float64
 14  V14     568630 non-null  float64
 15  V15     568630 non-null  float64
 16  V16     568630 non-null  float64
 17  V17     568630 non-null  float64
 18  V18     568630 non-null  float64
 19  V19     568630 non-null  float64
 20  V20     568630 non-null  float64
 21  V21     568630 non-null  float64
 22  V22     568630 non-null  float64
 23  V23     568630 non-null  float64
 24  V24     568630 non-null  float64
 25  V25     568630 non-null  float64
 26  V26     568630 non-null  float64
 27  V27     568630 non-null  float64
 28  V28     568630 non-null  float64
 29  Amount  568630 non-null  float64
 30  Class   568630 non-null  int64  
dtypes: float64(29), int64(2)
memory usage: 134.5 MB
None
                  id            V1            V2            V3            V4  \
count  568630.000000  5.686300e+05  5.686300e+05  5.686300e+05  5.686300e+05   
mean   284314.500000 -5.638058e-17 -1.319545e-16 -3.518788e-17 -2.879008e-17   
std    164149.486121  1.000001e+00  1.000001e+00  1.000001e+00  1.000001e+00   
min         0.000000 -3.495584e+00 -4.996657e+01 -3.183760e+00 -4.951222e+00   
25%    142157.250000 -5.652859e-01 -4.866777e-01 -6.492987e-01 -6.560203e-01   
50%    284314.500000 -9.363846e-02 -1.358939e-01  3.528579e-04 -7.376152e-02   
75%    426471.750000  8.326582e-01  3.435552e-01  6.285380e-01  7.070047e-01   
max    568629.000000  2.229046e+00  4.361865e+00  1.412583e+01  3.201536e+00   

                 V5            V6            V7            V8            V9  \
count  5.686300e+05  5.686300e+05  5.686300e+05  5.686300e+05  5.686300e+05   
mean   7.997245e-18 -3.958636e-17 -3.198898e-17  2.109273e-17  3.998623e-17   
std    1.000001e+00  1.000001e+00  1.000001e+00  1.000001e+00  1.000001e+00   
min   -9.952786e+00 -2.111111e+01 -4.351839e+00 -1.075634e+01 -3.751919e+00   
25%   -2.934955e-01 -4.458712e-01 -2.835329e-01 -1.922572e-01 -5.687446e-01   
50%    8.108788e-02  7.871758e-02  2.333659e-01 -1.145242e-01  9.252647e-02   
75%    4.397368e-01  4.977881e-01  5.259548e-01  4.729905e-02  5.592621e-01   
max    4.271689e+01  2.616840e+01  2.178730e+02  5.958040e+00  2.027006e+01   

       ...           V21           V22           V23           V24  \
count  ...  5.686300e+05  5.686300e+05  5.686300e+05  5.686300e+05   
mean   ...  4.758361e-17  3.948640e-18  6.194741e-18 -2.799036e-18   
std    ...  1.000001e+00  1.000001e+00  1.000001e+00  1.000001e+00   
min    ... -1.938252e+01 -7.734798e+00 -3.029545e+01 -4.067968e+00   
25%    ... -1.664408e-01 -4.904892e-01 -2.376289e-01 -6.515801e-01   
50%    ... -3.743065e-02 -2.732881e-02 -5.968903e-02  1.590123e-02   
75%    ...  1.479787e-01  4.638817e-01  1.557153e-01  7.007374e-01   
max    ...  8.087080e+00  1.263251e+01  3.170763e+01  1.296564e+01   

                V25           V26           V27           V28         Amount  \
count  5.686300e+05  5.686300e+05  5.686300e+05  5.686300e+05  568630.000000   
mean  -3.178905e-17 -7.497417e-18 -3.598760e-17  2.609101e-17   12041.957635   
std    1.000001e+00  1.000001e+00  1.000001e+00  1.000001e+00    6919.644449   
min   -1.361263e+01 -8.226969e+00 -1.049863e+01 -3.903524e+01      50.010000   
25%   -5.541485e-01 -6.318948e-01 -3.049607e-01 -2.318783e-01    6054.892500   
50%   -8.193162e-03 -1.189208e-02 -1.729111e-01 -1.392973e-02   12030.150000   
75%    5.500147e-01  6.728879e-01  3.340230e-01  4.095903e-01   18036.330000   
max    1.462151e+01  5.623285e+00  1.132311e+02  7.725594e+01   24039.930000   

          Class  
count  568630.0  
mean        0.5  
std         0.5  
min         0.0  
25%         0.0  
50%         0.5  
75%         1.0  
max         1.0  

[8 rows x 31 columns]
Index(['id', 'V1', 'V2', 'V3', 'V4', 'V5', 'V6', 'V7', 'V8', 'V9', 'V10',
       'V11', 'V12', 'V13', 'V14', 'V15', 'V16', 'V17', 'V18', 'V19', 'V20',
       'V21', 'V22', 'V23', 'V24', 'V25', 'V26', 'V27', 'V28', 'Amount',
       'Class'],
      dtype='object')
```
The output displays the structure of the DataFrame, showing that it contains 568,630 entries and 31 columns. Each column represents different feature of credit card transactions, such as transaction amount (Amount), transaction attributes (V1 through V28), and a binary label indicating whether the transaction is fraudulent (Class) or not.

Additionally, the output explains that there are no missing values in the dataset, as indicated by the non-null counts for all columns in the info() output.

### Data Processing and Cleaning

During this stage, the data is prepared for analysis and modeling. Following steps should be taken:

Data Loading: Importing the mentioned dataset.

Column Management: Getting rid of columns that are not very important and useful, thus making it easier to analyze the dataset.

Duplicate Removal: Deleting duplicate rows, keeping only the unique data for accurate results.

Feature-Label Separation: Splitting the dataset into features (input variables) and labels (output variables) for use in supervised learning algorithms.

Feature Scaling: Adjusting the range of features to improve model accuracy and speed.

Class Distribution: Analyzing the distribution of classes in order to design effective modeling approaches.

Correlation Analysis: Examining relationships between features and the target variable in order to get guidance for feature selection and interpretation.

Class Imbalance Management: Using the SMOTE technique, the representation of minority classes are balanced, ensuring fair model training.

Feature Engineering: Enhancing the dataset by introducing polynomial features to capture complex relationships that may not be evident in the original data. By meticulously processing and cleaning the data, a well-prepared dataset is created for accurate analysis and robust model development. This provides a strong foundation for our fraud detection system.

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import LocalOutlierFactor

# Load the dataset
df = pd.read_csv("C:/Users/TECHCOM/Desktop/Data Science Capstone Project/creditcard_2023.csv")

# Drop unnecessary columns
df.drop(columns=['id'], inplace=True)  # Drop 'id'

# Remove duplicate rows
df = df.drop_duplicates()

# Separate features and labels
X = df.drop(columns=['Class'])  # Features
y = df['Class']  # Labels

# Feature scaling
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Check for missing values
missing_values = df.isnull().sum()
print("Missing values:\n", missing_values)

# Check data types
data_types = df.dtypes
print("Data types:\n", data_types)

# Here, we'll use the Z-score method to detect outliers in the 'Amount' column and replace them with the median
from scipy import stats
z_scores = stats.zscore(df['Amount'])
outliers = (z_scores > 3) | (z_scores < -3)
df.loc[outliers, 'Amount'] = df['Amount'].median()

# Check summary statistics after handling outliers
summary_statistics_after = df.describe()

# Check for duplicates again (after removing outliers)
duplicates_after = df.duplicated().sum()
print("Number of duplicates after removal:", duplicates_after)

# Check target distribution
target_distribution = df['Class'].value_counts()
print("Target distribution:\n", target_distribution)

# Check correlations
correlation_matrix = df.corr()

# Initialize the Local Outlier Factor detector
lof = LocalOutlierFactor(n_neighbors=20, contamination=0.05)  # Adjust parameters as needed

# Fit the model and predict outliers
df['Anomaly'] = lof.fit_predict(df[['Amount']])

# Flag or remove anomalous records based on the predictions
anomalies = df[df['Anomaly'] == -1]
```
```text
Missing values:
 V1        0
V2        0
V3        0
V4        0
V5        0
V6        0
V7        0
V8        0
V9        0
V10       0
V11       0
V12       0
V13       0
V14       0
V15       0
V16       0
V17       0
V18       0
V19       0
V20       0
V21       0
V22       0
V23       0
V24       0
V25       0
V26       0
V27       0
V28       0
Amount    0
Class     0
dtype: int64
Data types:
 V1        float64
V2        float64
V3        float64
V4        float64
V5        float64
V6        float64
V7        float64
V8        float64
V9        float64
V10       float64
V11       float64
V12       float64
V13       float64
V14       float64
V15       float64
V16       float64
V17       float64
V18       float64
V19       float64
V20       float64
V21       float64
V22       float64
V23       float64
V24       float64
V25       float64
V26       float64
V27       float64
V28       float64
Amount    float64
Class       int64
dtype: object
Number of duplicates after removal: 0
Target distribution:
 Class
0    284315
1    284314
Name: count, dtype: int64
```
In this section of the code, we identify and handle any negative transaction amounts, which are unexpected in the context of credit card transactions.

```python
negative_amounts = df[df['Amount'] < 0]
print(negative_amounts)
```

```text
Empty DataFrame
Columns: [V1, V2, V3, V4, V5, V6, V7, V8, V9, V10, V11, V12, V13, V14, V15, V16, V17, V18, V19, V20, V21, V22, V23, V24, V25, V26, V27, V28, Amount, Class, Anomaly]
Index: []

[0 rows x 31 columns]
```
As a result, there aren't any transactions with negative amounts. This means that the data is accurate and follows the usual transaction rules. By completing this step, there is a high liklihood that the data include only valid and typical transaction records. Thus, this helps in making this fraud detection system more reliable and precise.

To prepare the dataset for analysis, the cleaning phase begins by removing missing values and duplicate entries, handling outliers, and standardizing formats. After cleaning, the data is saved in a CSV file named "cleaned_data.csv" using the Pandas to_csv() function. This file is the basis for future analysis and modeling work.

```python
df.to_csv("cleaned_data.csv", index=False)

import pandas as pd

# Import the cleaned data for further analysis
cleaned_data = pd.read_csv("cleaned_data.csv")
```
### Data Sampling

To solve the problem of unequal class representation in the dataset, Synthetic Minority Over-sampling Technique (SMOTE) is used. SMOTE is a common method for handling class imbalance by creating samples for the group with fewer samples. In this project, we SMOTE is used to increase the number of samples in the minority class (fraudulent transactions) in the training data. This helps create a balanced training set, making sure that the machine learning model is not biased towards the group with more samples. The resampled training data (X_train_resampled and y_train_resampled) is used to train the model, which improved its ability to predict the minority class while also keeping it able to generalize to the whole dataset.

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from imblearn.over_sampling import SMOTE

# Load the cleaned dataset
cleaned_data = pd.read_csv("cleaned_data.csv")

# Separate features and target variable
X = cleaned_data.drop(columns=['Class'])  # Features
y = cleaned_data['Class']  # Target variable

# Splitting the dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Application of SMOTE (Synthetic Minority Over-sampling Technique) to handle class imbalance
smote = SMOTE(random_state=42)
X_train_resampled, y_train_resampled = smote.fit_resample(X_train, y_train)
```
Data Exploration

Data exploration is crucial for a data science project. It provides a comprehensive overview of the data, allowing to gain insights and make informed decisions. By using visualization techniques, patterns, outliers, and relationships in the data can be identified. This process does not involve only the analysis of numbers; it uncovers the hidden story behind the data and use it to make better decisions. Data exploration is like a compass and a map, providing guidance through the vast ocean of data to valuable insights.

Visual representations are key to exploring data. Complicated data are shown in ways that make sense and are easy to understand. Visualizations like histograms, box plots, scatter plots, and heatmaps help in understanding how data is spread out, how it's related to other data, and what patterns it has.

Furthermore, this step helps in choosing the best modeling techniques, feature engineering strategies, and ways to measure success, which leads to accurate and informative predictive models.
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Combine resampled features and target variable into a single DataFrame
resampled_data = pd.concat([X_train_resampled, y_train_resampled], axis=1)

# Distribution of the target variable
plt.figure(figsize=(6, 4))
sns.countplot(data=resampled_data, x='Class')
plt.title('Distribution of Target Variable (Resampled)')
plt.xlabel('Class')
plt.ylabel('Count')
plt.show()

# Distribution of numerical features
plt.figure(figsize=(12, 8))
sns.pairplot(resampled_data.sample(1000), hue='Class', diag_kind='kde')
plt.suptitle('Pairplot of Numerical Features (Resampled)', y=1.02)
plt.show()

# Correlation heatmap
plt.figure(figsize=(10, 8))
sns.heatmap(resampled_data.corr(), cmap='coolwarm', annot=True, fmt=".2f", linewidths=0.5)
plt.title('Correlation Heatmap (Resampled)')
plt.show()
