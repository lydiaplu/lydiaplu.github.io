---
title: Spring MVC's @RestController
date: 2023-12-17 18:19:21
toc: true  
categories:  
- Spring Boot 3

---

# Spring MVC's @RestController

`@RestController` is an annotation in Spring MVC used to create RESTful web services. It combines the `@Controller` and `@ResponseBody` annotations, simplifying the controller implementation. Here are some key annotations related to `@RestController` along with their descriptions and usage:

1. **@RestController**

   - **Description**: Indicates that the class is a controller where every method returns a domain object instead of a view. Each method's return value is automatically serialized to JSON and written into the HTTP response body.
   - **Usage**: Typically used to create REST APIs. Used at the class level.

     ```java
     @RestController
     public class MyController {
         // ...
     }
     ```

2. **@RequestMapping**

   - **Description**: Maps HTTP requests to handler methods of MVC and REST controllers.
   - **Usage**: Can be used at both the class and method levels. Supports configuring URL patterns, HTTP methods, request parameters, headers, etc.

     ```java
     @RequestMapping(value = "/users", method = RequestMethod.GET)
     public List<User> getUsers() {
         // ...
     }
     ```

3. **@GetMapping, @PostMapping, @PutMapping, @DeleteMapping**

   - **Description**: Specialized versions of `@RequestMapping` for specific HTTP methods.
   - **Usage**: Used at the method level, directly specifying the URL path and the HTTP method type.

     ```java
     @GetMapping("/users")
     public User getUser() {
         // ...
     }
     ```

4. **@PathVariable**

   - **Description**: Binds a method parameter to a URI template variable.
   - **Usage**: Commonly used in RESTful web services.

     ```java
     @GetMapping("/users/{id}")
     public User getUser(@PathVariable Long id) {
         // ...
     }
     ```

5. **@RequestParam**

   - **Description**: Binds a method parameter to a web request parameter.
   - **Usage**: Used to handle query parameters.

     ```java
     @GetMapping("/users")
     public List<User> getUsers(@RequestParam String role) {
         // ...
     }
     ```

6. **@RequestBody**

   - **Description**: Binds the HTTP request body to a method parameter.
   - **Usage**: Commonly used in POST and PUT methods.

     ```java
     @PostMapping("/users")
     public User addUser(@RequestBody User user) {
         // ...
     }
     ```

7. **@ResponseBody**

   - **Description**: Indicates that the return value of a method should be written directly to the HTTP response body.
   - **Usage**: In a `@RestController`, all methods implicitly use `@ResponseBody`.

     ```java
     @GetMapping("/greeting")
     public String greeting() {
         return "Hello, World";
     }
     ```

8. **@ResponseStatus**

   - **Description**: Marks a method or exception class with the status code and reason message that should be returned.
   - **Usage**: Often used for exception handling or specific operations.

     ```java
     @ResponseStatus(HttpStatus.CREATED)
     @PostMapping("/users")
     public User addUser(@RequestBody User user) {
         // ...
     }
     ```

9. **@CrossOrigin**

   - **Description**: Enables cross-origin resource sharing (CORS) for the annotated methods or types.
   - **Usage**: Can be applied at both the class and method levels to allow cross-origin requests.

     ```java
     @CrossOrigin(origins = "http://example.com")
     @GetMapping("/users")
     public List<User> getUsers() {
         // ...
     }
     ```

### Example of a Spring MVC Controller with @RestController

```java
import org.springframework.web.bind.annotation.*;

import java.util.ArrayList;
import java.util.List;

@RestController
@RequestMapping("/api")
public class UserController {

    private List<User> users = new ArrayList<>();

    @GetMapping("/users")
    public List<User> getUsers() {
        return users;
    }

    @GetMapping("/users/{id}")
    public User getUser(@PathVariable int id) {
        return users.stream().filter(user -> user.getId() == id).findFirst().orElse(null);
    }

    @PostMapping("/users")
    @ResponseStatus(HttpStatus.CREATED)
    public User addUser(@RequestBody User user) {
        users.add(user);
        return user;
    }

    @PutMapping("/users/{id}")
    public User updateUser(@PathVariable int id, @RequestBody User userDetails) {
        User user = users.stream().filter(u -> u.getId() == id).findFirst().orElse(null);
        if (user != null) {
            user.setName(userDetails.getName());
            user.setEmail(userDetails.getEmail());
        }
        return user;
    }

    @DeleteMapping("/users/{id}")
    public void deleteUser(@PathVariable int id) {
        users.removeIf(user -> user.getId() == id);
    }
}
```

In this example:
- `@RestController` is used to define the controller.
- Various HTTP methods (`@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`) are used to handle different types of HTTP requests.
- `@RequestMapping("/api")` at the class level sets the base URL for all endpoints in the controller.
- `@PathVariable`, `@RequestParam`, and `@RequestBody` are used to handle path variables, query parameters, and request bodies, respectively.
- `@ResponseStatus` is used to set the HTTP status code for the response.