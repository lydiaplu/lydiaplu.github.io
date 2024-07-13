---
title: Captured Variables in Java
date: 2023-09-22 19:31:15
toc: true  
categories:  
- java  
---

# Captured Variables in Java

In Java, "captured variables" refer to those variables that are captured by anonymous inner classes, local classes, or lambda expressions from their enclosing scopes. This primarily involves local variables or parameters, as these variables are not visible outside the method or block scope in which they are defined. When an anonymous inner class, local class, or lambda expression references these variables in its definition, they are referred to as captured variables.

The concept of captured variables is a form of closure support in Java. This allows programmers to reference and use variables from the outer scope within inner classes, local classes, or lambda expressions, enabling more flexible and powerful programming patterns.

### Features

1. **Final or Effectively Final**: In Java 8 and later versions, the captured local variables must be either final or effectively final. This means that the variable cannot be modified after it is initialized. This rule ensures that the value of the variable remains consistent and safe when used within the inner class or lambda expression.

2. **Scope**: Anonymous inner classes, local classes, or lambda expressions can capture and use local variables defined within the method that defines them, but these variables are not visible outside their defining method or block scope.

3. **Lifecycle**: The lifecycle of captured variables within anonymous inner classes, local classes, or lambda expressions may exceed the lifecycle of the variables in their original scope. This is because instances of inner classes or lambda expressions may continue to exist even after the scope of the captured variables has ended.

### Example

```java
public class Example {
    public void method() {
        int localVar = 100; // Local variable to be captured

        // Anonymous inner class
        Runnable r = new Runnable() {
            public void run() {
                System.out.println(localVar);
            }
        };

        // Lambda expression
        Runnable rLambda = () -> System.out.println(localVar);
    }
}
```

In this example, `localVar` is a local variable that is captured by both an anonymous inner class and a lambda expression. Within these inner classes or lambda expressions, they can access and use `localVar`, even though their definition exceeds the direct scope of `localVar`.

### Additional Notes

- **Final or Effectively Final**: A variable is effectively final if it is not explicitly declared as final but is never modified after initialization. The Java compiler enforces this rule to prevent concurrent modifications and ensure thread safety.

- **State Sharing**: Capturing variables allow state sharing between the enclosing method and the inner class or lambda expression. This is useful for maintaining shared state or passing contextual information.

### Practical Use

Captured variables are commonly used in scenarios involving event handling, multithreading, and functional programming, where inner classes or lambda expressions need to reference the outer scope variables.

```java
public class CapturedVariablesExample {
    public void execute() {
        int counter = 10; // Captured variable

        // Lambda expression capturing counter
        Runnable task = () -> {
            for (int i = 0; i < counter; i++) {
                System.out.println("Count: " + i);
            }
        };

        // Run the task
        new Thread(task).start();
    }

    public static void main(String[] args) {
        CapturedVariablesExample example = new CapturedVariablesExample();
        example.execute();
    }
}
```

In this example, the `counter` variable is captured by the lambda expression used to define the `task` Runnable. This allows the lambda expression to access and use the `counter` variable even though it is defined outside the lambda's immediate scope.