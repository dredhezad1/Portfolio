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
### Data Exploration

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
```
<p align="center"> <img src="Credit Card Fraud_Images/1.png" width="1200"> </p>

The first line of the code enables combining resampled data into a unified format, allowing for thorough analysis and modeling in the project.

Visual representations are made to examine different parts of the re-sampled data. A count plot is used to visualize the target variable's distribution, indicating the frequency of each class within it. This helps understand the balance or imbalance of classes in the dataset, which is important for creating predictive models.

Furthermore, Seaborn's pairplot() function is used to create a pair plot that examines the distribution of numerical features. By showing the relationships between pairs of numerical features, this graph aids in pattern detection. Additionally, kernel density estimation (KDE) plots on the diagonal provide insight into the distribution of each feature, revealing potential clusters, patterns, or outliers within the dataset.

A correlation heatmap is created to visualize how closely numerical features in the resampled dataset correlate with each other. Different colors in the heatmap show the strength and direction of these correlations, while values on the heatmap indicate the correlation coefficients. This lets us see which features are highly correlated, which can affect how well a model performs and cause multicollinearity problems.

```python
# Boxplot of numerical features by class
plt.figure(figsize=(12, 8))
for column in X_train_resampled.columns:
    plt.subplot(5, 6, list(X_train_resampled.columns).index(column) + 1)
    sns.boxplot(x=y_train_resampled, y=X_train_resampled[column])
    plt.title(column)
plt.tight_layout()
plt.show()
```
<p align="center"> <img src="Credit Card Fraud_Images/2.png" width="1200"> </p>

From the graphs above, inferences as following can be made:

Center (Median) The middle line inside the box shows where the data is split in half. This line represents the "average" value for each feature within each class.

Spread: The size of the box shows how spread out the data is. The wider the box, the more spread out the data is.

Whiskers: The lines that extend from the box show the full range of the data. The whiskers usually extend up to 1.5 times the middle 50% of the data. Data points that are outside the whiskers are considered outliers.

```python
# Histograms of numerical features by class
plt.figure(figsize=(12, 8))
for column in X_train_resampled.columns:
    plt.subplot(5, 6, list(X_train_resampled.columns).index(column) + 1)
    sns.histplot(data=resampled_data, x=column, hue='Class', kde=True)
    plt.title(column)
plt.tight_layout()
plt.show()
```
<p align="center"> <img src="Credit Card Fraud_Images/3.png" width="1200"> </p>

The shape of the histogram and density plot shows how the data is distributed, it it is normal or with a bell curve or skewed, or with an uneven tail. The highest point of the density plot (mode) represents the value that occurs most often within each class. The width and shape of the histogram and density plot indicate how spread out (varied) the values are within each class. A wider spread means there is more variation in the data.

```python
# Violin plot of numerical features by class
plt.figure(figsize=(12, 8))
for column in X_train_resampled.columns:
    plt.subplot(5, 6, list(X_train_resampled.columns).index(column) + 1)
    sns.violinplot(x=y_train_resampled, y=X_train_resampled[column], split=True)
    plt.title(column)
