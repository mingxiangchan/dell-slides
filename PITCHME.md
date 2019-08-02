### Deployment

---

### What is a live site?

- running on a server
- accessible on a public URL
- connected to live DB and other services

---

### Cloud Foundry

- a cloud provider
- provides servers running 24/7
- has public and on-premise options

+++

### Setup

Download CLI [here](https://github.com/cloudfoundry/cli#installers-and-compressed-binaries)

Sign up for a trial acc [here](https://account.run.pivotal.io/z/uaa/sign-up)

+++

### CLI Setup

Log In (once per computer)

```
# login to cloudfoundry
cf login -a api.run.pivotal.io

# logout
cf logout
```

---

### 1: Barebones App Deployment

+++

### Setup

1. Create a Spring App
2. Only 1 RestController with 1 Endpoint
3. No database

+++

manifest.yml

```
---yml
applications:
- name: app-name
```

pom.xml

```xml
<packaging>jar</packaging>
```

+++

Build JAR file

```
mvn clean install spring-boot:repackage
```

Push to Cloud Foundry

```bash
# upload code
cf push -p target/**.jar

# check uploaded apps
cf apps

# check app route
cf routes
```

+++

### Convenience

Update your manifest.yml

```yml
applications:
- name: next-cloud-test
  random-route: true
  path: target\demo-0.0.1-SNAPSHOT.jar 
```

---

### Cloud DB

- a database server running in the cloud
- not running on your computer

+++

- not using SQL server
- only on Microsoft Azure
- for Cloud Foundry, use Postgresql and Mysql

+++

### Provision DB

```bash
# view possible services
cf marketplace
cf marketplace -s <service-name>

# mysql
cf create-service cleardb spark <name>
# postgresql
cf create-service elephantsql turtle <name>

# view list of services
cf services

# can delete service
cf delete-service s<name>
```

+++

### Setup Postgresql Locally

```bash
scoop install postgresql@10.9

# start postgresql
pg_ctl -D "C:\Users\<your-windows-user>\scoop\apps\postgresql\current\data" -l logfile start

# intialize typeorm postgresql mode
typeorm init --name ProjectName --database postgres

# create a databse under postgresql
psql -c "CREATE DATABASE <db_name>" -U postgres
```

+++

### Setup

1. create TypeORM project for Postgresql
2. create a Book entity
    - id
    - title
    - numPages (col_name: "num_pages")
3. set username and password
    - username: postgres
    - username: postgres
4. generate and run migration

---

### Attach DB to Prod Application

- provision cloud service
- get url, username, password, db_name
- set credentials in spring app

+++

### Approach 1: manifest.yml

```yml
applications:
- name: next-cloud-test
  random-route: true
  path: target\demo-0.0.1-SNAPSHOT.jar 
  env:
    SPRING_DATABASE_URL: <url>
    SPRING_DATASOURCE_USERNAME: <username>
    SPRING_DATASOURCE_PASSWORD: <password>
```

+++

### Approach 2: application-prod.properties

```yml
# manifest.yml
applications:
- name: next-cloud-test
  random-route: true
  path: target\demo-0.0.1-SNAPSHOT.jar 
  env:
    SPRING_PROFILES_ACTIVE: prod
```

```
# application.properties
spring.datasource.url = <url>
spring.datasource.username = <username>
spring.datasource.password= = <username>
```

+++

### Cloud Auto-Reconfiguration

- cloud foundry automatically sets url, username, password
- avoid it, too much magic, very inflexible






