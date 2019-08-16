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
- test <span class="text-blue">findAll</span> with <span class="text-blue">sorting</span>

+++

### AppointmentRepositoryTest

- test <span class="text-blue">findAll</span>
- test <span class="text-blue">findByTimeslotBetween</span>
- test <span class="text-blue">findByEmployeeEmailContains</span>

---

### Services

- intermediary between <span class="text-blue">controller</span> and <span class="text-blue">repository</span>
- can do more complex logic
- can interact with multiple repositories

+++

```java
@Service
public class BookingService {
    @Autowired
    EmployeeRepository employeeRepo;

    @Autowired
    AppointmentRepository appointmentRepo;
}
```

---

### Exercise: BookingService

<span class="text-blue">checkAppointment(Employee employee)</span>
- get all appointments for a user
- go through each appointment and get the timeslot, extract into array
- return `List<LocalDateTime>` 

+++

### Exercise: BookingService

<span class="text-blue">bookAppointment(timeslot, employee)</span>
- 1 timeslot is 2 hours
- check whether intended timeslot [conflicts with an existing appointment](https://stackoverflow.com/questions/46942351/checking-if-localdatetime-falls-within-a-time-range)
- if success, save appointment into DB
- if failure, return <span class="text-blue">null</span>


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
        employee.setName("John");
        employee.setEmail("john@gmail.com");
        HttpHeaders headers = new HttpHeaders();
        HttpEntity<Employee> request = new HttpEntity<>(employee, headers);

        ResponseEntity<String> response = this.restTemplate.postForEntity(url, request, String.class);
        String responseBody = response.getBody()
        Employee createdEmployee = new ObjectMapper().readValue(responseBody, Employee.class);

        assertEquals(201, response.getStatusCode());
        assertEquals("John", createdEmployee.getName());
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

+++

### AppointmentsController

- test GET <span class="text-blue">/appointments</span>
- test GET <span class="text-blue">/employees/{id}/appointments</span>
- test GET <span class="text-blue">/appointments/{id}</span>
- test POST <span class="text-blue">/appointments</span>

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
