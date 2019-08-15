### Automated Testing: Spring

---

### Spring vs No Spring

- testing HTTP requests
- testing DB interactions

---

### Setup

- exclude default junit (4.0)
- add junit 5.0

+++

#### pom.xml

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
    <exclusions>
        <exclusion>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.5.1</version>
</dependency>
```

---

### Data Layer Testing

- test DB repositories
- test services that use repositories

+++

### Repository Tests

```java
@SpringBootTest
public class UserServiceTest {

    @Autowired
    UserRepository userRepository;

    @Test
    void testFindUser() {
        // Given
        User seededUser = new User("John");
        userRepository.save(seededUser);

        // When
        User user = userRepository.findById(seededUser.getId());

        // Then
        assertEquals("John", user.getName());
    }
}
```

---

### Exercise

- Clone [this] repository
- Write tests for the BookingRepository
- Write tests for the ReviewRepository

---

### Controller Tests

- test HTTP requests
- set request method (GET/POST)
- set request body (json)
- assert the response

+++

```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
public class MainControllerTest {
    @LocalServerPort
    private int port;

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    public void getHello() throws Exception {
        String url = new URL("http://localhost:" + port + "/").toString()

        ResponseEntity<String> response = restTemplate.getForEntity(url, String.class);

        assertEquals("Hello Controller", response.getBody());
    }
}
```

---

### Exercise

- Clone [this] repository
- Write tests for the BookingRepository
- Write tests for the ReviewRepository

---

### Configuring Test DB in Spring

- use a different DB when running tests
- clean up the DB at the end of every test

---

```java
@ActiveProfiles("test")
@SpringBootTest
public class UserRepositoryTest {
    // ...
}
```

```yml
# application-test.properties
# set db url
# set db username
# set db password
```

+++

```java
class DatabaseCleaner {
    
}
```

---

### Types of Tests

- unit
- integration
- feature

+++

### Cost vs Benefit

- Integration tests have most value
- Integration tests are hardest to set up
- 

---

### Example: Grab Order Cancellation

- customer cancelling an order
- test how much is the cancellation fee

+++

### Integration Test Setup

- service
- customer
- driver
- customer's order
- discovery sent to driver
- driver confirmation for order

+++

### Unit Test Setup

- only set up customer's order
- setup 
