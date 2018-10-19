# SQL I (PostgreSQL)

## Slides

### How does a DB fit in

- Multiple clients talk to a server.
- One server talks to one database.
- Users cant interface with database directly to ensure users don't mess up data.
- Persistent data.

### What is SQL

- Structured query language.
- often called `Sequel`.
- Look like spreadsheets.
- SQL uses the paradigm called relational data.
- Many versions of SQL.

### MySQL

- syntax is the same.
- most things transfer over very easily.
- Be Sure to include `postgreSQL` in sql searches.

### Normalization and Schema

- Normalization: to create structure out of data, or to organize it so that the result of getting info is unambiguous.
- Schema: The outline for the data, Normalizing your data creates a Schema.

### Data Relations

- many to many
- one to many
- one to one

## Normalize/schema Practice

### Naming Conventions

https://docs.google.com/spreadsheets/d/12ND6OHd3M2IPHRBHuN4E2FyAaVNcGq4hac6Q3y4Ip7I/edit#gid=0

- Tables and Columns are not plural
- column names use _ for spaces (because not case sensitive)

- Walk the students through taking the data on the `Normalization` sheet and turn it into tables.
  - Create a users table with the users
    - teach them about primary keys so each user can have a unique identifier.
  - Create a products table.
    - Very similar to the users table
  - Create an orders table
    - This one will probably throw students for a loop, they may want to keep adding in columns for each item but you should show them how thats wrong.
  - Create a line items table to be a `junction table` between `order` and `product`

### Schema

- Show them the schema visual in the slides for the DB we just created.

## Writing SQL

### SQL Syntax

- Key words typically written all uppercase.
- must use single quotes.
- Statements end in `;`.
- No Trailing Commas.
- comments use --

```sql
  SELECT * FROM film
  WHERE id = '5';
```

### Creating Tables

- Start with the syntax for creating tables.
  - First we give the table a name then give it column names, data types, and constraints.

  ```SQL

  -- Command     Table
    CREATE TABLE account (
  -- Column  Data Type    Constraints
      id     serial    PRIMARY KEY NOT NULL
      name   text       NOT NULL
      email  text
    )

  ```

  - Data Types
    - `Null`
      - when the cell is empty, not the same as `''`
    - Number
      - `INTEGER` - Round Number, no decimals places.
      - `DECIMAL` - Unlimited Decimal places.
      - `FLOAT` - 15 decimal Places.
      - `SERIAL` - (Incrementing Integer) usually used with primary keys
    - Characters
      - `TEXT` - Unlimited characters.
      - `VARCHAR(n)` - limited characters.
  - Constraints
    - `NOT NULL` - For when the cell can't be left empty.
    - `PRIMARY KEY` - The Unique Identifier for the table, can not repeat. Cell will auto populate.

- Create all 4 tables.
  
### Inserting Data into tables

- Show how to insert into tables using `INSERT INTO` and `VALUES`.

```SQL

-- Command    Table    Columns
  INSERT INTO account (name, email)
-- Command  Value             Value
  values ('Bob Ross', 'bobIsRoss@gmail.com'),('Tim Allen')

```

### Selecting Data

- Show how to select basic Data

```SQL
  SELECT *
  FROM account
  WHERE id = 1
```

- Specific Columns

```SQL
  SELECT name, email
  FROM account
```

- Rows with distinct data

```SQL
  SELECT DISTINCT STATE
  FROM account_order
```

- Group BY with distinct

```SQL
  SELECT Count(STATE), state
  FROM account_order
  group by state
```

- OrderBy

```SQL
  SELECT *
  FROM state
  Order By state ASC
```

- Limit results

```SQL
  Select price, product_name
  FROM product
  Order by ASC
  limit 10;
```

- Where

```SQL
  SELECT *
  FROM account
  where id > 10
```

- In, search for multiple values

```SQL
  SELECT *
  FROM account
  where name in ('Georgi', 'Vivie', 'Lorry')
```

- Like, contains part of this.
  - %a end with a
  - a% start with a
  - %a% has an a
  - _a% second letter is an a
  - %o% second to last letter is an o

```SQL
SELECT *
FROM account
WHERE email LIKE '%com'
```

- Not, show me all that are not like (can use !=)

```SQL
SELECT *
FROM account
WHERE email NOT LIKE '%com'
```

- AND / OR / BETWEEN

```SQL
SELECT *
FROM account
WHERE id < 10 and id > 5
-- WHERE id BETWEEN 5 and 10
```

```SQL
SELECT *
FROM account
WHERE id >= 10 or id <= 5
```

- SUM / AVG / MAX / MIN

```SQL
  Select AVG(price)
  FROM product
  where price > 20
```

### Removing Data

- Don't forget the where or every thing will get deleted

```SQL
  DELETE FROM account
  where id = 10
```

### Updating Data

- Change data in table

```SQL
  UPDATE accounts
  SET name = 'Bob Ross'
  WHERE id = 20;
```

## SQL Injection

```SQL
test@email.com'); drop table account; --
```