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
|Age group|Amount|
|10-19    |34730 |
|20-29    |98215 |
|30-39    |95950 |
|40-49    |93795 |
|50+      |100085|

3. Total amount spent on each product category by different age brackets
```
Grouped_data = df.groupby(['Age group', 'Product Category'])['Total Amount'].sum().reset_index()
```
**Spending patterns of different Age brackets**

## Gender Soending Analysis
1. Calculating Total amount spent by each Gender
```Gender_Totalspend = df.groupby('Gender')['Total Amount'].sum().reset_index()
print(Gender_Totalspend)
```
   Gender        Total Amount
0  Female        232840
1  Male          223160

2. Product Preference by Gender
```Gender_preference = df.groupby(['Gender', 'Product Category'])['Total Amount'].sum().reset_index()
```
**A plot of Products showing preference by Total amount spent on each by each Gender**

3.Total_Amount spent by the Average Male vs Female
```Avg_amount_by_Gender = df.groupby('Gender')['Total Amount'].mean()
print(Avg_amount_by_Gender)
```
Gender
Female    456.549020
Male      455.428571

## Product Performance Analysis
1. Total revenue from Each Product Category
```Total_revenue = df.groupby('Product Category')['Total Amount'].sum().reset_index()
```
**A plot of Total revenue from Each Product**

2. Total number of each Product sold
```Total_num = df.groupby('Product Category')['Quantity'].sum().reset_index()
print(Total_num)
```
Product Category  Quantity
0      Beauty       771
1      Clothing     894
2      Electronics  849

## Recommendations
1. Create/Strengthen your online presence for age groups that show a higher inclination towards digital channels to improve sales.
2. Offer Age-group based discounts to incease client turn over for groups that are not performing well.
3. Create Product bundles, this pushes the sale of even products that are not getting alot of sales.
4. Engage with the community through events or partnerships that align with the interests of each age group.
5. Collect feedback from customers in each age/Gender group to understand their needs and expectations better.