plt.tight_layout()
plt.show()
```
<p align="center"> <img src="Credit Card Fraud_Images/4.png" width="1200"> </p>

Violin plots visually display how numerical data is distributed across categories.

The shape of each violin shows the probability distribution of the data. A line inside the violin marks the median value, providing a quick measure of central tendency. The width of the violin at different points indicates the spread of the data. Dots outside the violin represent extreme values.The dots beyond the whiskers may indicate that potential outliers are present.

```python
plt.figure(figsize=(8, 6))
plt.scatter(df['V1'], df['V2'], alpha=0.5, c=df['Class'], cmap='coolwarm')
plt.xlabel('V1')
plt.ylabel('V2')
plt.title('Scatter Plot of V1 vs. V2 (colored by Class)')
plt.colorbar(label='Class')
plt.show()
```
<p align="center"> <img src="Credit Card Fraud_Images/5.png" width="1200"> </p>

This scatter plot shows each observation in the dataset as a point. The point's position on the graph is determined by the values of variables V1 and V2. Each point is colored based on its class label (0 or 1), which is indicated by the 'Class' variable.It is seen that the data is spread out based on where the points are located.

As a result the different colors, in this case blue and red are clearly seperated, which means that variables V1 and V2 do a good job of distinguishing between the classes.

```python
plt.figure(figsize=(8, 6))
plt.hist(df['Amount'], bins=30, color='skyblue', edgecolor='black')
plt.xlabel('Transaction Amount')
plt.ylabel('Frequency')
plt.title('Histogram of Transaction Amount')
plt.show()
```
<p align="center"> <img src="Credit Card Fraud_Images/6.png" width="1200"> </p>

The histogram displays the distribution of transaction sizes. The bars are relatively similar in length, indicating that there are no significant differences in the frequency of transactions across different amounts. This suggests that the distribution of transaction sizes is uniform, with no particular range of sizes disproportionately represented.

In conclusion, consistent transaction amounts make it harder for fraud and anomaly detection algorithms. A balanced distribution of transaction sizes helps the algorithm learn patterns across all amounts, enhancing its ability to detect suspicious activities effectively.

```python
plt.figure(figsize=(10, 6))
sns.boxplot(data=df, x='Class', y='V1', palette='pastel')
plt.xlabel('Class')
plt.ylabel('V1')
plt.title('Boxplot of V1 by Class')
plt.show()
```
<p align="center"> <img src="Credit Card Fraud_Images/7.png" width="1200"> </p>

The pairplot provides pairwise scatter plots of numerical features, colored by class. It helps to visualize relationships between features and identify potential patterns or separations between classes.

In this case, for fraudulent transactions (Class 1), the middle 50% of values for V1 (amount in the transaction) are less varied than for non-fraudulent transactions (Class 0). Both types of transactions have outliers, but they are more common in fraudulent transactions. This suggests that the range of V1 values is larger and more variable for fraudulent transactions.

```python
import seaborn as sns
import matplotlib.pyplot as plt

def pairplot_data_grid(data, x_var, y_var, hue_var):
    sns.set(style="ticks")
    pair_grid = sns.pairplot(data, x_vars=[x_var], y_vars=[y_var], hue=hue_var, height=5)
    plt.show()

# Example usage:
pairplot_data_grid(df, "Amount", "Class", "Class")
```
<p align="center"> <img src="Credit Card Fraud_Images/8.png" width="1200"> </p>

It can be observed that the fraud transactions are generally not above an amount of 25000.

```python
amount_more = 0
amount_less = 0

for i in range(df.shape[0]):
    if df.iloc[i]["Amount"] < 25000:
        amount_less += 1
    else:
        amount_more += 1

print("Number of transactions with Amount less than 25000:", amount_less)
print("Number of transactions with Amount greater than or equal to 25000:", amount_more)
```
```text
Number of transactions with Amount less than 25000: 568630
Number of transactions with Amount greater than or equal to 25000: 0
```

```python
percentage_less = (amount_less/df.shape[0])*100
percentage_less
```

```text
100.0
```

Hence, it is observed that the 100% of transactions amount are less than 25000.

```python
# Initialize counters
fraud = 0
legitimate = 0

# Loop through the DataFrame rows
for i in range(df.shape[0]):
    # Check if the transaction amount is less than 25000
    if df.iloc[i]["Amount"] < 25000:
        # Check if the transaction is fraudulent (Class 0)
        if df.iloc[i]["Class"] == 0:
            fraud += 1
        else:
            legitimate += 1

