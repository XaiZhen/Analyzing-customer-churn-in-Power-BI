

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


## Second Step: Explore Data

### 1. Clustered Bar Chart of Churn Reasons

As shown in the graph below, a clustered bar chart has been created to show the reasons why customers become churned:
<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/7e925238-5ccc-41d5-8653-ac593077771c)


</div>

### 2. Map Visualization of Churn Rates by State
I created a map visualization to identify the states with higher churn rates.
<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/e922c6ea-25f0-45ca-8744-a9967deda1ee)

</div>

### 3. Insights from Discovered Data

I found some key insights from the data analysis:

1. The churn rate for Databel is approximately 27%.
2. About 45% of the reasons why customers churn are related to competitors (e.g., competitors have better products, better prices, or better offers).
3. The churn rate in California is abnormally high, exceeding 60%.




