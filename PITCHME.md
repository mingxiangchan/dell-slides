## Express 2: Database

---

### How to store information persistently?
- Text File
- Tables (Excel/ Google Sheet)
- Databases

+++

### Database Basics
- Database is an **organized collection** of data
- i.e: Data stored in a specific structure, commonly in the form of `Columns/Field` and `Rows/Records`
- Database become more organized and versatile when you include relationships

---

### DB Setup
- Setting up Postgresql Locally
```bash
scoop install postgresql@10.9
 
# start postgresql
pg_ctl -D "C:\Users\<your-windows-user>\scoop\apps\postgresql\current\data" -l logfile start

# create a databse under postgresql
psql -c "CREATE DATABASE <db_name>" -U postgres
```

+++

It's possible to use direct SQL queries to create and alter tables, but we usually migration managers to handle it.

---

### Exercise: dbdiagram.io
- Bitly: Urls
- Quora: Questions
- [PropertyGuru](https://www.propertyguru.com.my): Property

---

## Object Relational Mapping: Type ORM

+++

<img src="https://kroki.io/mermaid/svg/eNpNjksOgkAQRPeeonauuAALFobExISoxAsMQ4NjhMHuHom3d5jgp7f9XlUJPQKNlkpnejbDBvEO5mnEsps0K4rLa6JjXeXYk6I1atCxH9A2CV2_iCBOXrRnkhznQOxIUO7QeQb7OZnJ-FDIFuebXplJFnArsP4ehlGgHr65kVUYVXZNUJL_0iXgNzVHTRo4eqs0O73Gman5DSCoTLU=">
---

### Migration Management

+++

#### Migrations are changes to your database that are:
- Incremental
- Reversible
- Separate

+++

#### Setup
```bash
# installs typeorm commands
npm install -g typeorm
# initializes a typeorm project with postgres db
typeorm init --name ProjectName --database postgres
```

---

#### Entities

+++

```js
import { Entity, PrimaryGeneratedColumn, Column } from "typeorm";

@Entity()
export class User {

    @PrimaryGeneratedColumn()
    id: number

    @Column()
    name: string

    @Column("datetime")
    created_at
}
```

+++

### TypeORM Commands
```bash
# Generate Migration
ts-node ./node_modules/typeorm/cli.js migration:generate -n MigrationFileName
# Execute Migrations
ts-node ./node_modules/typeorm/cli.js migration:run
# Revert Migrations
ts-node ./node_modules/typeorm/cli.js migration:revert
```

---

### Exercise
- Generate the following tables in postgres database using typeorm
    - Urls
    - Questions
    - Properties

--- 

### Accessing DB in Express
- Read and find the differences
```
typeorm init --name MyProject --database postgres --express
```

+++

### Exercises
- Bitly
    - GET /urls
    - GET /urls/1
    - GET /urls/1/redirect
    - POST /urls
    - POST /urls/1
    - DELETE /urls/1

+++

- Quora
    - GET /questions
    - GET /questions/1
    - POST /questions
    - POST /questions/1
    - DELETE /questions

+++

- Properties
    - GET /properties
    - GET /properties/1
    - POST /properties
    - POST /properties/1
    - DELETE /properties

+++

### Separate each entity to different apps

---

## Deployment: Part 2

---

### Cloud DB
- a database running on the cloud
- not on your computer

+++

### Provision DB
On heroku dashboard
- Go to your app
- Select Resources tab
- In search bar, type `Heroku Postgres` and add to your app
- Settings, click `Reveal Config Vars`
- You will see a DATABASE_URL

+++

### Attach DB to Prod Application
- provision cloud service
- get url, username, password, db_name
- set credentials in ormconfig

+++

### How
From the DATABASE_URL, get the credentials and replace in your ormconfig
`username:password@host:port/databasename`
```json
{
   "host": host,
   "port": port,
   "username": username,
   "password": password,
   "database": databasename,
   "entities": [
      "build/entity/**{.ts,.js}"
   ],
   "migrations": [
      "build/migration/**{.ts,.js}"
   ],
   ...
}
```

+++

### Ensure
1. use `const PORT = process.env.PORT || 3000`
2. have a Procfile
3. add to package.json
   ```json 
    "scripts": {
      "build-ts": "tsc",
      "postinstall": "npm run build-ts",
      "start": "ts-node src/index.ts"
    }
   ```

+++

## Exercise
Deploy your Bitly, Quora and PropertyGuru clones.
---




