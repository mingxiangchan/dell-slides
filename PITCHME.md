### Java Web Apps

---

### How the Web Works

- browser sends request to server
- server checks data in DB
- server sends response to browser

+++

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server
    participant D as Database


    C->>S: GET /users
    S->>D: SELECT * FROM users
    D-->>S: user rows
    S-->>C: HTML/JSON data
```

---

### Spring Framework

- Framework for building apps in Java
- Powerful ecosystem with many extensions/libraries

+++

### Why use a Framework

- follow established conventions
- reusue existing code
- speed up development

+++

### Example
- receive request/send response using Spring Web
- connect to SQL Server using SQL Server Adapter
- interface with database using JDBC/Hibernate
- generate HTML using Thymeleaf
- interface with third party services via SDKs, e.g. Paypal

---

### Exercise: Nextagram V1

- HTML -> homepage displaying all images
- JSON -> list of users
- JSON -> list of images for a user
- no database, all data is hardcoded

---

### Phase 1: Homepage

- initialize in Spring Tools Suite
- hardcode images data 
- create GET endpoint returning HTML
- create HTML template for homepage

+++

### Initialization

- Spring Web
- Spring Dev Tools
- ThymeleafT

+++

### Harcode Images Data

- create `Image` class
- properties: `id`, `url`
- hardcode 12 images

+++

### GET endpoint

- create controller
- add required annotations
- import hardcoded images

+++

```java
```

+++

### HTML Template

- create .html file
- add mappings in controller
- use mappings in html file

---

### Phase 2: JSON -> List of users

- hardcode users data 
- create GET endpoint returning JSON
- process users data into JSON

---

### Phase 3: JSON -> List of images for a user

- hardcode users -> images data
- create GET endpoint returning JSON
- process user ID to get correct list of images