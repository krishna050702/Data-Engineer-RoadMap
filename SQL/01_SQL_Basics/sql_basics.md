#### What is SQL ?
- SQL stands for Structured Query Language
- It's used to manage & query data stored in a relational database management system (RDBMS).

---

#### What is a RDBMS ?
- RDBMS stands for Relational Database Management System
- It's a type of database management system that stores data in a structured format, using rows and columns.

---

### SQL SELECT

- The SELECT statement is used to select data from a database.
```
SELECT col1, col2,...
FROM table_name;
```

- First line in the query is the SELECT statement, which specifies the columns to be selected.
- Second line specifies the table from which the data is to be selected.

### Select * Example
- The * character is used to select all columns from a table.
```
Select *
From table_name;
```

---

### SQL Where
- The <b>WHERE</b>clause is used to filter records on certain conditions.

```
SELECT col1, col2,...
FROM table_name
WHERE condition;
```

#### Where wtith Multiple Conditions
```
Select *
FROM table
WHERE condition1 AND/OR condition2 AND/OR condition3;
```

#### Where with =
```
Select *
FROM table
WHERE col1 = value;
```

!!! Note: The WHERE clause is not only used in SELECT statement, but also in UPDATE, DELETE, etc.

---

#### Using Logical Operators
- The <b>WHERE</b> clause is often used with other logical operators like <b>=</b> and <b>!=</b> to filter down rows.

| Operator | Definition | Example in Query | Interpretation |
| --- | --- | --- | --- |
| = | Equals to | ```value = 2``` | value is equal to 2 |
| !=, <> | Not equals to | ```value != 2``` | value is not equal to 2 |
| <, > | Less than, more than | ```value < 2,``` <br>```value  > 5 ``` | value is less than 2, value is more than 5 |
| <=, >= | Less than or equal to, more than or equal to | ```value <= 2,``` <br>```value  >= 5 ``` | value is equal to or less than 2, value is equal to or more than 5 |

---

#### SQL AND Operator
- The <b>AND</b> is a logical operator in SQL that allows you to select only rows that satisfy multiple conditions.

```
SELECT *
FROM table
WHERE col1 = value1 AND 
      col2 != value2 AND
      col3 <= value3;
```

#### SQL OR Operator
```
SELECT *
FROM table
WHERE (col1 = value1 OR 
      col2 != value2) AND
      col3 <= value3;
```

---

#### SQL NOT Operator
- The <b>NOT</b> operator is SQL is used to display records for which a condition is NOT True.
```
SELECT * FROM table
WHERE NOT amount = 5;
```
(considering amount is a column in the table)

##### Not Between
```
SELECT * FROM table
WHERE column_name BETWEEN value1 AND value2;
```
---

#### SQL Between
- The <b>BETWEEN</b> operator is used to select values within a range.
```
SELECT * FROM table
WHERE column_name BETWEEN value1 AND value2;
```

!!!Note: Between is inclusive, i.e. it includes the values of value1 and value2.

---

#### SQL IN Operator
- The <b>IN</b> operator allows us to specify multiple values in a single line's <b>WHERE</b> clause, instead of using multiple <b>OR</b> conditions.
```
SELECT * 
FROM table
WHERE column_name IN (value1, value2, value3);
```

---
#### SQL LIKE Operator
- General synatx
```
Select *
FROM table
where column LIKE ....
    AND/OR column NOT Like ....;
```

- If we want to select a name which has K in it, we can use the following query.
```
Select *
FROM table
where name LIKE '%K%';
``` 

- The reason we use the % sign is because it is a wildcard character, and tells the database to match all the rows that have any character before K and any character after K making sure K is in the name.

- <b>SQL Like _ Example</b>
```
Select *
FROM table
where name LIKE 'K_i_h_a';
```
- It will match the name with 7 characters where the first character is K, the third character is i, the fifth character is h and the last character is a. eg. Krishna.

#### SQL Wildcard Characters
| Example in Query | Definition |
| --- | --- |
| ```WHERE name LIKE 'a%'``` | Finds any values that start with "a"|
| ```WHERE name LIKE '%a'``` | Finds any values that end with "a"|
| ```WHERE name LIKE '%ae%'``` | Finds any values that "ae" in the middle|
| ```WHERE name LIKE '_b%'``` | Finds any values that "b" in the second position|
| ```WHERE name LIKE 'a%o'``` | Finds any values that starts with "a" and ends with "o"|
| ```WHERE name LIKE 'a___'``` | Finds any values that starts with "a" and has 3 characters|

---


#### SQL Filtering Summary
| Operator | Definition | Example in Query | Interpretation |
| --- | --- | --- | --- |
| = | Equals to | ```user_id = 2``` | user_id is equal to 2 |
| !=, <> | Not equals to | ```user_id != 2``` | user_id is not equal to 2 |
| <,> | Less than, more than | ```age < 5``` | age is less than 5 |
| <=, >= | Less than or equal to, more than or equal to | ``` age <= 5``` | age is equal to or less than 5 |
| Between... <br> And... | Between a range | ```age BETWEEN 5 AND 10``` | age is between 5 and 10 |
| IN(...) | In a list of values | ```name IN ('Krishna','Panther','Lucifer')``` | name is either Krishna, Panther or Lucifer |
| LIKE | Search for a pattern | ```name LIKE 'K%'``` | name starts with K |

---

#### SQL Order By
- Ascending Order (no need to specify ASC its by default)
```
SELECT *
FROM table
WHERE condition(s)
ORDER BY column_name ASC;
```

- Descending Order
```
SELECT *
FROM table
WHERE condition(s)
ORDER BY column_name DESC;
```

- Multiple Columns
```
SELECT *
FROM table
WHERE condition(s)
ORDER BY column_name1 ASC, column_name2 DESC;
```

---

#### SQL LIMIT and OFFSET
- The <b>LIMIT</b> clause is used to limit the number of rows returned in a result set.
- The <b>OFFSET</b> clause is used to specify the number of rows to skip before starting to return rows from the query.

```
SELECT *
FROM table
WHERE condition(s)
ORDER BY column_name ASC
LIMIT number_of_rows OFFSET number_of_rows_to_skip;
```

---

!!! Note Let's Start with Intermediate topics in SQL.
