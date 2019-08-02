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

Split application.properties so local and prod are separated

```yml
# application.properties
spring.datasource.driverClassName=org.postgresql.Driver
spring.datasource.url = jdbc:postgresql://localhost:5432/book_db
spring.datasource.username = postgres
spring.datasource.password= = postgres
```

```yml
# application-prod.properties
spring.datasource.url = <url>
spring.datasource.username = <username>
spring.datasource.password= = <username>
```

+++

### Cloud Auto-Reconfiguration

- cloud foundry automatically sets url, username, password
- avoid it, too much magic, very inflexible

---

### application.properties

- global key value store
- can use to store configs for different environents
    - dev
    - staging
    - prod
    - test

+++

### application.properties Hierarchy

- application.properties
- application-{profile}.properties
- direct override from env, e.g. `SPRING_PROFILES_ACTIVE`
- [list of commonly used properties](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)

+++

Can reuse previously defined properties

```
haha.hehe = abc
hoho.hehe = ${haha.hehe}def

// hoho.hehe => abcdef
```

+++

Can use directly in Java code

```java
@Value("${help.me.message}")
public String message;

public void setup() {
	System.out.println(message)
}
```

+++

### Exercise

- create a messages in your properties
- display a different JSON message in dev and prod
    - dev: Hello Me
    - prod: Hello World
- set a ENV directly in `manifest.yml` and override
    - Hello Everyone

---

### Spring Profiles

- default profile is <span style="text-blue">default</span>
- can set profile using <span style="text-blue">spring.profiles.active</span>
- can set multiple profile

+++

### Using Profiles

The below code is only loaded in the <span style="text-blue">dev</span> profile

```java
@Component
@Profile("dev")
public class DevDatasourceConfig implements DatasourceConfig {
    public String paypalAccNo = "123";
		public String paypalAccPw = "456";
		public String paypalEndpoint = "https://sandbox.paypal.com";
}
```

+++

### Shared interface

```java
public interface DatasourceConfig {
    public String paypalAccNo;
		public String paypalAccPw;
		public String paypalEndpoint;
}
```

+++

### Prod vs Dev Classes

```java
@Component
@Profile("dev")
public class DevDatasourceConfig implements DatasourceConfig {
    public String paypalAccNo = "123";
		public String paypalAccPw = "456";
		public String paypalEndpoint = "https://sandbox.paypal.com";
}

@Component
@Profile("prod")
public class ProductionDatasourceConfig implements DatasourceConfig {
    public String paypalAccNo = "887123213";
		public String paypalAccPw = "7das712ekj";
		public String paypalEndpoint = "https://api.paypal.com";
}

```

+++

### Use via Autowired

```java
@Service
public class PaypalService {
	@Autowired
	private DatasourceConfig config;

	public void makePayment() {
    System.out.println(config.paypalAccNo)
		System.out.println(config.paypalAccPw )
		System.out.println(config.paypalEndpoint )
	}
}
```

+++

### Exercise

- Create a <span style="text-blue">DataConfig</span> interface
    - maybank_acc_no: string
    - maybank_acc_pw: string
- Create a <span style="text-blue">DevDataConfig</span>
    - fill in the values
- Create a <span style="text-blue">ProdDataConfig</span>
    - fill in the values

---

### Use ENV variables

- best practice
- use ENV variables for sensitive info
- set from dashboard/CLI
- can also set in <span style="text-blue">manifest.yml</span>

+++

```java
@Component
@Profile("prod")
public class ProductionDatasourceConfig implements DatasourceConfig {
    public String paypalAccNo = System.getenv("PAYAL_ACC_NO");
	public String paypalAccPw = System.getenv("PAYAL_ACC_PW");
	public String paypalEndpoint = "https://api.paypal.com";
}
```

+++

### Exercise

- use <span style="text-blue">System.getenv</span> in controller to change endpoint output
- use <span style="text-blue">System.getenv</span> in production config to change config setup



