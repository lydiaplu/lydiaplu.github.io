---
title: Spring Lombok
date: 2023-12-20 18:31:39
toc: true  
categories:  
- Spring Boot 3


---

# Spring Lombok

In Spring, Lombok is a Java library that is used to minimize boilerplate code. It uses annotations to generate common methods like getters, setters, constructors, `toString`, `equals`, and `hashCode` methods during compile time. Below are some of the most common Lombok annotations and features:

### Common Lombok Annotations and Features:

1. **@NoArgsConstructor**: Generates a no-arguments constructor.
2. **@RequiredArgsConstructor**: Generates a constructor with required arguments (fields marked as `final` or annotated with `@NonNull`).
3. **@AllArgsConstructor**: Generates a constructor with all fields as arguments.
4. **@Data**: Generates `getter`, `setter`, `equals()`, `hashCode()`, and `toString()` methods.
5. **@Value**: Similar to `@Data`, but generates an immutable class (all fields are `final`).
6. **@Builder**: Generates a builder pattern for creating complex objects.
7. **@SneakyThrows**: Automatically adds exception handling code in methods.
8. **@Cleanup**: Automatically closes resources, like file streams or database connections.
9. **@Slf4j**: Automatically generates logging code and integrates with various logging frameworks.
10. **@EqualsAndHashCode**: Generates `equals()` and `hashCode()` methods.
11. **@ToString**: Generates a `toString()` method.
12. **@Getter**: Generates `getter` methods.
13. **@Setter**: Generates `setter` methods.
14. **@Delegate**: Delegates method implementation to another object.
15. **@Value.Immutable**: Generates immutable value objects.
16. **@Wither**: Generates a method that returns a new instance with a specified field value changed.
17. **@NoArgsConstructor(force = true)**: Generates a no-arguments constructor, even if there are `final` fields.

### Detailed Explanation and Usage Examples:

1. **@NoArgsConstructor**, **@AllArgsConstructor**, and **@RequiredArgsConstructor**:

   - `@NoArgsConstructor`: Generates a no-arguments constructor.
   - `@AllArgsConstructor`: Generates a constructor with all fields as arguments.
   - `@RequiredArgsConstructor`: Generates a constructor with required arguments (fields marked as `final` or annotated with `@NonNull`).

   ```java
   import lombok.*;
   
   @NoArgsConstructor
   @AllArgsConstructor
   @RequiredArgsConstructor
   public class Person {
       @NonNull private String firstName;
       @NonNull private String lastName;
       private int age;
   }
   ```

2. **@Data** and **@Value**:

   - `@Data`: Generates `getter`, `setter`, `equals()`, `hashCode()`, and `toString()` methods.
   - `@Value`: Similar to `@Data`, but generates an immutable class (all fields are `final`).

   ```java
   import lombok.*;
   
   @Data
   public class Book {
       private String title;
       private String author;
       private int pageCount;
   }
   ```

3. **@Builder**: Generates a builder pattern for creating complex objects.

   ```java
   import lombok.*;
   
   @Builder
   public class Product {
       private String name;
       private String category;
       private double price;
   }
   
   // Creating an instance using the builder pattern
   Product product = Product.builder()
       .name("Widget")
       .category("Electronics")
       .price(19.99)
       .build();
   ```

4. **@SneakyThrows**: Automatically adds exception handling code in methods.

   ```java
   import lombok.SneakyThrows;
   
   public class FileProcessor {
       @SneakyThrows
       public void processFile() {
           // No need to explicitly handle the exception
           throw new Exception("Something went wrong.");
       }
   }
   ```

5. **@Cleanup**: Automatically closes resources, like file streams or database connections.

   ```java
   import lombok.Cleanup;
   
   public class FileHandler {
       public void readFile(String filePath) {
           @Cleanup FileReader reader = new FileReader(filePath);
           // Read file
       }
   }
   ```

6. **@Slf4j**: Automatically generates logging code and integrates with various logging frameworks.

   ```java
   import lombok.extern.slf4j.Slf4j;
   
   @Slf4j
   public class LoggerExample {
       public void logSomething() {
           log.debug("This is a debug message.");
           log.info("This is an info message.");
       }
   }
   ```

7. **@Getter** and **@Setter**: Generates `getter` and `setter` methods.

   ```java
   import lombok.Getter;
   import lombok.Setter;
   
   public class Student {
       @Getter @Setter private String name;
       @Getter @Setter private int age;
   }
   ```

Using Lombok annotations can significantly reduce the amount of boilerplate code in your Java classes, making your code more concise and easier to maintain.