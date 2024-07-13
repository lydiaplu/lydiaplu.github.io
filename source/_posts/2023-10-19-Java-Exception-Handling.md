---
title: Java Exception Handling
date: 2023-10-19 15:33:20
toc: true  
categories:  
- java  
---



# Java Exception Handling

In Java, you can throw errors (exceptions) in several ways:

1. **Using the `throw` keyword**: You can manually throw an exception using the `throw` keyword. Typically, you need to create an exception object (like a subclass of `RuntimeException`) and pass it to the `throw` keyword. For example:

   ```java
   throw new RuntimeException("This is a custom exception message");
   ```

2. **Using predefined exception classes**: Java has many built-in exception classes that you can use to throw exceptions as needed. For example:

   ```java
   throw new NullPointerException("Object is null, cannot perform the operation");
   throw new IOException("An I/O exception occurred");
   ```

3. **Custom exception classes**: You can create your custom exception classes, typically inheriting from `Exception` or its subclasses, to represent specific error conditions.

   ```java
   public class CustomException extends Exception {
       public CustomException(String message) {
           super(message);
       }
   }
   
   // Throwing a custom exception
   throw new CustomException("Custom exception message");
   ```

4. **Using the `throws` keyword**: In the method signature, you can use the `throws` keyword to declare that the method may throw an exception. This informs the caller that the method might raise a specific type of exception. The caller must handle the exception or propagate it to the next level.

   ```java
   public void someMethod() throws IOException {
       // ...
       if (someCondition) {
           throw new IOException("I/O exception");
       }
       // ...
   }
   ```

5. **Exception chaining**: After catching an exception, you can wrap it in another exception and throw it, thus creating an exception chain. This is often used to throw higher-level exceptions without losing the original exception information. For example:

   ```java
   try {
       // ...
   } catch (IOException e) {
       throw new CustomException("An exception occurred while processing the file", e);
   }
   ```

   Here, the `CustomException` includes the original `IOException` to aid in debugging and problem resolution.

### Example of Handling Exceptions

Here is a comprehensive example demonstrating the different ways to throw and handle exceptions in Java:

```java
// Custom Exception Class
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
    
    public CustomException(String message, Throwable cause) {
        super(message, cause);
    }
}

public class ExceptionHandlingExample {

    public static void main(String[] args) {
        try {
            methodThatThrows();
        } catch (IOException e) {
            System.out.println("Caught IOException: " + e.getMessage());
        } catch (CustomException e) {
            System.out.println("Caught CustomException: " + e.getMessage());
            e.printStackTrace();
        }
    }

    public static void methodThatThrows() throws IOException, CustomException {
        try {
            riskyMethod();
        } catch (IOException e) {
            throw new CustomException("CustomException wrapping IOException", e);
        }
    }

    public static void riskyMethod() throws IOException {
        throw new IOException("Original IOException");
    }
}
```

In this example:

- A `CustomException` class is defined.
- The `methodThatThrows` method declares that it may throw both `IOException` and `CustomException`.
- The `riskyMethod` method throws an `IOException`.
- The `methodThatThrows` method catches the `IOException` and wraps it in a `CustomException` before throwing it.
- The `main` method handles both `IOException` and `CustomException`, demonstrating how to catch and process multiple exceptions.