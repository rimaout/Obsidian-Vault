---
type: Uni Note
class:
academic year: 2024/2025
related:
completed: false
created: 2025-07-22T19:30
updated: 2026-01-31T13:32
---
## Creating Tables

**Syntax:**

```sql
CREATE TABLE table_name (
	column_name + data_type + constraints (optional)
	...
)
```

**Example:**

```sql
CREATE TABLE person (
	id SERIAL NOT NULL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	gender VARCHAR(7) NOT NULL,
	date_of_birth DATE NOT NULL,
	email VARCHAR(100) UNIQUE
)
```

The [[#Constraints|constraints]] used are:
- `NOT NULL`: Ensures the column cannot have a NULL value
- `SERIAL`: Automatically generates a unique, incrementing integer
- `PRIMARY KEY`: Uniquely identifies each record in the table
- `UNIQUE` to prevent duplicate

## Deleting Tables

```sql
DROP TABLE table_name;
```

## Inserting Tuples

**Syntax:**

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

**Example:**

```sql
INSERT INTO person (first_name, last_name, gender, date_of_birth, email)
VALUES 
    ('Marco', 'Rossi', 'Male', '1990-05-15', 'marco.rs@example.com'),
    ('Paperina', 'Pepe', 'Female', '1985-03-22', 'pap.pe@example.com');
```
- When using `SERIAL`,  the value is automatically created (increasing thr value of the latest person tuple), so you don't have to specify it when inserting records.

```sql
INSERT INTO person (first_name, last_name, gender, date_of_birth)
VALUES ('Lucia', 'Bianchi', 'Female', '1952-05-15')
```
- In the original table design, the `email` column does not have a `NOT NULL` constraint, this means you can insert a record without providing an email address.

>[!tip] Synthetic Data Generator
>
> To exercise or test databases, create synthetic data for tables using [Mockaroo](https://mockaroo.com/).
> 
> Once you've exported your synthetic data, you can import the SQL file in [[PSQL (PostgreSQL Terminal Interface)|psql]] using: `\i [file_path]`.

## Deleting Tuples

```sql
DELETE FROM table_name WHERE condition
```

**Example:**

```sql
DELETE FROM person WHERE date_of_birth < '1900-01-01';
```