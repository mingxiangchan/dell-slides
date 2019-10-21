## Python 2

---

### Topics

-   Python classes
-   SQLAlchemy, Alembic
-   Flask Templates
-   Scripting in Python

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
        print(f"Hello, my name is {self.name}. I am {self.age} years old")
```

---

### Using classes

```python
# use constructor
user = User("John")
print(user.name)
user.greeting()
```

---

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

---

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

-   SQL Alchemy: ORM (e.g. Hibernate, JDBC)
-   Alembic: Migration tool (e.g. TypeORM, Flyaway)
-   Marshmallow: Serializing/Deserializing data (e.g. Hibernate)

---

### Installation

```bash
poetry add flask-sqlalchemy
poetry add marshmallow-sqlalchemy
poetry add flask-migrate
poetry add psycopg2
```

Remember to start your Postgresql server

```powershell
C:/Users/<YOUR_USERNAME>/scoop/apps/postgresql/current/bin/pg_ctl -D "C:\Users\<YOUR_USERNAME>\scoop\apps\postgresql\current\data" -l logfile start
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

---

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

---

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

---

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

---

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

### Request Processing Flow

1. Receive request (url, body, params)
2. Query the DB
3. Generate a response JSON from DB data -> `marshmallow`
4. Return response json

---

### Marshmallow: Schemas

```python
class UserSchema(ModelSchema):
    class Meta:
        model = User
```

---

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

---

`GET /users`

-   return a json array of users
-   each user should have:
    -   id
    -   email
    -   username

---

`GET /bookings/{id}`

-   return a single booking json for booking with the correct id

---

`POST /users`

-   will create a user in the DB

```json
{
    "email": email,
    "username": username
}
```

---

`POST /users/{id}`

-   will update a user with ID in the DB

```json
{
    "email": email,
    "username": username
}
```

---

`GET /bookings`

-   return a json array of bookings
-   each booking should have:
    -   id
    -   checkin_date
    -   checkout_date
    -   amount_payable
    -   confirmed (boolean)

---

`GET /bookings`

-   can search using query params (e.g. `?min_amount_payable=2000)
-   `min_amount_payable`
-   `max_amount_payable`
-   `confirmed`

---

`POST /users/{id}/bookings`

-   creates a booking that is linked to a user
-   add a foreign key relationship between user and booking
-   request body will contain
    -   checkin_date
    -   checkout_data
    -   amount_payable

---

### Scripting in Python

---

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

---

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
3. write the results into a `hw_results.csv` file

---

1. Download [this](https://people.sc.fsu.edu/~jburkardt/data/csv/cities.csv) csv of city data
2. check how many cities are there per state
3. write the results into a `cities_results.csv` file

---

## Assignment:

1. read [this](https://people.sc.fsu.edu/~jburkardt/data/csv/homes.csv) file
2. use the data to seed your database
3. create a flask webserver that allows you to query homes by attributes
4. write documentation about how to use the flask api
