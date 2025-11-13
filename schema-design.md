#  Database Schema Design 

Understanding how **tables in a database are connected** is the foundation of good schema design.  
Relationships tell **how many records in one table are related to records in another table.**

---

##  1. One-to-One (1:1) Relationship

###  Definition
A **1:1 relationship** means **one record in Table A** is related to **only one record in Table B**, and **vice versa**.

> Each row in both tables matches exactly one row in the other table.

---

###  Example
**Tables:** `User` and `UserProfile`

| User | UserID | Name  |
|------|---------|-------|
| 1    | John    |
| 2    | Riya    |

| UserProfile | ProfileID | UserID | Address     |
|--------------|------------|--------|--------------|
| 1            | 1          | Pune   |
| 2            | 2          | Mumbai |

 Each user has **exactly one profile**.  
If we delete a user, their profile should also be deleted.

---

###  When to Use
- To **split sensitive or optional data** into a separate table.
- Example: Storing user login details (passwords) separately from personal info.

---

##  2. One-to-Many (1:M) or Many-to-One (M:1) Relationship

###  Definition
A **1:M relationship** means **one record in Table A** can relate to **many records in Table B**,  
but each record in Table B relates to **only one record in Table A**.

> “One parent, many children.”

---

###  Example
**Tables:** `Customer` and `Order`

| Customer | CustomerID | Name  |
|-----------|-------------|-------|
| 1         | Rahul       |
| 2         | Meena       |

| Order | OrderID | CustomerID | Amount |
|--------|-----------|-------------|---------|
| 1      | 1         | 5000        |
| 2      | 1         | 1200        |
| 3      | 2         | 900         |

 One customer can have many orders.  
But each order belongs to **only one customer**.

---

###  When to Use
- For **parent-child** relationships.
- Example: 
  - A **teacher** can teach many **students**.  
  - A **department** has many **employees**.

---

##  3. Many-to-Many (M:M) Relationship

###  Definition
A **M:M relationship** means **many records in Table A** relate to **many records in Table B**.

> “Many parents, many children.”  
> To make this work in databases, we create a **junction (bridge) table** between them.

---

###  Example
**Tables:** `Student`, `Course`, and `StudentCourse`

| Student | StudentID | Name   |
|----------|------------|--------|
| 1        | Amit       |
| 2        | Priya      |

| Course | CourseID | Title         |
|---------|-----------|----------------|
| 1       | Math       |
| 2       | Science    |

| StudentCourse (Bridge Table) | StudentID | CourseID |
|-------------------------------|------------|-----------|
| 1                             | 1          |
| 1                             | 2          |
| 2                             | 2          |

 A student can enroll in **many courses**,  
and a course can have **many students**.

---

###  When to Use
- When both sides can have **multiple connections**.
- Example:
  - **Authors and Books**
  - **Movies and Actors**
  - **Students and Subjects**

---

##  Summary Table

| Relationship | Description | Example | Implementation Tip |
|---------------|--------------|----------|----------------------|
| 1:1 | One record ↔ One record | User ↔ Profile | Use unique foreign key |
| 1:M / M:1 | One record ↔ Many records | Customer ↔ Orders | Add foreign key in child table |
| M:M | Many records ↔ Many records | Student ↔ Courses | Use a bridge (junction) table |

---

##  Schema Design Tips

- Always identify the **"one"** and **"many"** sides early.
- Use **foreign keys** to enforce relationships.
- Use **ON DELETE CASCADE** if deleting parent should delete children.
- Normalize data but don’t overdo it — balance **performance** and **clarity**.

---

 **Real-world analogy:**
| Real-world Scenario | Relationship Type | Example |
|----------------------|-------------------|----------|
| Person & Passport | 1:1 | Each person has exactly one passport |
| Company & Employees | 1:M | One company has many employees |
| Students & Subjects | M:M | Many students can take many subjects |