# Print the results
print("Number of fraudulent transactions with Amount less than 25000:", fraud)
print("Number of legitimate transactions with Amount less than 25000:", legitimate)
```
```text
Number of fraudulent transactions with Amount less than 25000: 284315
Number of legitimate transactions with Amount less than 25000: 284315
```
This indicates that all transactions in the dataset have an amount less than 250000.

```python
df.Class.value_counts()
```

```text
Class
0    284315
1    284315
Name: count, dtype: int64
```
### Feature Engineeiring

In this step, we create new features by combining existing ones using polynomial features transformation. This captures complex relationships and interactions between features, which might not be evident in the original individual features. We use the PolynomialFeatures class from scikit-learn to generate combinations of features up to a specific level (degree 2 in this case). The resulting X_poly dataset includes the original features and these newly generated combinations.

To ensure that all features have a consistent range, they are standardized before training the model. This is crucial for models like logistic regression, as scaling affects optimization and performance. Using the StandardScaler from scikit-learn, the features are transformed such that their mean becomes 0 and their standard deviation becomes 1. The standardized features are stored in a new variable called X_scaled.

The data is divided into training and testing groups. A logistic regression model is created with specific settings, like a maximum of 1,000 iterations to prevent overfitting. The training data is used to train the model. The trained model is tested on the testing data. Metrics like precision, recall, F1-score, and overall accuracy are used to evaluate the model's performance. Scikit-learn's classification_report function provides a detailed analysis of these metrics.

```python
#Adding interaction terms
from sklearn.preprocessing import PolynomialFeatures

poly = PolynomialFeatures(degree=2)
X_poly = poly.fit_transform(X)
```
```python
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report

# Split the data into train and test sets
X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2, random_state=42)

# Initialize and train a logistic regression model with increased max_iter
model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)

# Evaluate the model
y_pred = model.predict(X_test)
print(classification_report(y_test, y_pred))
```
```text
 precision    recall  f1-score   support

           0       0.95      0.98      0.96     56794
           1       0.98      0.95      0.96     56932

    accuracy                           0.96    113726
   macro avg       0.96      0.96      0.96    113726
weighted avg       0.96      0.96      0.96    113726
```

The classification report provides several metrics for evaluating the performance of the logistic regression model:

Precision: The proportion of true positive predictions among all positive predictions. For class 0 (non-fraudulent transactions), precision is 0.95, meaning that 95% of transactions predicted as non-fraudulent are actually non-fraudulent. For class 1 (fraudulent transactions), precision is 0.98, indicating that 98% of transactions predicted as fraudulent are truly fraudulent.

Recall: The proportion of true positive predictions among all actual positives. For class 0, recall is 0.98, meaning that 98% of actual non-fraudulent transactions are correctly identified as non-fraudulent. For class 1, recall is 0.95, indicating that 95% of actual fraudulent transactions are detected.

F1-score: The harmonic mean of precision and recall. It provides a balance between precision and recall. Both classes have an F1-score of 0.96, indicating good overall performance.

Support: The number of actual occurrences of each class in the test dataset.

Accuracy: The proportion of correctly classified instances out of all instances. The overall accuracy is 96%.

Macro avg: The average of precision, recall, and F1-score across classes, giving equal weight to each class.

Weighted avg: The weighted average of precision, recall, and F1-score, where each class's score is weighted by its support. This metric accounts for class imbalance.

Overall, the model shows strong performance with high precision, recall, and F1-score for both classes, as well as high accuracy. This indicates that the logistic regression model is effective in distinguishing between fraudulent and non-fraudulent transactions.

```python
# Hyperparameter tuning:

from sklearn.model_selection import GridSearchCV

#Grid search for logistic regression
param_grid = {'C': [0.001, 0.01, 0.1, 1, 10, 100]}
grid_search = GridSearchCV(LogisticRegression(), param_grid, cv=5)
grid_search.fit(X_train, y_train)

