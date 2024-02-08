# Walmart Sale Analysis

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
- Dataset can be accessed through the link below (https://www.kaggle.com/datasets/alaxcarry/walmart-sales-data)
  
## ANALYTICAL TOOL
- Microsoft Excel - Data cleaning
- SQL - For loading and exploration.

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


- Add a new column **monthsname** It contains the months of the year on which the trasactions were made. it helps to determine the month with the higest sales and profit.
	---monthname.
```
select date,
	DATENAME(MONTH, date) AS monthname
	From walmartsale
```

---Alter table walmart
```
Alter table walmartsale
	Add monthname varchar(20)
```

----Update the table to include the monthsname column.


```
Update walmartsale
	set monthname = (
	DATENAME(MONTH, date) 
	)
```

### DATA EXPLORATION

## How many unique cities those the data have?

```
select distinct( city) as uniquecity
	from walmartsale
```
##  what is the loctaion of the city in each branch?

```
select distinct( city), branch
	from walmartsale
```

### PRODUCT ANALYSIS
## How many unique product line those the data have?

```
select distinct(Product_line) as uniqueproductline
	from walmartsale
```

## what is the common payment method?

```
select payment,  count(payment) as common_payment_method
	from walmartsale
	group by payment
	order by common_payment_method desc
```
## What is the most selling product line ?

```
select Product_line, COUNT(Product_line) as common_payment_method
	from walmartsale
	group by Product_line
	order by common_payment_method desc
```

## What is the total revenue by month?

```
select monthname,
	sum(total) as total_revenue
	from walmartsale
	group by monthname
	order by total_revenue desc
```

## What month have the largset cogs(cost of goods sold)?

```
select monthname,
	sum(cogs) as largest_cogs
	from walmartsale
	group by monthname
	order by largest_cogs desc
```

## What product line had the largest revenue?

```
select product_line,
	sum(total) as total_revenue
	from walmartsale
	group by product_line
	order by total_revenue desc
```

## What is the city with the largest revenue?

```
select city,branch,
	sum(total) as total_revenue
	from walmartsale
	group by city,branch
	order by total_revenue desc
```

## Which branch sold more products than average product sold?

```
select branch, 
	sum(quantity) as quantityproduct
	from walmartsale
	group by branch
	having sum(quantity) > (select avg (quantity) from walmartsale)
```

## What is the most common product line by gender?

```
select gender, product_line,
	count(gender) as total_count
	from walmartsale
	group by gender, product_line
	order by total_count desc
```

## Average rating of each product line

```
select product_line,
	round(avg(rating),2)as avg_rating
	from walmartsale
	group by  product_line
	order by avg_rating  desc
```

### SALE ANALYSIS

## Find number of sales in each time of the day per week

```
select timecategory,
	count(*) as total_sales
	from walmartsale
	where dayoftheweek = 'Monday'
	group by timecategory
	order by total_sales desc
```

## Which of the customer type brings the most revenue?

```
select customer_type,
	round(sum(total),2) as total_revenue 
	from walmartsale
	group by customer_type
	order by total_revenue  desc
```

## Which city has the largest tax percent?

```

	select city,
	round(avg(tax_5),2)  as tax
	from walmartsale
	group by city
	order by tax  desc
```

## Which customer type pays the most in tax?

```
select customer_type,
	round(avg(tax_5),2)  as tax
	from walmartsale
	group by customer_type
	order by tax  desc

```

## INSIGHT

## RECOMENDATION

## CONCLUSION

