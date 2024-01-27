# Walmart-Sale-Analysis

## PROJECT OVERVIEW
The project aim to analyze the retail sales data (Walmart sale data set) to gain insight into consumer behavior, product performance, and general market trends. SQL was for cleaning and exploration. The best performing city, branches,product and the sales trend of different products were determined. 

## DATA STRUCTURE
The dataset is a  structured tabular dataset capturing sales transactions in a retail environment. It contain a year sales dataset with 1000 rows and 17 columns. Key features of the dataset includes:

- Invoice ID: A unique identifier for each transaction.
- Branch: The location or branch where the sale occurred (A, B, C).
- City: The city in which the branch is situated (Yangon, Naypyitaw, Mandalay).
- Customer Type: Indicates whether the customer is a member or a normal customer.
- Gender: The gender of the customer making the purchase.
- Product Line: The category of the product being sold (e.g., Health and beauty, Electronic accessories, Food and beverages).
- Unit Price: The price of a single unit of the product.
- Quantity: The number of units purchased in the transaction.
- Tax 5%: The tax amount applied to the sale.
- Total: The total amount paid by the customer, including tax.
- Date and Time: Timestamps indicating when the transaction occurred.
- Payment Method: The method used by the customer to pay (Ewallet, Cash, Credit card).
- COGS (Cost of Goods Sold): The cost incurred to produce or purchase the goods sold.
- Gross Margin Percentage: The percentage representing the gross profit margin.
- Gross Income: The gross profit generated from the sale.
- Rating: The customer satisfaction rating for the transaction.


#### CODE FOR DISPLAING DATASET
```
SELECT count(distinct(year(date))) 
FROM walmartsale
```
#### DATASET PREVIEW
![Screenshot (655)](https://github.com/olaiyaaminat/Walmart-Sale-Analysis/assets/150556677/29d41a80-7e13-45e6-925e-dcd09ff84730)


## DATA SOURCE
- Dataset can be accessed through the link below (https://github.com/Princekrampah/WalmartSalesAnalysis/blob/master/WalmartSalesData.csv.csv)
  
## ANALYTICAL TOOL
Microsoft Excel - Data cleaning
SQL - For loading and exploration.

## DATA PREPARATION AND CLEANING
#### DATA IMPORTATION

The data was in comma seperated value (.csv) format and was load into the SQL software using the directory. The code below was used to view the dataset for better understanding in the database

---create database
```
Create database walmartporfolio
```
----view table from database
```
select *
From walmartsale
```

- Add a new column **timecategory** (morning,afternoon and evening) to give insight on which time of the day most sale were made.

---create timecategory column
  ```
select time,
	case
	When time BETWEEN '00:00:00'  AND '12:00:00' then 'Morning'
	When time BETWEEN '12:01:00'  AND '16:00:00' then 'Afternoon'
	ELSE 'Evening'
	END AS timecategory
	From walmartsale
  ```
---Alter table walmart
```
Alter table walmartsale
Add timecategory varchar(30)
```
----Update the table to include the timecategory column.

```
update walmartsale
set timecategory = (
case
	When time BETWEEN '00:00:00'  AND '12:00:00' then 'Morning'
	When time BETWEEN '12:01:00'  AND '16:00:00' then 'Afternoon'
	ELSE 'Evening'
	END
	)
```

- Add a new column **daysoftheweek** (Monday, Tuesday, Wednesday, Thursday, Friday,Saturday,Sunday) to give insight on days each branch get busy most.

  ---- create column daysoftheweek
  ```
  select date,
	DATENAME(WEEKDAY, date) AS dayoftheweek
	From walmartsale
  ```

---Alter table walmart
```
Alter table walmartsale
	Add dayoftheweek varchar(20)
```

----Update the table to include the daysoftheweek column.
```
update walmartsale
set dayoftheweek = (
DATENAME(WEEKDAY, date))
```
