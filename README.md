# Analyzing-customer-churn-in-Power-BI

# Data Analysis for Customer Churn

This repository contains scripts and instructions for analyzing customer churn data. The primary goal is to ensure data integrity and calculate key metrics related to customer churn.

## First Step: Data Check

### 1. Checking Customer ID Count

We start by creating two measures to ensure the count of customer IDs matches the count of unique customer IDs:

- **Customer ID**: This measure counts the total number of customer IDs in the dataset.
- **Unique Cx**: This measure counts the number of unique customer IDs in the dataset.

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

### 2. Converting Churn Label
Next, we use an IF() function to convert the ‘Churn Label’ column into a ‘Churned’ column.

Here is the DAX formula for this measure:
```dax
Churned = IF('Databel – Data'[Churn Label] = "Yes", 1, 0)
```

### 3. Creating a Measure for Number of Churned Customers
We then create a measure for the number of churned customers using the previously created ‘Churned’ column:
```dax
Number of Churned Customers = SUM('Databel – Data'[Churned])
```

### 4. Calculating the Churn Rate
Finally, we calculate the churn rate:
```dax
Churn Rate = [Number of Churned Customers] / [Unique Cx]
```

By following the steps above, you can ensure your dataset does not contain duplicate customer IDs, and accurately calculate churn metrics. If duplicates are found or other issues arise, further data cleaning and investigation may be necessary.
