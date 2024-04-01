# EDA and Time Series Anlaysis
## Project Overview 
This data Analysis project involves performing EDA and a Time-series analysis on a retail Slaes Data set. 
I will also provide insights on customer versus Product Analysis.

## Data Source
The data set was downloaded from kaggle as a csv file.
## Tools 
- Pandas (Explaratory Data Analysis and descriptive Analysis)
- Matplotlib (Data Visualization)
- Seaborn (Data Visualization)

## Uploading data and Explatory Data Analysis
Uploadind data set and viewing it 
```
df = pd.read_csv("retail_sales_dataset.csv")
df.head()
```
EDA involved exploring the data to answer key questions such as;
1. Checking for Null-values
   ```Pandas
   df.isna().sum()
   ```
2. Checking data types for each column
```Pandas
df.info()
```
3. Finding number of unique entries for each column
  ```Pandas
df.nunique()
  ```
## Descriptive Analysis
1. Calculating Mean, Frequency, Standard deviation and median for different columns
```Pandas
df.derscibe()
```
2. Calculating Modal Values
```Pandas
df.mode().dropna()
```
## Data Manuplation for Time series Analysis.
1. Ordering data by date   
```
df=df.sort_values(by ="Date")
```
2. Converting Date's datatype to date_time
 ```
df["Date"] = pd.to_datetime(df["Date"])
```
**Visualization of the Times series plot**

![1](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/fa49b922-a7c4-475d-a126-4e0a3f1ff054)

## Time series Analysis by Month
1. Creating Month and Date Columns
```
df["Month"]=df["Date"].dt.month
df["Year"]=df["Date"].dt.year
```
2. Calculating Total Monthly_sales
```
Monthly_sales = df.groupby(["Year", "Month"], as_index=False)["Total Amount"].sum()
df['Monthly_sales']= Monthly_sales['Total Amount']
```
**A plot of Total_Monthly Sales Throughout the Year**

![2](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/b6aaafd7-eb7c-4c43-a19f-e71598fc1dac)

## Age Spending Analysis
1. Creating Age brackets
```
age_bins = [10, 20, 30, 40, 50, 60]
age_labels = ['10-19', '20-29', '30-39', '40-49', '50+']
df["Age group"] = pd.cut(df["Age"], bins=age_bins, labels=age_labels, right= True)
```
2. Calculating Total Amount Spent by each Age_group 
```
Total_amount_by_age = df.groupby('Age group')['Total Amount'].sum()
print(Total_amount_by_age)
```
![3](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/8f61a1ef-c71c-47e0-afea-8ad6eb605d40)


3. Total amount spent on each product category by different age brackets
```
Grouped_data = df.groupby(['Age group', 'Product Category'])['Total Amount'].sum().reset_index()
```
**Spending patterns of different Age brackets**

![4](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/e394367d-62e9-4a75-893f-ffb2148cab83)

## Gender Spending Analysis
1. Calculating Total amount spent by each Gender

```
Gender_Totalspend = df.groupby('Gender')['Total Amount'].sum().reset_index()
print(Gender_Totalspend)
```

![5](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/88ee4396-c9ed-426c-96bd-c10b4d0294a2)

2. Product Preference by Gender
```
Gender_preference = df.groupby(['Gender', 'Product Category'])['Total Amount'].sum().reset_index()
```
**A plot of Products showing preference by Total amount spent on each by each Gender**

![7](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/2db61249-1be3-4a70-89ac-e65ce2754447)

3.Total_Amount spent by the Average Male vs Female
```
Avg_amount_by_Gender = df.groupby('Gender')['Total Amount'].mean()
print(Avg_amount_by_Gender)
```

![8](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/1a7d65e2-5f49-49d8-ac66-f0a123361954)

## Product Performance Analysis
1. Total revenue from Each Product Category
```
Total_revenue = df.groupby('Product Category')['Total Amount'].sum().reset_index()
```
**A plot of Total revenue from Each Product**

![9](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/cdab0ee3-11ed-4c82-80a9-3ca08e771172)

2. Total number of each Product sold
```
Total_num = df.groupby('Product Category')['Quantity'].sum().reset_index()
print(Total_num)
```

![10](https://github.com/solomonadupa/Time-Series-Analysis/assets/160836596/642cccde-a67d-4c5d-8761-327d309748a9)

## Recommendations
1. Create/Strengthen your online presence for age groups that show a higher inclination towards digital channels to improve sales.
2. Offer Age-group based discounts to incease client turn over for groups that are not performing well.
3. Create Product bundles, this pushes the sale of even products that are not getting alot of sales.
4. Engage with the community through events or partnerships that align with the interests of each age group.
5. Collect feedback from customers in each age/Gender group to understand their needs and expectations better.
