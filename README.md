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



```
SELECT count(distinct(year(date))) 
FROM walmartsale
```

## DATA SOURCE
- Dataset can be accessed through the link below (https://github.com/Princekrampah/WalmartSalesAnalysis/blob/master/WalmartSalesData.csv.csv)
  
## ANALYTICAL TOOL
SQL - For loading, cleaning and exploration.




