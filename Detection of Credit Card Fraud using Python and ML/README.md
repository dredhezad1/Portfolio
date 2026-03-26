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
