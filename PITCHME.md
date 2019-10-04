---
marp: true
---

## SQL

- Structured Query Language
- a language for dealing with relational databases

---

## CRUD

- Create
- Read
- Update
- Delete

---

## Keyword Hierarchy

- SELECT
- FROM
- JOIN  ... ON
- WHERE
- GROUP BY
- HAVING
- ORDER BY

---

Have to follow this exact order

---

## SELECT

- specifies the column names in the final result

```sql
SELECT id, name, email
FROM users
```

---

## FROM

- specifies source of the data

```sql
SELECT id, name, email
FROM users
```

---

## JOIN ... ON

- joins multiple data sources based on a criteria
- refer to different data source by table name

```sql
SELECT users.id, users.name, permissions.name
FROM users
JOIN permissions ON users.id = permissions.user_id
```

---

## WHERE

- filters data according to condition
- can add `ON` or `AND`
- can check equality etc.

```sql
SELECT id, name, email
FROM users
WHERE email LIKE '%gmail%'
```

---

## GROUP BY

- aggregrates rows into grouped rows based on condition

```sql
SELECT role, COUNT(*) 
FROM users
GROUP BY role
```

---

## HAVING

- WHERE filter but on the grouped conditions
- can only be used together with GROUP BY
- e.g. filter by sum of rows

```sql
SELECT role, COUNT(*) 
FROM users
GROUP BY role
HAVING email LIKE '%gmail%'
```

---

## ORDER BY

- sort the final data in a particular order

```sql
SELECT id, name, email
FROM users
ORDER BY name
```

---

## Complex JOINS

---

Default JOIN is INNER JOIN

---

## LEFT JOIN

- allow right side to be NULL

---


## LEFT JOIN

| `users.name` | `users.country_id` | `country.id` | `country.name` |
|--------------|--------------------|--------------|----------------|
| Ming Xiang   | 1                  | 1            | Malaysia       |
| John         | 5                  |              |                |
| Jane         | 6                  |              |                |
---

## RIGHT JOIN

- allow left side to be NULL

---

## RIGHT JOIN

| `users.name` | `users.country_id` | `country.id` | `country.name` |
|--------------|--------------------|--------------|----------------|
| Ming Xiang   | 1                  | 1            | Malaysia       |
|              |                    | 2            | America        |
|              |                    | 3            | Japan          |
---

## FULL OUTER JOIN

- allow either side to be null

---

## FULL OUTER JOIN


| `users.name` | `users.country_id` | `country.id` | `country.name` |
|--------------|--------------------|--------------|----------------|
| Ming Xiang   | 1                  | 1            | Malaysia       |
|              |                    | 2            | America        |
| John         | 5                  |              |                |


---

## JOIN Exercises

---

### Employee Table

| id | name     | department_id |
|----|----------|---------------|
| 1  | John     | 1             |
| 2  | Jane     | 2             |
| 3  | Kevin    | 3             |
| 4  | Nicholas | 5             |
| 5  | Lily     | 2             |
| 6  | Riley    | 1             |

---

### Department Table

| id | name          | manager_id |
|----|---------------|------------|
| 1  | Finance       | 1          |
| 2  | Manufacturing | 2          |
| 3  | Sales         | 3          |

---

## Exercises

- `JOIN ON employee.department_id = department.id`
- `JOIN ON department.manager_id = employee.id`
- `LEFT JOIN ON employee.department_id = department.id`

---

# Many To Many Exercise

---

## Exercise

- teachers
    - id, name
- students
    - id, name
- teachers_students
    - teacher_id
    - student_id

---

1. Create 3 teachers, John, Jane, Ken
2. Create 3 students, Ryan, Chris, Kelly
3. Kelly's teachers: John, Jane
4. Ryan's teachers: John, Ken
5. Chris' teachers: Jane, Ken
