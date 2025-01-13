
---

# Sales Insights Data Analysis Project

This project focuses on analyzing sales data to gain valuable insights. It involves working with SQL for querying a database and using Power BI for data visualization. Below are the instructions to set up and perform data analysis.

---

## 1. **Setting Up MySQL on Your Local Computer**

- **Download the SQL Database Dump:**  
  First, download the `db_dump.sql` file from this repository to your local machine.

- **Import the Database:**  
  Follow the instructions from the tutorial video to import the `db_dump.sql` file into your local MySQL instance.

---

## 2. **Data Analysis Using SQL**

Perform the following queries to analyze the data:

### a. **Show All Customer Records**
```sql
SELECT * FROM customers;
```

### b. **Show the Total Number of Customers**
```sql
SELECT count(*) FROM customers;
```

### c. **Show Transactions for Chennai Market (Market Code: Mark001)**
```sql
SELECT * FROM transactions WHERE market_code='Mark001';
```

### d. **Show Distinct Product Codes Sold in Chennai**
```sql
SELECT DISTINCT product_code FROM transactions WHERE market_code='Mark001';
```

### e. **Show Transactions in US Dollars**
```sql
SELECT * FROM transactions WHERE currency="USD";
```

### f. **Show Transactions in 2020**
```sql
SELECT transactions.*, date.* 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020;
```

### g. **Show Total Revenue in 2020**
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 
AND (transactions.currency = "INR" OR transactions.currency = "USD");
```

### h. **Show Total Revenue in January 2020**
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 
AND date.month_name = "January" 
AND (transactions.currency = "INR" OR transactions.currency = "USD");
```

### i. **Show Total Revenue in Chennai (2020)**
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date = date.date 
WHERE date.year = 2020 
AND transactions.market_code = "Mark001";
```

---

## 3. **Data Analysis Using Power BI**

In Power BI, you'll be transforming and visualizing the sales data. To standardize the sales amount across currencies, you can use the following formula to create a new column called `norm_amount`.

### Formula for `norm_amount` Column:
```text
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
```

This formula converts the `sales_amount` from USD to INR by multiplying it by a conversion factor (75). If the currency is INR, it leaves the amount unchanged.

![Power BI Screenshot](https://github.com/user-attachments/assets/f5531e12-e7bc-4e88-b12b-87546b3d7b00)

---

## 4. **Conclusion**

After executing the SQL queries and applying the necessary transformations in Power BI, you'll be able to visualize trends in the sales data and gain deeper insights into customer behavior, market performance, and revenue growth.

