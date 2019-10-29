---
marp: true
---

# Database: One Table Vs Multi Table

---

[Unorganized Laptop Sales](https://docs.google.com/spreadsheets/d/1aoycRdgvbkgsxfIKDVdU8w1ZaSwz4zs8MAzh8UYR4HI/edit#gid=0)
[Laptop Sales](https://docs.google.com/spreadsheets/d/1H7Q4gxrL4lqf_nU2DjzA6xJkz4biUEer8dK0Imm1XfQ/edit#gid=1408105866)

---

# One Table

-   Redundant
-   Conflicting
-   Difficult to update

---

# Separated Table

-   Easy to update
-   Not redundant/ conflicting

---

## Separated tables are connected via primary key and foreign key pairs, which denote the relationship

---

-   Primary Key is
    -   a unique identifier for a record in a table
    -   cannot be null
    -   only one in table
-   Foreign Key is
    -   a primary key on another table (serves as the reference that denotes relationships between entities)
    -   can be null
    -   can have multiple in a table

---

# Entity Relationships

[Lesson](https://school.nextacademy.com/courses/backend-web-development-java/lessons/3284)

---

# Entity Relationship Diagrams & Schemas

-   Demo: Quora
    [dbdiagram](https://dbdiagram.io/d)

---

# Database Actions: CRUD

-   Create
-   Read
-   Update
-   Delete

---

# Structured Query Language (SQL)

-   is a language specifically used to interact with databases, or more specific, relational databases

---

# Beginner Exercises:

-   [Music DB](https://next-sql.netlify.com/pages/intro/comparators/)
-   [SQLZoo](https://sqlzoo.net/)
    -   Complete from _0 Select basics_ to _7 More Join Operators_
    -   The remainder are optional, but good to learn

# Advanced Exercises:

-   [Congress Poll]()

---

## Keyword Hierarchy

-   SELECT
-   FROM
-   JOIN ... ON
-   WHERE
-   GROUP BY
-   HAVING
-   ORDER BY

*   Have to follow this exact order

---

## SELECT

-   specifies the column names in the final result

```sql
SELECT id, name, email
FROM users
```

## FROM

-   specifies source of the data

```sql
SELECT id, name, email
FROM users
```

---

## JOIN ... ON

-   joins multiple data sources based on a criteria
-   refer to different data source by table name

```sql
SELECT users.id, users.name, permissions.name
FROM users
JOIN permissions ON users.id = permissions.user_id
```

---

## WHERE

-   filters data according to condition
-   can add `ON` or `AND`
-   can check equality etc.

```sql
SELECT id, name, email
FROM users
WHERE email LIKE '%gmail%'
```

---

## GROUP BY

-   aggregrates rows into grouped rows based on condition

```sql
SELECT role, COUNT(*)
FROM users
GROUP BY role
```

---

## HAVING

-   WHERE filter but on the grouped conditions
-   can only be used together with GROUP BY
-   e.g. filter by sum of rows

```sql
SELECT role, COUNT(*)
FROM users
GROUP BY role
HAVING email LIKE '%gmail%'
```

---

## ORDER BY

-   sort the final data in a particular order

```sql
SELECT id, name, email
FROM users
ORDER BY name
```

---

## Complex JOINS

Default JOIN is INNER JOIN

---

## LEFT JOIN

-   allow right side to be NULL

| `users.name` | `users.country_id` | `country.id` | `country.name` |
| ------------ | ------------------ | ------------ | -------------- |
| Ming Xiang   | 1                  | 1            | Malaysia       |
| John         | 5                  |              |                |
| Jane         | 6                  |              |                |

---

## RIGHT JOIN

-   allow left side to be NULL

| `users.name` | `users.country_id` | `country.id` | `country.name` |
| ------------ | ------------------ | ------------ | -------------- |
| Ming Xiang   | 1                  | 1            | Malaysia       |
|              |                    | 2            | America        |
|              |                    | 3            | Japan          |

---

## FULL OUTER JOIN

-   allow either side to be null

| `users.name` | `users.country_id` | `country.id` | `country.name` |
| ------------ | ------------------ | ------------ | -------------- |
| Ming Xiang   | 1                  | 1            | Malaysia       |
|              |                    | 2            | America        |
| John         | 5                  |              |                |

---

## JOIN Exercises

---

### Employee Table

| id  | name     | department_id |
| --- | -------- | ------------- |
| 1   | John     | 1             |
| 2   | Jane     | 2             |
| 3   | Kevin    | 3             |
| 4   | Nicholas | 5             |
| 5   | Lily     | 2             |
| 6   | Riley    | 1             |

---

### Department Table

| id  | name          | manager_id |
| --- | ------------- | ---------- |
| 1   | Finance       | 1          |
| 2   | Manufacturing | 2          |
| 3   | Sales         | 3          |

---

# Demo: Using SQL Server

-   Database Management
-   Record Management (INSERT, DELETE, UPDATE)

---

# TypeORM with Multiple Tables

-   Quora Demo

---

#### One To One

```js
@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number
}
```

```js
@Entity()
export class UserProfile {
    @PrimaryGeneratedColumn()
    id: number

    @OneToOne(type => User)
    @JoinColumn({ name: 'user_id' })
    user: User
}
```

---

#### One To Many, Many To One

```js
@Entity()
export class Author {
    @PrimaryGeneratedColumn()
    id: number

    @OneToMany(type => Book, book => book.author)
    books: Book[]
}
```

---

```js
@Entity()
export class Book {
    @PrimaryGeneratedColumn()
    id: number

    @ManyToOne(type => Author, author => author.books)
    @JoinColumn({ name: 'author_id' })
    author: Author
}
```

---

#### Many to Many

```js
@Entity()
export class Employee {
    @PrimaryGeneratedColumn()
    id: number

    @ManyToMany(type => Project, project => project.employees)
    projects: Project[]
}
```

---

```js
@Entity()
export class Project {
    @PrimaryGeneratedColumn()
    id: number

    @ManyToMany(type => Employee, employee => employee.projects)
    @JoinTable({
        name: 'employees_projects',
        joinColumns: [{ name: 'project_id' }],
        inverseJoinColumns: [{ name: 'employee_id' }],
    })
    employees: Employee[]
}
```

---

# Exercise: Project Management

-   Company has many Employees
-   Employee has many Projects
-   Project has many Employees

---

# Assignment: AirBnB

---

#### Phase 1

-   User has many Bookings
-   Property has many Bookings
-   Owner has many properties

---

### Fields

```
User: id, name, email,contact_no, created_at, updated_at
Booking: id, property_id, price, booking_date, user_id, check_in, check_out,created_at, updated_at
Property: id, address,owner_id, created_at, updated_at
Owner: id, name, email, contact_no, created_at, updated_at
```

---

#### Phase 2

-   One booking can have many payments
-   Many properties can have many tags

---

### Fields

```
Payments: id,status, amount, booking_id
Tags: id, label
```

---

#### Phase 3

-   Include
    -   Reviews on Property with Ratings
    -   Comments made by Users on Review
    -   Locality of Property
-   You decide the fields
