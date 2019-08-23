## Testing-3

---

### Today's topics
- controller testing
- testing environments

---


### Controller Tests

- test HTTP requests
- set request method (GET/POST)
- set request body (json)
- assert the response

---

### Concept

- Given
- When

+++

### Given:

- which endpoint
- which request method (GET/POST)
- what request body (json?)
- which request params
- any existing data in DB?

+++

### When

- executing the request

+++

### Then

- what kind of response?
- any changes in the DB?

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
    public void testGetIndex() throws Exception {
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
    public void testPostIndex() throws Exception {
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

### Refactorings

- configure different DB for tests vs dev
- use inheritance to make your tests DRY
- cleaning up data in DB before/after tests

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
spring.datasource.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
spring.datasource.url=jdbc:sqlserver://localhost;databaseName=<name>
spring.datasource.username=<name>
spring.datasource.password=<password>
```

---

### Tests Inheritance

- share similar DB
- share similar profiles
- share simiar before/after methods

+++

### Parent

```java
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
public abstract class BaseControllerTest {
    @LocalServerPort
    protected int port;

    @Autowired
    protected TestRestTemplate restTemplate;
}
```

+++

### Child

```java
public class EmployeeControllerTest extends BaseControllerTest {

    @Test
    public void getHello() throws Exception {
        String url = new URL("http://localhost:" + port + "/").toString();

        ResponseEntity<String> response = restTemplate.getForEntity(url, String.class);

        assertEquals("{}", response.getBody());
    }
}
```

+++

What is the diff between <span class="text-blue">protected</span> and <span class="text-blue">private</span>?

---

### Configuring Test DB in Spring

- use a different DB when running tests
- clean up the DB at the end of every test



+++

### Cleaning Up Database Before/After Tests

- not needed for repository/service tests (they are transactional)
- required for controller tests

+++

```java
@After
public void cleanDB() {
    userRepo.deleteAll();
    appointmentRepo.deleteAll()
}
```

+++

### For All Tables

```java
@PersistenceContext(type = PersistenceContextType.EXTENDED)
private EntityManager entityManager;

@After
public void teardown() {
    List<String> tableNames = new ArrayList<>();
    Session session = entityManager.unwrap(Session.class);
    Set<EntityType<?>> entities = session.getEntityManagerFactory().getMetamodel().getEntities();
    
    for (EntityType<?> entity: entities) { 
        String tablename = entity.getJavaType().getAnnotation(Table.class).name();
        tableNames.add(tablename);
    }

    Transaction txn = session.beginTransaction();
    entityManager.flush();

    for (String tableName: tableNames) {
        entityManager.createNativeQuery("ALTER TABLE " + tableName + " NOCHECK CONSTRAINT all").executeUpdate();
    }

    for (String tableName: tableNames) {
        entityManager.createNativeQuery("DELETE FROM " + tableName).executeUpdate();
    }

    for (String tableName: tableNames) {
        entityManager.createNativeQuery("ALTER TABLE " + tableName + " WITH CHECK CHECK CONSTRAINT all").executeUpdate();
    }

    txn.commit();
}
```

---

### Exercise

- add login to the app

+++iti

### Exercise

- test user login
- test user signup
- test <span class="text-blue">/employees/1/appointments</span> with authorization