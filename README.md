# Database-SQL
This repo covers Introduction to DB, keys, CRUD, Joins, aggregator queries, subqueries, indexing, Transactions and Schema design

## What is a Database

Okay, tell me, In your day to day life whenever you have a need to save some information, where do you save it? Especially when you may need to refer to it later, maybe something like your expenses for the month, or your todo or shopping list?

Correct! Many of us use softwares like Excel, Google Sheets, Notion, Notes app etc to keep a track of things that are important for us and we may need to refer to it in future. Everyone, be it humans or organizations, have need to store a lot of data that me useful for them later. Example, let's think about Jigisa. At Jigisa, we would want to keep track of all of your's attendance, assignments solved, codes written, psp etc! We would also need to store details about instructors, mentors, batches, etc. And not to forget all of your's email, phone number, password. Now, where will we do this?

For now, forget that you know anything about databases. Imagine yourself to be a new programmer who just knows how to write code in a programming language. Where will you store data so that you are able to retrieve it later and process that?

Correct! You will store it in files. You will write code to read data from files, and write data to files. And you will write code to process that data. For example you may create separate CSV (comma separated values, you will understand as we proceed) files to store information about let's say students, instructors, batches. Eg:

```
students.csv
name, batch, psp, attendance, coins, rank
Pradip, 1, 94, 100, 0, 1
Amit, 2, 81, 70, 400, 1
Pravin, 1, 31, 100, 100, 2
```

```instructors.csv
name, subjects, average_rating
Rachit, C++, 4.5
Rishabh, Java, 4.8
Aayush, C++, 4.9
```

```batches.csv
id, name, start_date, end_date
1, AUG 22 Intermediate, 2022-08-01, 2023-08-01
2, AUG 22 Beginner, 2022-08-01, 2023-08-01
```

Now, let's say you want to find out the average attendance of students in each batch. How will you do that? You will have to write code to read data from students.csv, and batches.csv, and then process it to find out the average attendance of students in each batch. Right? Do you think this will be very cumbersome?


# Issues with Files as a Database

1. Inefficient

Let's think of large scale data like suppose we have 2M+ users in our system. Imagine going through a file with 2M lines, reading each line, processing it to find your relevant information. Even a very simple task like finding the psp of a student named Pradip will require you to open the file, read each line, check if the name is Pradip, and then return the psp. Time complexity wise, this is O(N) and very slow.

2. Integrity

Is there anyone stopping you from putting a new line in `students.csv` as ```Pradip, 1, Hello, 100, 0, 1``` . If you see that `Hello` that is unexpected. The psp can't be a string. But there is no one to validate and this can lead to very bad situations. This is known as data integrity issue, where the data is not as expected.

3. Concurrency

Later in the course, you will learn about multi-threading and multi-processing. It is possible for more than 1 people to query about the same data at the same time. Similarly, 2 people may update the same data at the same time. On save, whose version should you save? Imagine you give same Google Doc to 2 people and both make changes on the same line and send to you. Whose version will you consider to be correct? This is known as concurrency issue.

4. Security

Earlier we talked about storing password of users. Imagine them being stored on files. Anyone who has access to the file can see the password of all users. Also anyone who has access to the file can update it as well. THere is no authorization at user level. Eg: a particular person may be only allowed to read, not write. '

# What is Databae
A database is nothing but collection of related data like in Jigisa we have a Database that stores information about our students, users, batches, classes, instructors, and everything else.Similarly, Facebook will have a database that stores information about all of it's users, their posts, comments, likes, etc. The above way of storing data into files was also nothing but a database, though not the easiest one to use and with a lot of issues.

# What is DBMS
A DBMS as the name suggests is a software system that allows to efficiently manage a database. A DBMS allows us to create, retrieve, update, and delete data (often also called CRUD operations). It also allows to define rules to ensure data integrity, security, and concurrency. It also provides ways to query the data in the database efficiently. Eg: find all students with psp > 50, find all students in batch 1, find all students with rank 1 in their batch, etc. There are many database management systems, each with their tradeoffs. 

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

# Keys
Key is unique identifier for each row in table.

1. super keys - Any column or combination of columns will help to uniquely identify each row of table is super key.

2. candidate keys - It is a super key from which no column can be removed and it still have proerty to uniquely identify row in table. Candidate key is subsetof super key.
    Example- we have table student with column student_id, batch_id, attendance. Now student_id and batch_id combination is superkey as well as candidate key but student_id, batch_id and attendance combination is only super key but not candidate key as we can remove attendance from combination.

3. primary key - Table is sorted according to primary key, display/query table also sorted according to primary key. Database create index by default upon primary key (index is data structure for faster searching in table)
    Properties of Primary key 
        - should be fast to sort on example in student table roll number will be faster than email
        - have smaller size (index will have smaller size too)
        - should not change, example email might change later.
    Because of above reasons every table need 1 key to be used as primary key. a primary key is candidate key that is chosen to be key for that table.

4. composit keys - Its general term, any key which is having more than one column is composit key. All keys like super key, candidate key, primary key and foreign key formed with 2 columns is composit key as well.

5. foreign key - Now let's get to the last topic of the day. Which is foreign keys. Let's say we have a table called batches which stores information about batchesat Scaler. It has columns (id, name, startDate, endDate). We would want to know for every student, which batch do they belong to. How can we do that?

Correct, We can add batchId column in students table. But how do we know which batch a student belongs to? How do we ensure that the batchId we are storing in the students table is a valid batchId? What if someone puts the value in batchID column as 4 but there is no batch with id 4 in batches table. We can set such kind of constraints using foreign keys. A foreign key is a column in a table that references a column in another table. It has nothing to do with primary, candidate, super keys. It can be any column in 1 table that refers to any column in other table. In our case, batchId is a foreign key in the students table that references the id column in the batches table. This ensures that the batchId we are storing in the students table is a valid batchId. If we try to insert any value in the batchID column of students table that isn't present in id column of batches table, it will fail. ANother example:

Let's say we have `years` table as:
`| id | year | number_of_days |`

and we have a table students as:
`| id | name | year |`

Is `year` column in students table a foreign key? 

The correct answer is yes. It is a foreign key that references the id column in years table. Again, foreign key has nothing to do with primary key, candidate key etc. It is just any column on one side that references another column on other side. Though often it doesn't make sense to have that and you just keep primary key of the other table as the foreign key. If not a primary key, it should be a column with unique constraint. Else, there will be ambiguities.

Okay, now let's think of what can go wrong with foreign keys?

Correct, let's say we have students and batches tables as follows:

| batch_id | batch_name |
|----------|------------|
| 1        | Batch A    |
| 2        | Batch B    |
| 3        | Batch C    |


| student_id | first_name | last_name | batch_id |
|------------|------------|-----------|----------|
| 1          | John       | Doe       | 1        |
| 2          | Jane       | Doe       | 1        |
| 3          | Jim        | Brown     | 2        |
| 4          | Jenny      | Smith     | 3        |
| 5          | Jack       | Johnson   | 2        |

Now let's say we delete the row with batch_id 2 from batches table. What will happen? Yes, the students Jim and Jack will be orphaned. They will be in the students table but there will be no batch with id 2. This is called orphaning. This is one of the problems with foreign keys. Another problem is that if we update the batch_id of a batch in batches table, it will not be updated in students table. Eg: If we update the batch_id of Batch A from 1 to 4, the students John and Jane will still have batch_id as 1. This is called inconsistency.

To fix for these, MySQL allows you to set ON DELETE constraints so that cascading deletes happen when such a delete happens.  


