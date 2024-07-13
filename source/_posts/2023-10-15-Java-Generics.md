---
title: Java Generics
date: 2023-10-15 08:23:31
toc: true  
categories:  
- java  

---

# Java Generics

Generics in Java is a feature that allows you to write code that can handle different types of data in a type-safe and reusable manner. Generics provide a way to define classes, interfaces, and methods with type parameters, which increases code reusability, type safety, and readability.

### Types of Generics

### 1. Generic Classes

A generic class allows you to define a class with a type parameter.

```java
public class Box<T> {
    private T content;

    public Box(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

// Instantiation
Box<Integer> intBox = new Box<>(42);
Box<String> strBox = new Box<>("Hello, Generics!");

Integer intValue = intBox.getContent();
String strValue = strBox.getContent();
```

In this example, `Box` is a generic class where `<T>` denotes the type parameter. When creating a `Box` object, you specify the actual type, such as `Box<Integer>` or `Box<String>`.

### 2. Generic Methods

A generic method allows you to define a method with a type parameter.

```java
public class Main {
    public static void main(String[] args) {
        Integer[] intArray = { 5, 2, 9, 1, 5, 6 };
        Integer maxInt = findMax(intArray);
        System.out.println("Max Integer: " + maxInt);

        String[] strArray = { "apple", "banana", "cherry", "date" };
        String maxStr = findMax(strArray);
        System.out.println("Max String: " + maxStr);
    }

    public static <T extends Comparable<T>> T findMax(T[] arr) {
        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("Array is empty");
        }

        T max = arr[0];
        for (T element : arr) {
            if (element.compareTo(max) > 0) {
                max = element;
            }
        }
        return max;
    }
}
```

In this example, `findMax` is a generic method using `<T>` to specify the type parameter. It can accept arrays of any type that implements the `Comparable` interface and find the maximum value.

### 3. Generic Interfaces

A generic interface allows you to define an interface with a type parameter.

```java
public interface MyListInterface<T> {
    void add(T element);
    T get(int index);
    int size();
}

public class MyList<T> implements MyListInterface<T> {
    private List<T> list = new ArrayList<>();

    @Override
    public void add(T element) {
        list.add(element);
    }

    @Override
    public T get(int index) {
        return list.get(index);
    }

    @Override
    public int size() {
        return list.size();
    }
}

// Usage
MyListInterface<Integer> intList = new MyList<>();
intList.add(1);
intList.add(2);

MyListInterface<String> strList = new MyList<>();
strList.add("apple");
strList.add("banana");
```

### Generic Wildcards

Wildcards in Java generics provide flexibility when using generic types. They are often used with generic classes, methods, and interfaces to handle different types of data.

#### Types of Wildcards

1. **Unbounded Wildcard `?`**: Represents any type.

```java
public void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}
```

2. **Bounded Wildcard `? extends T`**: Represents any type that is a subclass of `T`.

```java
public static double sumOfList(List<? extends Number> list) {
    double sum = 0.0;
    for (Number num : list) {
        sum += num.doubleValue();
    }
    return sum;
}
```

### Wildcard Usage Notes

- Wildcards represent an unknown type and ensure type safety by only allowing read operations.
- Writing to a wildcard collection is not allowed to maintain type safety.

```java
public void writeToList(List<?> list) {
    list.add("New Element"); // Compilation error
}

// Correct usage with generic method
public <T> void writeToList(List<T> list, T element) {
    list.add(element); // Valid operation
}
```

### Summary

Generics in Java enhance code reusability and type safety by allowing you to write classes, interfaces, and methods that can operate on different types of data. They ensure that your code is flexible, readable, and less error-prone by providing compile-time type checking. Understanding how to use generic classes, methods, interfaces, and wildcards effectively is crucial for writing robust and maintainable Java programs.