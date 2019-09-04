
- class syntax
- sql alchemy
- alembic
- flask cookiecutter

## Python 2

+++

### Topics

- Python classes
- SQLAlchemy
- Alembic
- Flask Templates
- Scripting in Python

---

### Python Classes

```python
class User:
    # properties
    age = 15

    # constructor
    def __init__(self, name):
        self.name = name

    def greeting(self):
        print(f"Hello, my name is {name}. I am {age} years old")
```
+++

### Using classes

```python
# use constructor
user = User("John")
print(user.name)
user.greeting()
```

+++

### Inheritance

```python
class Admin(User):
    def login(self):
        print("You are logged in!")

# can inherit from multiple classes
class SuperAdmin(User, Admin):
    def drop_db(self):
        print("DB Dropped!")
```

---

## Exercise

+++

### Orange Tree

```python
tree = OrangeTree()

basket = []

while tree.age < 10:
    while tree.oranges > 0:
        orange = tree.pick_orange()
        basket.append(orange)
    
    tree.grow()

total_size = 0

for orange in basket:
    total_size += orange.size

print(f"The average size of the oranges on this tree is { total_size / length(basket) }")
```
---

### SQLAlchemy + Alembic

- SQL Alchemy: ORM (e.g. Hibernate, JDBC)
- Alembic: Migration tool (e.g. TypeORM, Flyaway)

+++

- add sqlalchemy + alembic to flask
- add some sample classes
- run some queries
- exercise: airbnb db, properties, bookings, reviews, users

---

### Flask Templates

- python is fragmented, pip, poetry, pipenv etc.
- application factory pattern to split up files

---

### Scripting Tools

- CSV parsing
- reading json files
- writing to a CSV file
- creating charts
- using CLIs

