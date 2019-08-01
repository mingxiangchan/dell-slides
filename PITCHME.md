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

```
cf push -p target/**.jar




