# Analyzing-customer-churn-in-Power-BI

# First Step
# Data Quality Check for Customer IDs

This repository contains scripts and instructions to perform a data quality check on customer IDs. The goal is to ensure that the count of customer IDs matches the count of unique customer IDs.

### 1. Doing a Data Check

#### a) Measures to Check Customer ID Count

To verify the integrity of the customer data, we will create two measures:

1. **Customer ID**: This measure counts the total number of customer IDs in the dataset.
2. **Unique Cx**: This measure counts the number of unique customer IDs in the dataset.

Here are the DAX formulas for these measures:



```dax
Customer ID = COUNT('Databel – Data'[Customer ID])
Unique Cx = DISTINCTCOUNT('Databel – Data'[Customer ID])
```
The visualization shows as:
<br>
<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/efb0de97-9601-43ec-a417-691633c66cdb)

</div>
