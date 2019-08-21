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