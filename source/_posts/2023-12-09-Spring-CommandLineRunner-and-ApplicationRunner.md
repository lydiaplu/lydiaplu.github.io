---
title: Spring CommandLineRunner and ApplicationRunner
date: 2023-12-09 09:18:52
toc: true  
categories:  
- Spring Boot 3
---

# Spring CommandLineRunner and ApplicationRunner

In Spring Boot, `CommandLineRunner` and `ApplicationRunner` are two interfaces used to run specific blocks of code after the application has started. They are commonly used for initialization tasks, such as loading data, checking system status, or performing some automated tasks.

### CommandLineRunner

- **Purpose**: All beans implementing the `CommandLineRunner` interface will be run after the Spring Boot application has started and is ready.

- **Method**: It has a single method `run(String... args)` that receives the command-line arguments passed to the application.

- **Example**:

  ```java
  import org.springframework.boot.CommandLineRunner;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyCommandLineRunner implements CommandLineRunner {
      @Override
      public void run(String... args) {
          // Initialization code here
          System.out.println("CommandLineRunner is executing");
      }
  }
  ```

  In this example, the `MyCommandLineRunner` class implements the `CommandLineRunner` interface and overrides the `run` method. The code inside the `run` method will be executed when the application starts.

### ApplicationRunner

- **Purpose**: Similar to `CommandLineRunner`, `ApplicationRunner` is also used to execute code after the Spring Boot application has started.

- **Method**: It has a single method `run(ApplicationArguments args)` that provides a more structured way to access command-line arguments.

- **Example**:

  ```java
  import org.springframework.boot.ApplicationArguments;
  import org.springframework.boot.ApplicationRunner;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyAppRunner implements ApplicationRunner {
      @Override
      public void run(ApplicationArguments args) {
          // Initialization code here
          System.out.println("ApplicationRunner is executing");
      }
  }
  ```

  In this example, the `MyAppRunner` class implements the `ApplicationRunner` interface and overrides the `run` method. `ApplicationArguments` provides more detailed access to the command-line arguments, such as distinguishing between named and unnamed arguments.

### Choosing Between CommandLineRunner and ApplicationRunner

The main difference between the two interfaces is how they handle command-line arguments. If you need a simple string array (e.g., standard command-line arguments), `CommandLineRunner` is sufficient. If you need more complex functionality, such as distinguishing between option arguments and non-option arguments or converting arguments to specific types, then `ApplicationRunner` is more suitable.

In a Spring Boot application, you can choose one or both interfaces to implement beans that will run initialization tasks based on your needs.