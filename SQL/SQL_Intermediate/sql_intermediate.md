### Intermediate SQL
---
#### Aggregate Functions
- <b>SUM</b> adds together all the values in a particular column.
- <b>MIN</b> returns the lowest value in a particular column.
- <b>MAX</b> returns the highest value in a particular column.
- <b>AVG</b> calculates the average of a group of selected values.
- <b>Count</b> counts how many rows are in a particular column.

---

#### SUM
```
SELECT SUM(col_name)
FROM table_name;
```

---

#### MIN
```
SELECT MIN(col_name)
FROM table_name;
```

---

#### MAX
```
SELECT MAX(col_name)
FROM table_name;
```

---

#### AVG
```
SELECT AVG(col_name)
FROM table_name;
```

---
#### COUNT
- The ```COUNT()``` function enables you to count the total number of rows in a table.
```
SELECT COUNT(user_id)
FROM product;
```
- user_id is column in product table
- Generall syntax for COUNT will be:-
```
SELECT COUNT(*)
FROM table_name;
```
----

#### Real World Scenario for SQL aggregate functions
```
1. Calculating Total Sales for Financial Analysis. -> SUM()
2. Average Ratings for Product Reviews. -> AVG().
3. Identifying most active users. -> COUNT().
4. Finding lowest and highest prices. -> MIN() and MAX().
```

---

#### SQL Group By
```
SELECT col1, SUM(col2)
FROM table_name
GROUP BY col1;
```
- Example
```
select category, sum(spend)
from product
group by category;
```

!!! Note: We can ```group by``` multiple columns, just separate them by ```(,)```.

```
SELECT
    stock,
    EXTRACT(YEAR FROM date) AS year,
    ROUND(AVG(open),2) AS avg_open
FROM stock_prices
GROUP BY stock, year
ORDER BY year DESC:
```
!!! Note: And we can also use as numbers instead of column full name so instead of stock, year we can write GROUP BY 1, 2.

---

#### HAVING
- Having allows you to filter data based on values from aggregate functions. In the below example we can't use where condition as <b>Aggregate functions are not allowed with where.</b>
```
SELECT stock, AVG(open)
FROM stock_prices
GROUP BY stock
HAVING AVG(open) > 500;
```
---

#### WHERE vs HAVING
| | WHERE | HAVING |
|------|------|------|
| When it filters | Value BEFORE Grouping | Value After Grouping|
| Operates on Data From | Individual Rows | Aggregated Values from Groups of Rows |
| Example | ```Select username, followers``` <br>```FROM instagram_Data```<br>```WHERE followers > 1000;``` | ```Select country```<br>```FROM instagram_Data```<br>```GROUP BY country```<br>```Having AVG(followers) > 100;``` |

---

!!! Note: We can use having with multiple condition same as where by using and/or.

- General structure of SQL query while using Having
```
1. Select
2. FROM
3. Where
4. Group By
5. Having
6. Order By
```
----

#### Distinct
- The <b>DISTINCT</b> SQL command is used in conjuction with the <b>SELCT</b> statement to return only different values,
```
SELECT DISTINCT col1
FROM table_name;
```

- <b>DISTINCT</b> can be particularly helpful when exploring a new data set. In many real-world scenarios, you will generally end up writing several exploratory ```SELECT DISTINCT``` queries in order to figure out what data you have access too, and how you might want to group or filter the data.
- <b>DISTINCT with Two columns</b> If you include two or more columns in a ```SELECT DISTINCT``` clause, your results will contain all of the unique pairs of those two columns.

#### Count DISTINCT
```
SELECT COUNT(DISTINCT user_id)
from trades;
```

---

### SQL Arithmetic Operators

##### Addition +
```
SELECT salary + bonus as total_compensation
FROM employees;
```

##### Subtraction -
```
SELECT revenue - expenses AS profit
FROM product_sales;
```

##### Multiplication *
```
SELECT units_sold * price AS revenue FROM ecomm_orders;
```

##### Division /
```
SELECT country_gdp / population AS gdp_per_capita FROM econ_stats;
```

##### Modulus %
```
SELECT 23 % 6;
```

##### Exponentiation (^)
```
SELECT 10 ^ 2;
```

##### ABS():- Calculating Absolute Differences
- will get the difference in positive value.

##### ROUND():- 
- By using ROUND(AVG(close),2) you specify the number of decimals.
```
SELECT
    stock,
    AVG(close) AS avg_close,
    ROUND(AVG(close), 2) AS rounded_avg_close
FROM stock_prices
WHERE EXTRACT(YEAR FROM date) = 2025
GROUP BY stock;
```

---

##### CEIL() and FLOOR():- Rounding Up and Down
- We can utilize the ```CEIL()``` function to round up and the ```FLOOR()``` function to round down to the lowest and highest prices.

| high | CEIL() - Round up | | low | FLOOR() - Round down |
|------|--------------|-----------|--------|---------|
|224.20|225| | 201.06|206|
|218.76|219| | 181.82| 181|

---

##### POWER():- Calculatng Squared Values
- The ```POWER()``` function raises a number to a specified power, allowing us to perform exponential calculations.
- ```POWER(close, 2)```

---

##### MOD() or %
- The ```MOD()``` function or ```%``` modulo operator calculates the remainder of division between two numbers.

!!! Note:- ```CAST()``` or we can use ```::``` notation to cast data types.

---

#### SQL NULL
- ```IS NULL``` and ```IS NOT NULL``` :- Used to identify null and non-null values.
- ```COALESCE()``` :- Returns the first non-null value from a list of arguments.
- ```IFNULL()``` :- Substitutes null value with a specified value specified.

##### IS NULL
```
SELECT *
FROM table_name
WHERE col1 IS NULL;
```

##### IS NOT NULL
```
SELECT *
FROM table_name
WHERE col1 IS NOT NULL;
```

---

#### COALESCE()
- The ```COALESCE()``` function takes multiple inputs and returns the first non-null value.
```
COALESCE(column_name, 'expression')
```
- If ```column_name``` is NULL, it returns the specified 'expression'. Otherwise, it returns the value of ```column_name```.

---

#### Handling Gaps with SQL IFNULL()
``` IFNULL(column_name, value_if_null) ```

---

- ```COALESCE()``` is versatile for multiple arguments, it returns the first non-null value among them.
``` COALESCE(arg1, arg2, arg3, ....)```
- ```IFNULL()``` handles two arguments, returning the second if the first is null, else it returns the first.
```IFNULL(expression, value_if_null)```

---

### SQL CASE
- The ```CASE()``` statement in SQL allows you to shape, transform, manipulate, and filter data bassed on specified conditions.
```
SELECT
    column1,
    column2,
    CASE
        WHEN condition_1 THEN result_1
        WHEN condition_2 THEN result_2
        WHEN ..... THEN .....
        ELSE result_3
    END AS column_3_name -- (Give your new column an alias)
FROM table_1;
```

!!! We can use Case in where condition also.

```
SELECT
  platform,
  COUNT(CASE 
    WHEN followers >= 500000 THEN 1
    ELSE NULL
  END) AS popular_actor_count,
  COUNT(CASE 
    WHEN followers < 500000 THEN 1
    ELSE NULL
  END) AS less_popular_actor_count
FROM marvel_avengers
GROUP BY platform;
```

!!! Similarly we can use SUM(), AVG().

---

### SQL JOINS
