### Spring JDBC

---

### JDBC

- Java Database Connectivity
- Allow connecting to the database from Java

---

### Set Up

+++

### DB Setup

- ensure you database is set up properly
- TCP/IP ports 
- username/password
- user-DB permission mapping (if not admin)
- database schema is set up properly

+++ 

### Spring Setup

- add JDBC to list of Maven dependencies
- add DB config to application.properties

```
spring.datasource.driver-class-name=
spring.datasource.url=
spring.datasource.username=
spring.datasource.password= 1
```

+++

### .gitignore

- tells `git` to avoid pushing a particular folder/file to git
- avoid uploading sensitive info (e.g. emails/passwords)

---

### AirBnB Schema

- users
- properties
- bookings
- payments
- reviews
- tags

---

### JDBC Concepts

+++

### Entities

- beans representing objects in the DB
- 1 class per table
- each bean much have correct getters/setters

+++

```java
class User {
    private name;

    String getName() {
        return this.name;
    }

    void setName(String name) {
        this.name = name;
    }
}
```

+++

### Data Access Object (DAO)

- connector between DB and Java
- similar to `Repository`, used interchangeably

+++

```java
@Transactional
@Repository
public class UserDAO {
    private final JdbcTemplate jdbcTemplate;
    @Autowired
    public UserDAO(JdbcTemplate jdbcTemplate) {
	  this.jdbcTemplate = jdbcTemplate;
    }

    public List<User> getAllUsers() {
        String sql = "SELECT id, name FROM users";
        RowMapper<User> rowMapper = new UserRowMapper();
        return this.jdbcTemplate.query(sql, rowMapper);
    } 
}
```

@[1-3,15](DAO wrapper)
@[4-8](Constructor)
@[5-14](Method)

+++

### RowMapper 

- converts SQL data to Java Objects
- checks SQL column name
- matches to Java class property name

+++


```java
import java.sql.ResultSet;
import java.sql.SQLException;
import org.springframework.jdbc.core.RowMapper; 

public class UserRowMapper implements RowMapper<User> {
   @Override
   public User mapRow(ResultSet row, int rowNum) throws SQLException {
	User user = new User();
	user.setId(row.getInt("id"));
	user.setName(row.getString("name"));
	return user;
   }
}
```

+++

### BeanRowMapper

- automatically maps Sql to Java 
- can only be used if column names and Java property names match

+++

```java
public List<User> getAllUsers() {
    String sql = "SELECT id, name FROM users";
    RowMapper<User> rowMapper = new BeanPropertyRowMapper();
    return this.jdbcTemplate.query(sql, rowMapper);
} 
```
---

### CRUD

+++

### Create

```java
public void addArticle(Article article) {
    //Add article
    String sql = "INSERT INTO articles (articleId, title, category) values (?, ?, ?)";
    jdbcTemplate.update(sql, article.getArticleId(), article.getTitle(), article.getCategory());
    
    //Fetch article id
    sql = "SELECT articleId FROM articles WHERE title = ? and category=?";
    int articleId = jdbcTemplate.queryForObject(sql, Integer.class, article.getTitle(), article.getCategory());
    
    //Set article id 
    article.setArticleId(articleId);
}
```

+++

### Read

```java
public Article getArticleById(int articleId) {
    String sql = "SELECT articleId, title, category FROM articles WHERE articleId = ?";
    RowMapper<Article> rowMapper = new BeanPropertyRowMapper<Article>(Article.class);
    Article article = jdbcTemplate.queryForObject(sql, rowMapper, articleId);
    return article;
}


public List<Article> getAllArticles() {
    String sql = "SELECT articleId, title, category FROM articles";
            //RowMapper<Article> rowMapper = new BeanPropertyRowMapper<Article>(Article.class);
    RowMapper<Article> rowMapper = new ArticleRowMapper();
    return this.jdbcTemplate.query(sql, rowMapper);
}
```

+++

### Update

```java
public void updateArticle(Article article) {
    String sql = "UPDATE articles SET title=?, category=? WHERE articleId=?";
    jdbcTemplate.update(sql, article.getTitle(), article.getCategory(), article.getArticleId());
}
```

+++

### Delete

```java
public boolean articleExists(String title, String category) {
    String sql = "SELECT count(*) FROM articles WHERE title = ? and category=?";
    int count = jdbcTemplate.queryForObject(sql, Integer.class, title, category);
    if(count == 0) {
                return false;
    } else {
        return true;
    }
}
```