print("Best Parameters:", grid_search.best_params_)
```
```text
Best Parameters: {'C': 1}
```
The output indicates the best parameter found by the grid search cross-validation, which is C = 1 in this case. The parameter C represents the inverse of regularization strength in logistic regression. A smaller C value indicates stronger regularization.

Here's what it means:

C: Regularization parameter. Smaller values specify stronger regularization, meaning the model will be more constrained. Higher values of C allow the model to fit the training data more closely. In this case, the best parameter found by the grid search is C = 1, suggesting that moderate regularization is preferred for this logistic regression model on this dataset. This parameter value strikes a balance between fitting the training data well and avoiding overfitting.

```python
import pandas as pd
from sklearn.preprocessing import PolynomialFeatures
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LogisticRegression

# Load the cleaned dataset
cleaned_data = pd.read_csv("cleaned_data.csv")

# Separate features and target variable
X = cleaned_data.drop(columns=['Class'])  # Features
y = cleaned_data['Class']  # Target variable

# Generate polynomial features
poly = PolynomialFeatures(degree=2)
X_poly = poly.fit_transform(X)

# Initialize logistic regression model with custom parameters
model = LogisticRegression(max_iter=1000)  # Adjust max_iter as needed

# Perform cross-validation
cv_scores = cross_val_score(model, X_poly, y, cv=5)

# Print cross-validation scores and mean accuracy
print("Cross-Validation Scores:", cv_scores)
print("Mean CV Accuracy:", cv_scores.mean())
```
```text
Cross-Validation Scores: [0.95950794 0.96283172 0.95935846 0.96055431 0.96183777]
Mean CV Accuracy: 0.9608180395648604
```
The cross-validation scores give us the accuracy of the model for each part of the cross-validation. Due to the closeness of the score, 0.9595 and 0.9628, it can be inferred that the model produces accurate results across different subsets of the data.

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

# Load the cleaned dataset
df = pd.read_csv("cleaned_data.csv")

# Separate features (X) and target variable (y)
X = df.drop(columns=['Class'])
y = df['Class']

# Split the dataset into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Initialize logistic regression model with custom parameters
model = LogisticRegression(max_iter=10000, solver='saga', penalty='l1', C=0.1)

# Model Training
model.fit(X_train, y_train)
```
```text
LogisticRegression(C=0.1, max_iter=10000, penalty='l1', solver='saga')
```

This step begins by training a logistic regression model for a specific dataset using customized parameters. First, a cleaned DataFrame is loaded with the features (X) and target variable (y). This sets up the data for the machine learning process.

To evaluate the model's ability to handle new data, the dataset is split into training and testing sets using the "train_test_split" function from scikit-learn. This enables the testing of the model's performance on data it has not encountered before, ensuring its reliability and accuracy in real-world applications.

The logistic regression model is set up with specific parameters: the number of iterations is limited, the 'saga' solver is chosen, a 'l1' regularization penalty is applied, and the regularization strength is set to 0.1 (C=0.1). These settings are based on expertise in the field, tests, or past studies, and are designed to produce the best possible results.

After creating the model, the next step is to train it using real-world data. This is done by calling the "fit" method, which adjusts the model's settings. The goal of this training is to make the model better at predicting the desired outcome while minimizing errors.

The code snippet provides information about the logistic regression model after training, such as: the type of regularization penalty and its strength, the algorithm used to solve the model and the configuration of these choices. This information helps in understanding the modeling decisions made during the training process and how the model operates.

### Model Deployment

```python
import joblib

#The trained model is named 'model'
joblib.dump(model, 'model.pkl')
```
```text
['model.pkl']
```
Files with a .pkl extension usually contain serialized objects saved using Python's pickle module. In this case, "model.pkl" probably has a serialized form of a machine learning model called "model." This format is used to store trained models, allowing them to be quickly loaded and used again without having to redo the training process.


### Results

To conclude, this project has focused on improving the safety of credit card transactions within Europe. An advanced machine learning model was created to precisely identify fraudulent activities while maintaining ethical principles. This work helps in increasing trust in digital financial dealings, leading to a more secure financial environment.




