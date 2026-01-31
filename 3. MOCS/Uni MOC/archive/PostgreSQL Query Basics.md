---
type: Uni Note
class: "[[Basi di Dati 2 (class)]]"
academic year: 2024/2025
related:
completed: false
created: 2025-07-10T16:05
updated: 2026-01-31T13:32
---
## SELECT

The `SELECT` statement is used to retrieve data from one or more database tables. It allows you to specify:
- the ***columns*** you want to retrieve, 
- the ***table(s)*** from which you want to retrieve the data
- and also, any ***conditions*** that must be met for the data to be included in the result set.

This statement can be combined with others to perform more complex queries.

>[!note] Sintax
>```java
>SELECT [columns] FROM [tables] WHERE [conditions]
>```
>
>>***Note:*** `*` con be use in `[columns]` to select all the columns form the specified tables.

>[!example] Example
>![[Pasted image 20250710163222.jpg|900]]

>[!question] Insight
>
>The result of a `SELECT` statement in SQL is a **result set**. This result set can be thought of as a temporary table, but it's not stored in the database and doesn't have a name.
>
>This result set can be manipulated as a table using other operation such as `WHERE`, `GROUP BY`, `ORDER BY`, and more.

## DISTINCT

The `DISTINCT` statement is used to remove duplicate rows from a result set. 

