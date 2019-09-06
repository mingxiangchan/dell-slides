## Python 2

+++

### Topics

- Python classes
- SQLAlchemy, Alembic
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

### Database-Webserver Libraries

- SQL Alchemy: ORM (e.g. Hibernate, JDBC)
- Alembic: Migration tool (e.g. TypeORM, Flyaway)
- Marshmallow: Serializing/Deserializing data (e.g. Hibernate)

+++

### Installation

```bash
poetry add flask-sqlalchemy
poetry add marshmallow-sqlalchemy
poetry add flask-migrate 
```

---

### SQLAlchemy: Setup

```python
from flask_sqlalchemy import SQLAlchemy

url = "postgres://localhost:5432/db_name"
app.config["SQLALCHEMY_DATABASE_URI"] = url
app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False
db = SQLAlchemy(app)
```

+++

### SQLAlchemy: Model

```python
from datetime import datetime

class User(db.Model):
    # column_name = db.Column(column_type, **options)
    id = db.Column(db.Integer, primary_key=True)
    email = db.Column(db.String(120), unique=True, nullable=False)
    description = db.Column(db.Text, nullable=True)
    created_at = db.Column(db.DateTime, nullable=False, default=datetime.utcnow)
```

+++

### SQLAlchemy: Querying

```python
# set the SELECT field
query = db.session.query(User)
query = User.query
query = db.session.query(User.id, User.email)

# add filters and ordering
query.filter_by(User.id==123).one()
query.filter_by(User.id.like('%John%')).all()
```

You can read more [here](https://docs.sqlalchemy.org/en/13/orm/tutorial.html#querying)

+++

### SQLAlchemy: CRUD

```python
# insert/update
user = User()
user.email = 'john@example.com'
user.age = 15

db.session.add(user)
db.session.commit()

# delete
db.session.delete(user)
```

---

### Alembic: Setup

```python
from flask_migrate import Migrate

db = SQLAlchemy(app)
migrate = Migrate(app, db)
```

+++

### Alembic: Commands

```bash
# initialize migration folder
flask db init

# generate a migration from models
flask db migrate

# run the pending migrations
flask db upgrade
```

---

### Marshmallow: Schemas

```python
class UserSchema(ModelSchema):
    class Meta:
        model = User
```

+++

### Mashmallow: Convert to JSON

```python
@app.route("/users")
def users():
    users = User.query.all()
    users_json = UserSchema(many=True).dump(users)
    return jsonify(users_json)
```

---

### Exercise

+++

<span class="text-blue">GET /users</span>

- return a json array of users
- each user should have:
    - id
    - email
    - username

+++

<span class="text-blue">GET /bookings/{id}</span>

- return a single booking json for booking with the correct id

+++

<span class="text-blue">POST /users</span>

- will create a user in the DB

```json
{
    "email": email,
    "username": username
}
```

+++

<span class="text-blue">POST /users/{id}</span>

- will update a user with ID in the DB

```json
{
    "email": email,
    "username": username
}
```

+++

<span class="text-blue">GET /bookings</span>

- return a json array of bookings
- each booking should have:
    - id
    - checkin_date
    - checkout_date
    - payment_amount
    - confirmed (boolean)

+++

<span class="text-blue">GET /bookings</span>

- can search using query params (e.g. <span class="text-blue">?min_payment_amount=2000)
- min_payment_amount
- max_payment_amount
- confirmed

---

### Scripting in Python

+++

### Reading CSV

```python
import csv

with open('employees.csv', mode='r') as csv_file:
    csv_reader = csv.DictReader(csv_file)
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            print(row)
        else:
            print(row["name"])
            print(row["id"])
        line_count+= 1
```

+++

### Writing CSV

```python
import csv

with open('employees_2.csv', mode='w') as csv_file:
    fieldnames = ['name', 'dept', 'birth_month']
    writer = csv.DictWriter(csv_file, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerow({'name': 'John Smith', 'dept': 'Accounting', 'birth_month': 'November'})
    writer.writerow({'name': 'Erica Meyers', 'dept': 'IT', 'birth_month': 'March'
```

---

### Exercise

1. Download [this](https://people.sc.fsu.edu/~jburkardt/data/csv/hw_200.csv) csv of height data
2. get the average height and weight of all participants
3. write the results into a <span class="text-blue">hw_results.csv</span> file

+++

1. Download [this](https://people.sc.fsu.edu/~jburkardt/data/csv/cities.csv) csv of city data
2. check how many cities are there per state
3. write the results into a <span class="text-blue">cities_results.csv</span> file
