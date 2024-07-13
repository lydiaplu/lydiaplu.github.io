---
title: Consumerin Java
date: 2023-10-07 18:27:33
toc: true  
categories:  
- java  

---

# Consumer in Java

In Java, the `Consumer` interface is a functional interface defined in the `java.util.function` package. It represents an operation that takes a single input argument and returns no result. As a functional interface, `Consumer` can be used for lambda expressions and method references.

1. **Single Abstract Method**: The `Consumer` interface defines one abstract method, `accept(T t)`, which takes an argument and performs some operation but does not return any result.
2. **Generics**: The `Consumer` interface is generic, allowing you to specify the type of the input object.
3. **Usage**: Commonly used in scenarios where an operation needs to be performed on an object (such as printing, modifying, etc.) without needing to return a result.
4. **Chaining Operations**: The `Consumer` interface also provides the `andThen` method, allowing you to chain multiple `Consumer` operations together.

### Example

```
java
Copy code
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        Consumer<String> printConsumer = s -> System.out.println(s);
        printConsumer.accept("Hello, World!"); // Outputs: Hello, World!
    }
}
```

In this example, `printConsumer` is a `Consumer<String>` that takes a string as input and prints it to the console.

### `andThen` Method Example

The `andThen` method of the `Consumer` interface can be used to create a sequence of `Consumer` operations:

```
java
Copy code
Consumer<String> printConsumer = s -> System.out.println(s);
Consumer<String> printConsumerUpperCase = printConsumer.andThen(s -> System.out.println(s.toUpperCase()));

printConsumerUpperCase.accept("hello"); // First prints "hello", then prints "HELLO"
```

In this example, `printConsumerUpperCase` first executes the `printConsumer` operation (printing the original string) and then executes the operation that converts the string to uppercase and prints it.

### Practical Example

Suppose we have a list of strings and we want to print each string. We can use the `Consumer` interface to accomplish this:

```
java
Copy code
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        List<String> strings = Arrays.asList("one", "two", "three");

        Consumer<String> printConsumer = str -> System.out.println(str);
        
        strings.forEach(printConsumer); // Prints each string
    }
}
```

In this example:

- `printConsumer` is an implementation of `Consumer` that takes a string and prints it.
- We use the `forEach` method to iterate over the list of strings and apply `printConsumer` to each string (i.e., print each string).

### Usage Scenarios

The `Consumer` interface is commonly used in scenarios where an operation needs to be performed on an object without returning a result, such as iterating over collections to perform operations, executing side effects of functions, etc. Due to its simplicity, it is very common in Java code that follows a functional programming style.