---
title: Functional Interface in Java
date: 2023-09-25 15:18:33
toc: true  
categories:  
- java  

---

# Functional Interface in Java

In Java, a functional interface is a special type of interface that defines exactly one abstract method. Because of this characteristic, functional interfaces can be implicitly converted to lambda expressions. Java 8 introduced the concept of functional interfaces as a key foundation for lambda expressions.

### Features

1. **Single Abstract Method (SAM)**: A functional interface contains only one abstract method. This characteristic is known as the "Single Abstract Method" (SAM) principle. This does not mean that a functional interface cannot have other methods; it can have default and static methods.

2. **`@FunctionalInterface` Annotation**: While not mandatory, it is common practice to use the `@FunctionalInterface` annotation on a functional interface. This annotation not only clarifies the intended use of the interface but also ensures that the interface does not accidentally have more than one abstract method during compilation.

3. **Compatible with Lambda Expressions**: Since a functional interface has only one abstract method, it can be implicitly converted to a lambda expression. This makes functional interfaces ideal for implementing functional programming concepts, such as passing methods as parameters.

### Example

A simple example of a functional interface:

```java
@FunctionalInterface
public interface SimpleFunctionalInterface {
    void execute(); // Single abstract method
}
```

You can use a lambda expression to implement this interface:

```java
SimpleFunctionalInterface sfi = () -> System.out.println("Executing...");
sfi.execute(); // Outputs: Executing...
```

### Built-in Functional Interfaces

Java 8 provides a series of built-in functional interfaces located in the `java.util.function` package. Some commonly used ones include:

- `Predicate<T>`: Takes one argument and returns a boolean value.
- `Consumer<T>`: Takes one argument and returns no result.
- `Function<T, R>`: Takes one argument and returns a result.
- `Supplier<T>`: Takes no arguments and returns a result.
- `UnaryOperator<T>`: Takes one argument of type T and returns a result of type T.
- `BinaryOperator<T>`: Takes two arguments of the same type and returns a result of the same type.

### Example of Using Built-in Functional Interfaces

Here are some examples of how to use these built-in functional interfaces with lambda expressions:

```java
import java.util.function.*;

public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        // Predicate example
        Predicate<Integer> isPositive = (i) -> i > 0;
        System.out.println(isPositive.test(10)); // Outputs: true

        // Consumer example
        Consumer<String> print = (s) -> System.out.println(s);
        print.accept("Hello, World!"); // Outputs: Hello, World!

        // Function example
        Function<String, Integer> length = (s) -> s.length();
        System.out.println(length.apply("Hello")); // Outputs: 5

        // Supplier example
        Supplier<String> greeting = () -> "Hello, World!";
        System.out.println(greeting.get()); // Outputs: Hello, World!

        // UnaryOperator example
        UnaryOperator<Integer> square = (i) -> i * i;
        System.out.println(square.apply(5)); // Outputs: 25

        // BinaryOperator example
        BinaryOperator<Integer> add = (a, b) -> a + b;
        System.out.println(add.apply(2, 3)); // Outputs: 5
    }
}
```

The introduction of functional interfaces in Java greatly enhances the language's expressiveness, especially when using lambda expressions and method references. This allows Java to write more concise, flexible, and understandable code, making it an important step forward in modernizing the language.