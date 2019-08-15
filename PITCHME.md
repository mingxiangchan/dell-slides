### Automated Testing: Spring

---

### Spring vs No Spring

- testing HTTP requests
- testing DB interactions

---

### Setup

- no setup needed! Spring Boot already comes wth JUnit 4 preinstalled.

---

### Data Layer Testing

- test DB repositories
- test services that use repositories

+++

### Repository Tests

```java
@RunWith(SpringRunner.class)
@DataJpaTest
@AutoConfigureTestDatabase(replace = Replace.NONE)
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

- Clone [this](https://github.com/mingxiangchan/dell-spring-junit) repository

+++

### EmployeeRepositoryTest

- test <span class="text-blue">findAll</span>
- test <span class="text-blue">findById</span>
- test <span class="text-blue">findByEmail</span>
- test <span class="text-blue">findByName</span>
- test <span class="text-blue">findAll/span> with <span class="text-blue">sorting</span>

+++

### AppointmentRepositoryTest

- test <span class="text-blue">findAll</span>
- test <span class="text-blue">findByTimeslotBetween</span>
    - happy
    - unhappy
- test <span class="text-blue">findByEmployeeEmailContains</span>

---

### Controller Tests

- test HTTP requests
- set request method (GET/POST)
- set request body (json)
- assert the response

+++

#### GET Tests

```java
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
public class MainControllerTest {
    @LocalServerPort
    private int port;

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    public void getHello() throws Exception {
        String url = new URL("http://localhost:" + port + "/").toString();

        ResponseEntity<String> response = restTemplate.getForEntity(url, String.class);

        assertEquals("Hello Controller", response.getBody());
    }
}
```

+++

#### POST Tests

```java
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
public class EmployeeControllerTest {
    @Test
    public void postHello() throws Exception {
        String url = new URL("http://localhost:" + port + "/employees").toString();

        Employee employee = new Employee();
        HttpHeaders headers = new HttpHeaders();
        HttpEntity<Employee> request = new HttpEntity<>(employee, headers);

        ResponseEntity<String> response = this.restTemplate.postForEntity(url, request, String.class);

        assertEquals(201, response.getStatusCode());
        assertEquals("[]", response.getBody());
    }
}
```

---

### Exercise

- Write tests for the EmployeeController
- Write tests for the AppointmentsController

+++


### EmployeeControllerTest

- test GET <span class="text-blue">/employees</span>
- test GET <span class="text-blue">/employees?email=<email></span>
- test GET <span class="text-blue">/employees/{id}</span>
- test POST <span class="text-blue">/employees</span>

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
spring.datasource.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
spring.datasource.url=jdbc:sqlserver://localhost;databaseName=<name>
spring.datasource.username=<name>
spring.datasource.password=<password>
```

+++

### Cleaning Up Database Before/After Tests

- not needed for repository/service tests (they are transactional)
- required for controller tests

+++

```java
@AfterEach
public void cleanDB() {
    userRepo.deleteAll();
    appointmentRepo.deleteAll()
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
