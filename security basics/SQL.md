to log in: `mysql -u root -p`
user: -u
prompt: `-p`


#### create database
``mysql> CREATE DATABASE database_name;``

#### show databases:
``mysql> SHOW DATABASES;``

#### use database
``mysql> USE thm_bookmarket_db;``

### drop database
`mysql> DROP database database_name;`

### drop table
`mysql> DROP TABLE table_name;`

#### create table
`mysql> CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);`

#### show tables
`mysql> SHOW TABLES;`

#### describe
`DESCRIBE book_inventory`

#### alter
`mysql> ALTER TABLE book_inventory
ADD page_count INT;`




# CRUD

#### create
`mysql> INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");`

#### read
`SELECT * FROM books;`
`SELECT name, description FROM books`

#### update
`mysql> UPDATE books
    SET description = "An In-Depth Guide to Android's Security Architecture."
    WHERE id = 1;`


#### delete
`mysql> DELETE FROM books WHERE id = 1;`


# Clauses

### DISTINCT
- used to select unique items: 
- `mysql> SELECT DISTINCT name FROM books;`

### GROUP BY
-  clause aggregates data from multiple records and groups the query results in columns
- `mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name;
+----------------------------+----------+
| name                       | COUNT(*) |
+----------------------------+----------+
| Android Security Internals |        1 |
| Bug Bounty Bootcamp        |        1 |
| Car Hacker's Handbook      |        1 |
| Designing Secure Software  |        1 |
| Ethical Hacking            |        2 |
+----------------------------+----------+`

### ORDER BY (sorting)

`mysql> SELECT *
    FROM books
    ORDER BY published_date ASC;`

### HAVING

`mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name
    HAVING name LIKE '%Hack%';`


### Operators
- Booleans: `TRUE` and `FALSE`

LIKE operators: `LIKE` and `WHERE`
examples: 
- `mysql> SELECT *
    FROM books
    WHERE description LIKE "%guide%";`


``AND`` and ``OR``
- `mysql> SELECT *
    FROM books
    WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp"; `

- `mysql> SELECT *
    FROM books
    WHERE name LIKE "%Android%" OR name LIKE "%iOS%"; `

NOT operator:
- `mysql> SELECT *
    FROM books
    WHERE NOT description LIKE "%guide%";`

BETWEEN operator
- `mysql> SELECT *
    FROM books
    WHERE id BETWEEN 2 AND 4;`

EQUAL TO operator
- `mysql> SELECT *
    FROM books
    WHERE name = "Designing Secure Software";`

NOT EQUAL TO operator
- `mysql> SELECT *
    FROM books
    WHERE category != "Offensive Security";`

LESS THAN operator
- `mysql> SELECT *
    FROM books
    WHERE published_date < "2020-01-01";`

GREATER THAN operator
- `mysql> SELECT *
    FROM books
    WHERE published_date > "2020-01-01";`

Less Than or Equal To and Greater  Than or Equal To Operators
- `mysql> SELECT *
    FROM books
    WHERE published_date <= "2021-11-15";`

- mysql> SELECT *
    FROM books
    WHERE published_date >= "2021-11-02";


### Functions

CONCAT() Function
- `mysql> SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;`

GROUP_CONCAT() Function
- `mysql> SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
    FROM books
    GROUP BY category;`

SUBSTRING() Function
- `mysql> SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;`

LENGTH() Function
- `mysql> SELECT LENGTH(name) AS name_length FROM books;`

COUNT() Function
- `mysql> SELECT COUNT(*) AS total_books FROM books;`

SUM() Function
- `mysql> SELECT SUM(price) AS total_price FROM books;`

MAX() Function
- `mysql> SELECT MAX(published_date) AS latest_book FROM books;`

MIN() Function
- `mysql> SELECT MIN(published_date) AS earliest_book FROM books;`

