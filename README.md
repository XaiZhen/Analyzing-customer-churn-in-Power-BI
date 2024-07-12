

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


## Third Step: Dive Deep to Discover the Data & Analyze Data

### 1. Categorizing Demographics by Age
In this step, I gathered the categorized demographic variables related to age in a new column called 'Demographics'. I used the IF() function to create a column with three categories: "Senior", "Under 30", and "Other".

Here is the DAX formula:

```dax
Demographics = 
IF(('Databel - Data'[Senior]) = "Yes", "Senior", 
    IF(('Databel - Data'[Under 30]) = "Yes", "Under 30", 
        "Other"
    ))
```
Check the Graph below
<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/0de86f92-771d-42d8-9ba9-ea20b702219b)
</div>


### 2. Creating Age Bins and Visualizing Customer Data

I created bins for the 'Age' column, choosing a bin size of 3. Then, I designed a line and stacked column chart to show the number of customers and churn rate for each age bracket. From the visualization, I found that the age bracket 25 has the highest number of customers.

<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/95ddb6ce-3459-413c-a74d-22262f44b8ae)

</div>

### 2. Analyzing Group Membership Impact on Phone Bill and Churn Rate

Now I want to analyze whether customers who are part of a group have a lower phone bill and if this impacts the churn rate. Please check the line and stacked column chart below.

<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/4dd78e3c-29e2-4216-a337-82e627f9f673)


</div>

### 3. Analyzing the Impact of Contract Types on Churn Rate

Since there are three different contract types:

- One year
- Two year
- Month-to-month
  
I decided to consolidate the values of yearly contracts into one category. This allows us to observe the differences between customers with yearly contracts and those with monthly contracts.

Firstly, I created a new column called "Contract Category" using the SWITCH() function to categorize the contract types. The DAX function looks like this:
```dax
Contract Category = SWITCH('Databel - Data'[Contract Type], "One Year", "Yearly", "Two Year", "Yearly", "Month-to-month", "Monthly")
```
To observe how yearly and monthly contracts affect the churn rate, I used a multi-row card visualization to show the differences. Please refer to the figure below.

<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/fe8d2d89-0017-4a68-9e6f-721025b502a3)

</div>

It can be seen that customers with monthly contracts have a higher churn rate than those with yearly contracts. Additionally, I created a clustered column chart to analyze how churn rates differ by contract category and gender. As shown in the graph below, females with monthly contracts have the highest churn rate, at 47.31%.

<div align="center">
  
![image](https://github.com/XaiZhen/Analyzing-customer-churn-in-Power-BI/assets/157572976/14b37657-446e-480a-8304-2621d167f1a4)

</div>


### 4. Investigating the Influence of Unlimited Data Plan on Churn Rate

To investigate how the 'unlimited data plan' influences the churn rate, I created a Table visualization to check the churn rate for customers with and without the unlimited plan. As shown in the table, customers on an unlimited plan are more likely to churn.

<div align="center">

![image](https://github.com/user-attachments/assets/8219d2b5-c489-4a28-b94f-95fb9eccf709)

</div>

To explore if this is related to a certain amount of mobile data (GB) usage, I created a new column 'Grouped Consumption' that classifies the average monthly GB download into the following groups:

- Less than 5 GB
- Between 5 and 10 GB
- 10 or more GB

The DAX formula used is:
```dax
Grouped Consumption = IF('Databel - Data'[Avg Monthly GB Download] < 5, "Less than 5 GB", 
    IF('Databel - Data'[Avg Monthly GB Download] < 10, "Between 5 and 10 GB", 
        "10 or more GB"
    )
)
```

Next, I created a clustered bar chart to visualize the 'Churn Rate' by 'Unlimited Data Plan' and by the different groups of the newly created column.
<div align="center">

![image](https://github.com/user-attachments/assets/a54d55b9-65ac-41e9-b7bc-d180c1c17569)

</div>


### 5. Analyzing the Impact of International Activity on Customer Churn

Moreover, it is essential to understand the international activity of customers and its relationship to churn. I want to analyze the behavior of customers who make international calls and determine if paying for an international plan influences their loyalty.

Firstly, I created a matrix that shows the churn rate by the variables 'Intl Plan' and 'Intl Active'. Then, I added a map visualization to display the different churn rates for each state.

As shown in the figure below, California (CA) has a particularly high percentage of churners. Additionally, 72% of customers who actively make international calls do not have an international plan.

<div align="center">

![image](https://github.com/user-attachments/assets/a586e0b4-fe05-480b-9568-a28cf465cbd0)

</div>

In this case, I would advise Databel to contact customers who are on an international but have not called internationallly and propose them downgrade their plan


### 6. Investigating Customer Behavior: Payment Method, Contract Type, and Account Length

Now I want to investigate three important topics related to customers: the payment method, the contract type, and the duration of customer relationships.

Firstly, I created a line chart using the account length and churn rate to evaluate if the churn rate decreases over time. As shown in the figure below, it appears that the churn rate does decrease over time. Next, I will investigate how this decrease varies across different types of contracts. To do this, I created another visualization - a pie chart to display the number of customers by their payment methods.

<div align="center">

![image](https://github.com/user-attachments/assets/f5a0e00e-d730-4dd9-ac4b-c847adbe3f38)
</div>
