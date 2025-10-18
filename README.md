# Database-SQL
This repo covers Introduction to DB, keys, CRUD, Joins, aggregator queries, subqueries, indexing, Transactions and Schema design
# Types of Databases
1. Rational DB - RDBMS
    - collection of related tables
    - Databae examples MySQL, Postgres, OracleDB, SQL Server

2. Non- Rational DB - No SQL DBMS
    - everything except a table like documents, K-V pair, json, graph DB etc.
    - Database examples grapQL, mangoDB, dynamoDB, Apache Cassandra, Firebase

# Properties of RDBMS
1. Rational Databases represnt a database as collection of tables which store something. This something can be entity or relationship between entities.

    Example- I have table named student where we will store information of all student (entity). Similarly i have table student_batch where we will store information about which student in which batch (relation between entities)

2. Every row is unique. That means, no 2 rows in table have same value for all columns.
    Example- In student table no two rows have same name, surname, age, attendance etc.

3. All of the values present in column hold same the same data type.Fix Data integrity.
    Example- In student table name should hold string data type, attendance should hold integer data type. No value from attendance should hold string data type.

4. Values are automic.
    Example- you can not store values as list. Like suppose we are capturing order for person, we can not store like person_id 1 have order for prodcuts [1,34,23,57]

5. Column sequence is not guaranteed. This is very important, SQL standard doesnt guarantee that the columns will be stored in same order as you defined them. Although MySql does store data similar to order used while creating table but again its not part of SQL standard.
    Example- Suppose you have table student with column name, address, attendance, it is not guareantee that data will be stored in same order, so while accessing data always use column name.

6. Row sequence is not guaranteed. SQL doesnt guarantee in which order rows will be returned on executing query. You need to explicitly use order by clause. Having said that MYSQl, return rows in order of their primary key but again its not part of SQL standard.

7. Name of every column should be unique

# Install MYSQL server (DBMS)

1. Install MySQL Server (DBMS Server)
Install Version 8.0 or higher
https://dev.mysql.com/downloads/mysql/


2. Install My SQL Workbench (UI Tool, Code Editor to execute SQL)
About MySQL Workbench
https://dev.mysql.com/downloads/workbench/


3. Set up Sakila Database (DOWNLOAD) 
https://downloads.mysql.com/docs/sakila-db.zip

Execute the sakila-schema.sql script to create the database structure, and execute the sakila-data.sql script to populate the database structure, by using MySQLWorkbench.

View the Database tables using MySQL Workbench.

