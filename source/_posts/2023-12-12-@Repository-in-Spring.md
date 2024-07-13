---
title: @Repository in Spring
date: 2023-12-12 17:09:25
toc: true  
categories:  
- Spring Boot 3

---

# @Repository in Spring

The `@Repository` annotation in Spring is used to mark a class as a Data Access Object (DAO). It is a specialization of the `@Component` annotation, which makes it eligible for Spring's component scanning to detect and register as a Spring bean. Using `@Repository` provides several additional benefits specific to the data access layer.

### Key Features

1. **Component Scanning**: Classes annotated with `@Repository` are automatically detected and registered as Spring beans during component scanning. This enables dependency injection for these classes throughout the application.

2. **Exception Translation**: One of the significant benefits of using `@Repository` is that it provides automatic exception translation. Spring converts database-related exceptions (such as those thrown by JDBC, JPA, or Hibernate) into Spring's `DataAccessException`. This ensures that the application does not need to handle vendor-specific exceptions and can rely on consistent exception handling.

3. **Code Clarity and Layering**: By using `@Repository`, you clearly indicate the purpose of the class, which is to perform data access operations. This improves the readability and maintainability of the code by clearly separating the data access layer from other layers such as the service layer or the controller layer.

### Example

Here is an example of using the `@Repository` annotation in a Spring application:

```java
import org.springframework.stereotype.Repository;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.beans.factory.annotation.Autowired;

@Repository
public class UserRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public User findById(Long id) {
        String sql = "SELECT * FROM users WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new Object[]{id}, (rs, rowNum) ->
                new User(
                        rs.getLong("id"),
                        rs.getString("name"),
                        rs.getString("email")
                ));
    }

    public int save(User user) {
        String sql = "INSERT INTO users (name, email) VALUES (?, ?)";
        return jdbcTemplate.update(sql, user.getName(), user.getEmail());
    }

    // Additional CRUD methods can be defined here
}
```

In this example, the `UserRepository` class is marked with `@Repository`, indicating that it is a DAO. The class uses `JdbcTemplate` to perform database operations. The methods `findById` and `save` handle specific queries and updates, respectively.

### Points to Note

- **Optional Usage**: Technically, you can use `@Component` instead of `@Repository`, but using `@Repository` explicitly indicates the role of the class and leverages the benefits of exception translation.
- **Integration with JPA or Hibernate**: When using JPA or Hibernate, the `@Repository` annotation is typically used in conjunction with `EntityManager` or `SessionFactory` to perform data access operations.
- **Improved Maintainability**: Proper use of `@Repository` helps in organizing the code better, making it more maintainable and readable, especially in large applications.

### Example with JPA

Here's an example of a repository using JPA:

```java
import org.springframework.stereotype.Repository;
import org.springframework.data.jpa.repository.JpaRepository;

@Repository
public interface UserJpaRepository extends JpaRepository<User, Long> {
    // JpaRepository provides CRUD methods
}
```

In this example, `UserJpaRepository` extends `JpaRepository`, which provides built-in CRUD methods. The `@Repository` annotation indicates that this interface is a Spring repository bean, and Spring Data JPA will automatically provide the implementation.

Using `@Repository` appropriately ensures that your data access layer is well-defined and consistent with Spring's architecture, providing better exception handling and component management.