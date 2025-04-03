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
