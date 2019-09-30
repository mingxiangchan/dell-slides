---
marp: true
---

# Automated Testing: Spring

---

## Spring vs No Spring

- testing HTTP requests
- testing DB interactions

---

## Setup

- no setup needed! Spring Boot already comes wth JUnit 4 preinstalled.

---

## Data Layer Testing

- test DB repositories
- test services that use repositories

---

## Repository Tests

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

## Exercise

- Clone [this](https://github.com/mingxiangchan/dell-spring-junit) repository

---

## EmployeeRepositoryTest

- test `findAll`
- test `findById`
- test `findByEmail`
- test `findByName`
- test `findAll` with `sorting`

---

## AppointmentRepositoryTest

- test `findAll`
- test `findByTimeslotBetween`
- test `findByEmployeeEmailContains`

---

# Services

- intermediary between `controller` and `repository`
- can do more complex logic
- can interact with multiple repositories

---

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

`checkAppointment(Employee employee)`
- get all appointments for a user
- go through each appointment and get the timeslot, extract into array
- return `List<LocalDateTime>` 

---

### Exercise: BookingService

`bookAppointment(timeslot, employee)`
- 1 timeslot is 2 hours
- check whether intended timeslot [conflicts with an existing appointment](https://stackoverflow.com/questions/46942351/checking-if-localdatetime-falls-within-a-time-range)
- if success, save appointment into DB
- if failure, return `null`


---

### Controller Tests

- test HTTP requests
- set request method (GET/POST)
- set request body (json)
- assert the response

---

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

---

## POST Tests

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

## Exercise

- Write tests for the `EmployeeController`
- Write tests for the `AppointmentsController`

---


## EmployeeControllerTest

- test `GET /employees`
- test `GET /employees?email=<email>`
- test `GET /employees/{id}`
- test `POST /employees`

---

## AppointmentsController

- test `GET /appointments`
- test `GET /employees/{id}/appointments`
- test `GET /appointments/{id}`
- test `POST /appointments`

---

## Configuring Test DB in Spring

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

---

## Cleaning Up Database Before/After Tests

- not needed for repository/service tests (they are transactional)
- required for controller tests

---

```java
@AfterEach
public void cleanDB() {
    userRepo.deleteAll();
    appointmentRepo.deleteAll()
}
```

---

## Types of Tests

- unit
- integration
- feature

---

## Cost vs Benefit

- Integration tests have most value
- Integration tests are hardest to set up

---

## Example: Grab Order Cancellation

- customer cancelling an order
- test how much is the cancellation fee

---

## Integration Test Setup

- service
- customer
- driver
- customer's order
- discovery sent to driver
- driver confirmation for order

---

## Unit Test Setup

- only set up customer's order
- setup 

---

## Assignment: Order Creation

- products
- orders
- line_items
- payments

---

## Features

- create an order with line_items
    - product, customer are set up before order creation
- pay for an order
    - order is set up before payment creation
- refund an order
    - payment is set up before refund processing

---

### Instructions

1. create the tables needed
2. create a `ShoppingService`
3. create tests for the 3 features
4. write code to make the 3 features work!