>[!note] Syntax
>
>```sql
>SELECT DISTINCT column1, column2, ...
>FROM table_name;
>```
>
>Distinct can also be used to filter the input of [[#Aggregation Operations]]:
>
>```sql
>-- Count unique values
>SELECT COUNT(DISTINCT column_name) 
>FROM table_name;
>
>-- Sum of unique values
>SELECT SUM(DISTINCT column_name) 
>FROM table_name;
>```

>[!example] Example
>
>``` sql
>SELECT DISTINCT customer_id, payment_date, amount 
>FROM payment
>```
>
>```text
>customer_id | payment_date | amount
>1           | 2023-05-15   | 50.00
>2           | 2023-05-16   | 75.50
>1           | 2023-05-17   | 25.00
>```

>[!note] DISTINCT ON
>
>It's used to *select only one row* from a set of rows that have the **same values in the specified columns**.
>
>```sql
>SELECT DISTINCT ON (customer_id) customer_id, payment_date, amount
>FROM payment;
>```
>
>Usually `DISTINCT ON` is used with an [[#ORDER BY]] statement to control which row is selected, for example:
>
>
>```sql
>SELECT DISTINCT ON (customer_id) customer_id, payment_date, amount
>FROM payment
>ORDER BY payment_date DESC;
>```
>- `ORDER BY payment_date DESC` sorts the rows in descending order based on the `payment_date`, so the most recent payments are at the top.
>- `SELECT DISTINCT ON (customer_id)` selects only one row per distinct `customer_id`. The `ON` clause specifies that the distinctness should be determined based on the `customer_id` column.
>
>So the result is the most recent payment for each customer.
>
>>[!example] Example
>>
>>For example, if the `payment` table contains the following data:
>>
>>```
>> customer_id | payment_date | amount
>>1           | 2022-01-01   | 10.00
>>1           | 2022-01-15   | 20.00
>>2           | 2022-02-01   | 30.00
>>3           | 2022-03-01   | 40.00
>>3           | 2022-03-15   | 50.00
>>```
>>
>>The query will return:
>>
>>```
>>customer_id | payment_date | amount
>>1           | 2022-01-15   | 20.00
>>2           | 2022-02-01   | 30.00
>>3           | 2022-03-15   | 50.00
>>```

## WHERE

The `WHERE` clause is typically used in combination with the [[#SELECT]] statement to filter rows based on specific conditions. The basic syntax is as follows:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

WHERE supports the usual conditional operations:
- `=`: equal to
- `!=` or `<>`: not equal to
- `>`, `>=`, `<`, `=` for comparison operations
- `AND`, `OR`, `NOT`: logic operators for combining multiple conditions

Bit it also supports more advanced operations such as:
- `BETWEEN`: Between a range of values (inclusive)
- `LIKE`: Pattern matching using wildcards (often used with `%` and `_`)
- `IN`: Matches any value in a list
- `IS NULL` Checks for null values

>[!note] Basic Operators
>	
>The **equal to** operator is used to filter rows where the specified column is equal to a given value.
>
>```sql
>SELECT * FROM employees
>WHERE department = 'sales';
>```
>
>---
>
>The **not equal to** operator is used to filter rows where the specified column is NOT equal to a given value.
>
>```sql
>SELECT * FROM employees
>WHERE department != 'sales';
>```
>
>---
>
>The **greater than** operator is used to filter rows where the specified column is greater than a specified value:
>
>```sql
>SELECT * FROM employees
>WHERE salary > 50000;
>```

>[!note] Advanced Operators
>
>The operator **BETWEEN** is used to filter rows where the specified column is within a range.
>
>```sql
>SELECT * FROM employees
>WHERE age BETWEEN 25 AND 50;
>```
>
>It can be used also with dates, days, hours, ecc:
>
>```sql
>WHERE oder_date BETWEEN '2023-01-01' AND '2023-06-30';
>```
>
>>***NOTE:*** It is `inclusive`, meaning it includes both the specified start and end values in the range.
>
>---
>
>The operator **IN** is used to filter rows where the specified column's values is contained in a "list" of given values.
>
>```sql
>SELECT * FROM employees
>WHERE department IN ('HR', 'IT', 'Finance');
>```
>
>>***Better Optimization:*** PostgreSQL's query optimizer can often optimize `IN` queries more effectively than complex combinations of `OR` conditions.
>
>---
>
>The operator **IS NULL** is used to filter rows where the specified column's values is `null`.
>
>```sql
>SELECT * FROM employees
>WHERE phone_number is NULL;
>```
>
>---
>
>The operator **LIKE** is used for pattern matching, like can uses normal symbols such as letters and numbers, but it also can use with wildcard chars `%`, `_`, and `[chars]` that can be used to match flexible patterns in text searches.
>- `%` represents zero, one or multiple characters
>- `_` represents a single character
>- `[chars]` matches exactly ONE character that is within the specified set of characters
>
>```sql
>-- Matches any name starting with 'John'
>WHERE name LIKE 'John%';
>
>-- Matches any 5-letter name starting with 'A'
>WHERE name LIKE 'A____';
>
>-- Matches any 5-letter name starting with 'A' or 'B' or 'C'
>WHERE name LIKE '[ABC]____';
>
>-- Matches names containing 'an' anywhere
>WHERE name LIKE '%an%';
>```
>
>>***Note:*** `LIKE` is **case-sensitive**, if you want it be be case-insensitive you can use `ILIKE`.

## ORDER BY

The `ORDER BY` clause is used to sort the result set in a specified order. The syntax is as follows:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE conditions
ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...;
```

- **ASC & DESC:** The `ASC` (ascending) and `DESC` (descending) option are optional, when not specified the default is ascending (`ASC`).
- **Data Type:** the sorting works on `chars`, `varchars`, `numbers` and `dates`.
- **NULL:** NULL is considered the lowest possible value when sorting. In ascending order, NULL values appear first; in descending order, they appear last.

>[!note] One Column Ordering 
>
>When ordering by a single column, you can specify the sorting direction:
>
>
>```sql
> -- Sort names in ascending order (default)
> SELECT * FROM employees ORDER BY name; 
>
> -- Sort names in descending order 
> SELECT * FROM employees ORDER BY name DESC;
>
> -- Sort salaries from highest to lowest
> SELECT * FROM employees ORDER BY salary DESC;`
> ```

> [!note] Multiple Column Ordering 
> 
> You can order by multiple columns, with each subsequent column used as a tiebreaker:
>
>```sql
>-- First sort by department in ascending order, 
>-- then sort salaries within each department from highest to lowest
>SELECT name, department, salary 
>FROM employees 
>ORDER BY department ASC, salary DESC;
>```

## LIMIT

The `LIMIT` command is used to restrict the number of rows returned by a query by specifying the maximum number of rows.

```sql
SELECT column1, column2, ...
FROM table_name
LIMIT number_of_rows
```

>***note:*** It's written always at the end of a query.

>[!example] Example
>
>```sql
>SELECT * FROM payment
>ORDER BY payment_date
>LIMIT 10
>```

>[!note] SQL Standard (FETCH FIRST)
>
>`LIMIT` isn't a SQL standard, but `FETCH FIRST n ROWS ONLY` is the standard SQL alternative to `LIMIT`.
>
>```sql
>SELECT * FROM payment
>ORDER BY payment_date
>FETCH FIRST 10 ROWS ONLY
>```

## OFFSET

The `OFFSET` clause allows you to skip a specified number of rows before starting to return results. It's typically used with [[#ORDER BY]] or [[#LIMIT]].

```sql
SELECT * FROM users ORDER BY id LIMIT 10 OFFSET 20;`
```
- Skips the first 20 rows
- Returns the next 10 rows

## Aggregation Operations
	
In PostgreSQL, aggregation operations are statements that **perform calculations** on a table or result set and return a **single result** (tuple).

The most common and simple aggregation operations are: 
- `COUNT()`: Counts the number of rows
- `SUM()`: Calculates the total of numeric values
- `AVG()`: Calculates the average of numeric values
- `MAX()`: Finds the maximum value
- `MIN()`: Finds the minimum value
 
>[!note] Single Tuple Output
>
>When using aggregate functions in a SELECT statement, any non-aggregated columns must be part of a GROUP BY clause, for example:
>
>This cases are allowed:
>
>```sql
>SELECT MAX(cost) from film
>SELECT MAX(cost), MIN(cost) from film
>```
>
>This is not:
>
>```sql
>SELECT title, MAX(cost) 
>FROM film;  -- Error: column "film.title" must appear in the GROUP BY clause
>```
>
>This is because aggregate functions produce a single value (or one value per group), while non-aggregated columns can have multiple values.
>
>---
>**How to SELECT title, MAX(cost) with out error:**
>
>In this case if we want to get the title of the films with the higher replacement cost we have two options:
>
>```sql
>WITH min_val AS (
>    SELECT MAX(replacement_cost) AS max_replacement_cost 
>    FROM film
>)
>
>SELECT * 
>FROM film, max_val
>WHERE film.replacement_cost = max_val.max_replacement_cost;
>```
>
>```sql
>SELECT * 
>FROM film
>WHERE replacement_cost = (SELECT MAX(replacement_cost) FROM film);
>```

### COUNT

The COUNT function counts the number of rows that match a specified condition within a table or a result set. 

It returns a single value representing the count of rows that meet the criteria.

>[!note] COUNT(\*)
>
>Use `COUNT(*)` to count the total number of rows in a table, irrespective of whether there are `NULL` values.
>
>

>[!note] COUNT(column_name)
>
>The `COUNT(column_name)` counts the number of non-NULL values in the specified column. 
>
>So It ignores `NULL` values in that particular column and only counts the rows where the specified column has a non-NULL value.

>[!note] COUNT + DISTINCT
>
>The [[#DISTINCT]] keyword is used to eliminate duplicate rows from the result set. When combined with the COUNT function, it allows you to *count the number of unique values in a specific column*.
>
>
>**For example:** count the name of the departments in the "employees" table:
>
>![[Pasted image 20250711121322.png|1000]]
>
>1. To get the ***output 1*** we can use: `SELECT COUNT(department) FROM employees`
>2. To get the ***output 2*** we can use: `SELECT COUNT(DISTINCT department) FROM employees`

## GROUP BY

The `GROUP BY` clause divides the result set into groups based on common values present in the defined columns, then a [[#Aggregation Operations|Aggregate Function]] operates on each group separately, producing a single row for each group.

The GROUP BY operation follows a Split, Apply, Combine process. Let's consider a hypothetical sales table with columns "Region," "Product," and "SalesAmount." To analyze total sales for each region, we apply the following steps:
- ***Split:*** The dataset is divided into groups based on unique values in the "Region" column.
- ***Apply:*** Aggregate functions, such as SUM(SalesAmount), are applied to the "SalesAmount" column within each region group.
- ***Combine:*** The aggregated results are combined, creating a summary table that displays the total sales for each region!

![[Pasted image 20250721170831.png|1000]]

>[!note] HAVING (filtering)
>
>`HAVING` it's a clause that uses a condition to filter the resulting groups resulted from `group by`. 
>
>It's important to net get confused with `where`, that filters the result of the `select`.
>
>|WHERE|HAVING|
>|---|---|
>|Filters before grouping|Filters after grouping|
>|Works on individual rows|Works on grouped results|
>|Cannot use aggregate functions|Can use aggregate functions|
>|Comes before GROUP BY|Comes after GROUP BY|
>
>>[!example]- Example
>>
>>```sql
>>SELECT department, 
>>       AVG(salary) as avg_salary, 
>>       COUNT(*) as employee_count
>>FROM employees
>>GROUP BY department
>>HAVING AVG(salary) > 50000 
>>   AND COUNT(*) > 5;
>>```
>>
>>In this example:
>>- Groups employees by department
>>- Calculates average salary and employee count per department
>>- Filters to show only departments with:
>>  1. Average salary over $50,000
>>  2. More than 5 employees

## AS

The `AS` statements is uses to give "nicknames" to tables, columns, or calculations within you queries.

>[!note] Giving Simpler Names
>
>``` sql
>SELECT 
>    first_name AS fname, 
>    last_name AS lname, 
>    email_address AS contact_email
>FROM employees;
>```

>[!note] Renaming Columns from Aggregate Functions
>
>```sql
>SELECT 
>    department, 
>    AVG(salary) AS average_department_salary,
>    COUNT(*) AS total_employees,
>    SUM(bonus) AS total_bonus_payout
>FROM employee_compensation
>GROUP BY department;
>```

>[!note] Disambiguating Tables with Same Column Names
>
>```sql
>SELECT 
>    e.id AS employee_id, 
>    e.name AS employee_name,
>    d.name AS department_name
>FROM employees e
>JOIN departments d ON e.department_id = d.id;
>```

>[!note] Calculations with Aliases
>
>```sql
>SELECT 
>    product_name, 
>    price, 
>    price * 1.1 AS price_with_tax
>FROM products;
>```

>[!note] Subquery Aliases
>
>```sql
>SELECT department, avg_salary
>FROM (
>    SELECT department, AVG(salary) AS avg_salary
>    FROM employees
>    GROUP BY department
>) AS dept_salaries
>WHERE avg_salary > 50000;
>```


## ## Arithmetic Operations

PostgreSQL supports standard arithmetic operations in SELECT queries:

```sql
SELECT 
    column_name,
    column1 + column2 AS sum,
    column1 - column2 AS difference,
    column1 * column2 AS multiplication,
    column1 / column2 AS division,
    column1 % column2 AS modulo
FROM table_name;
```

- Operations work with numeric data types
- Can be used in SELECT, WHERE, and ORDER BY clauses

>[!example] Example
>
>Apply a 10% discount to car prices
>
>```SQL
>SELECT 
>		id, maker, model, price,
>		ROUND(price * .10, 2) AS discount, 
>		ROUND(price - price * .10,  2) as final_price
>FROM car
>```
>
>```
>  id  |     maker     |          model          |  price   | discount | final_price
>-----+---------------+-------------------------+----------+----------+-------------
>    1 | GMC           | 3500 Club Coupe         | 58907.00 |  5890.70 |    53016.30
>    2 | GMC           | Envoy                   | 28756.00 |  2875.60 |    25880.40
>    3 | GMC           | Vandura 2500            | 15068.00 |  1506.80 |    13561.20
>    4 | Mercury       | Lynx                    | 65885.00 |  6588.50 |    59296.50
>    5 | Lexus         | GX                      | 27477.00 |  2747.70 |    24729.30
>```
>
>***Note:*** `ROUND()` is a function used to round a numeric value to a specified number of decimal places.

PostgreSQL follows standard mathematical order of operations (PEMDAS):
1. Parentheses `()`
2. Exponents `^`
3. Multiplication `*`, Division `/`, Modulo `%`
4. Addition `+`, Subtraction `-`

```sql
SELECT (2 + 3) * 4 AS result;  -- Result is 20, not 14
```

## COALESCE

`COALESCE` returns the first non-NULL value in a "list", if all arguments are NULL, returns NULL.

```sql
COALESCE(value1, value2, ..., valueN)
```

>[!example] Example
>
>```sql
>SELECT COALESCE(email, 'Email not provided')
>```
>
>**output:**
>
>```
>              coalesce
>------------------------------------
 >fdickson0@unc.edu
 >jgiraldo1@independent.co.uk
 >Email not provided
>```

## NULLIF (division by zero)

`NULLIF` returns NULL if the two input value are equal, otherwise returns the first value.

```sql
NULLIF(val1, val2)
```

This operation can be really useful for handling potential division by zero.

>[!bug] Division by Zero
>
>In PostgreSQL a division by zero will return an error:
>
>```sql
>SELECT 10 / 0; --ERROR: division by zero
>```
>
>But a division by NULL is allowed and will return a "empty" (null) value.
>
>```sql
>SELECT 10 / NULL;
>```
>
>***Output:***
>
>```
> ?column?
>----------
>
>```

>[!note] Handling division by zero using NULLIF
>
>When performing division where the denominator might be zero, use NULLIF to prevent division by zero errors. This ensures that instead of raising an error, the result becomes NULL when the denominator is zero.
>
>>***Note:*** It's always possible to use [[#COALESCE]] to replace null values with a default value, such as zero or another meaningful placeholder.
>
>```sql
>SELECT 
>    product_name,
>    total_sales,
>    num_sold,
>    total_sales / NULLIF(num_sold, 0) AS average_price
>FROM product_sales
>```


## Date/Time

In PostgreSQL there are many ways to represent time and dates:

>[!note] Date Type
>
>`DATE`: Stores date values (year, month, day)
>
>```sql
>-- Examples
>'2023-11-15'
>'2024-02-29'
>```

>[!note] Time Type
>
>`TIME`: Stores time of day
> 
>
>```sql
>-- Without time zone
>'14:30:00'
>-- With time zone
>'14:30:00+02:00'
>```

>[!note] Timestamp Type
>
>`TIMESTAMP`: Combines date and time
>
>```sql
>-- Without time zone
>'2023-11-15 14:30:00'
>-- With time zone
>'2023-11-15 14:30:00+02:00'
>```

>[!note] Interval Type
>
>`INTERVAL`: Represents a period of time
>
>```sql
>-- Various interval representations
>'1 year 2 months'
>'3 days 4 hours'
>'30 minutes'
>```

^210e7e

### Constants

There are special date/time constants:
- `CURRENT_DATE`
- `CURRENT_TIME`
- `CURRENT_TIMESTAMP`

### Operations

In a nutshell, this are the operation that can be used between date/time data types:

- `+` : Add interval to date/timestamp
-  `-`  : Subtract interval or calculate difference
- `*` : Multiply interval
- `<`, `>`, `<=`, `>=` : Comparison operators
- `BETWEEN` : Range checking

Not in a nutshell, this are the operation that can be used between date/time data types:

| Operation                     | Description                            | Example                                                                          |
| ----------------------------- | -------------------------------------- | -------------------------------------------------------------------------------- |
| `date + integer`              | Add a number of days to a date         | `date '2001-09-28' + 7 → 2001-10-05`                                             |
| `date + interval`             | Add an interval to a date              | `date '2001-09-28' + interval '1 hour' → 2001-09-28 01:00:00`                    |
| `date + time`                 | Add a time-of-day to a date            | `date '2001-09-28' + time '03:00' → 2001-09-28 03:00:00`                         |
| `interval + interval`         | Add intervals                          | `interval '1 day' + interval '1 hour' → 1 day 01:00:00`                          |
| `timestamp + interval`        | Add an interval to a timestamp         | `timestamp '2001-09-28 01:00' + interval '23 hours' → 2001-09-29 00:00:00`       |
| `time + interval`             | Add an interval to a time              | `time '01:00' + interval '3 hours' → 04:00:00`                                   |
| `- interval`                  | Negate an interval                     | `- interval '23 hours' → -23:00:00`                                              |
| `date - date`                 | Subtract dates, producing days elapsed | `date '2001-10-01' - date '2001-09-28' → 3`                                      |
| `date - integer`              | Subtract days from a date              | `date '2001-10-01' - 7 → 2001-09-24`                                             |
| `date - interval`             | Subtract an interval from a date       | `date '2001-09-28' - interval '1 hour' → 2001-09-27 23:00:00`                    |
| `time - time`                 | Subtract times                         | `time '05:00' - time '03:00' → 02:00:00`                                         |
| `time - interval`             | Subtract an interval from a time       | `time '05:00' - interval '2 hours' → 03:00:00`                                   |
| `timestamp - interval`        | Subtract an interval from a timestamp  | `timestamp '2001-09-28 23:00' - interval '23 hours' → 2001-09-28 00:00:00`       |
| `interval - interval`         | Subtract intervals                     | `interval '1 day' - interval '1 hour' → 1 day -01:00:00`                         |
| `timestamp - timestamp`       | Subtract timestamps                    | `timestamp '2001-09-29 03:00' - timestamp '2001-07-27 12:00' → 63 days 15:00:00` |
| `interval * double precision` | Multiply an interval by a scalar       | `interval '1 second' * 900 → 00:15:00`                                           |
| `interval / double precision` | Divide an interval by a scalar         | `interval '1 hour' / 1.5 → 00:40:00`                                             |

```sql
-- Check if date is within a specific range
SELECT * FROM employees 
WHERE hire_date BETWEEN '2020-01-01' AND '2022-12-31';
```

### Functions

There are specific function that can be used on date and time types:

>[!note] EXTRACT
>
>`extract()`is used to pull specific components form date ore time, for example:
>
>```sql
>-- Extract year, month, day form a date
>EXTRACT(YEAR FROM current_date)
>EXTRACT(MONTH FROM current_timestamp)
>EXTRACT(DOW FROM current_date)  -- Day of week
>```
>
>```sql
>-- Extract hour, minute, second from current time
>EXTRACT(HOUR FROM current_time)
>EXTRACT(MINUTE FROM current_time)
>EXTRACT(SECOND FROM current_time)
>
>-- Additional time-related extractions
>EXTRACT(EPOCH FROM current_time)  -- Seconds since midnight
>```
>
>>There are also the `MILLISECONDS` and `MICROSECONDS` components for `TIME`.

>[!warning] Day of the week rap presentation
>
>Days of the week use a numeric representation, this means that:
>
>`EXTRACT(DOW FROM date)` returns:
>- `0` = Sunday     
>- `1` = Monday     
>- `2` = Tuesday     
>- `3` = Wednesday     
>- `4` = Thursday     
>- `5` = Friday     
>- `6` = Saturday
>  
>But they can be converted to text by using:
>
>```sql
>-- Convert numeric to text
>SELECT TO_CHAR(CURRENT_DATE, 'Day');  -- 'Monday'
>SELECT TO_CHAR(CURRENT_DATE, 'Dy');   -- 'Mon'
>```

>[!note] Extremely Specific Operations
>
>In PostgreSQL there are a lot of specific operation that can used on dates, to see all of the use the [official documentation](https://www.postgresql.org/docs/current/functions-datetime.html).
>
>But one of the must useful is `AGE()`:
>
>```sql
>-- Age from a specific date to now
>SELECT AGE('1990-05-15');
>
>-- Age between two specific dates
>SELECT AGE('2023-01-01', '1990-05-15');
>```
>
>This functions return a [[#^210e7e|INTERVAL data tipe]] and can be used to do stuff like this:
>
>```sql
>SELECT name 
>FROM persons 
>WHERE age(birthdate) >= INTERVAL '18 years';
>```
