### Spring Session and Security

---

Recap:

1. render HTML
2. render JSON
3. query database using JDBC
4. query database using Spring Data/Hibernate

---

How do we differentiate logged in / non logged in users?

---

### HTTP Request structure

1. Header <- Auth Data Here
2. Body

+++

### Formats

1. client-side session
2. server-side session
3. client-side cookie
4. authorization header

+++

Usually the authorization format just stores an identifier string

1. user_id
2. generated token unique to the user

+++

We will be focusing on:

1. authorization header
2. generated token unique to the user (JWT format)

+++

### Why only JWT?

1. focus on building API endpoints
2. sessions/cookies not applicable

---

### Dependencies

Install `spring-boot-starter-security`

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-jwt</artifactId>
</dependency>
```

### Authorization Flow

```mermaid
```