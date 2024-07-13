---
title: Introduction to Java Classes
date: 2023-09-17 13:20:32  
toc: true  
categories:  
- java  

---

# Introduction to Java Classes

In Java, a class is a blueprint or template used to create objects.

A class defines the properties and behaviors of objects. Properties are commonly referred to as fields, and behaviors are commonly referred to as methods.

### Class:

- **Definition**: A class is a user-defined data type that describes the common characteristics and behaviors of a group of objects.
- **Purpose**: A class defines the properties (fields) and actions (methods) of objects. You can create multiple objects based on the class, and each object can have the same properties and methods.

```java
public class Person {
    // Instance fields
    private String name;
    private int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Instance method
    public void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}
```

In the example above, the `Person` class defines two instance fields (`name` and `age`) and one instance method (`sayHello`).

### Fields:

- **Definition**: Fields are member variables of a class used to store the state or properties of objects. Each object has a set of fields, and the values of these fields can vary between different objects.
- **Purpose**: Fields are used to describe the properties of objects, such as name, age, address, etc. They are stored in the memory of objects and can be accessed and modified through object references.
- **Example**: In the example above, `name` and `age` are two instance fields.

### Methods:

- **Definition**: Methods are functions or operations within a class used to perform specific tasks or operations. Methods define the behaviors of objects.
- **Purpose**: Methods are used to define the actions of objects, such as calculations, printing, modifying field values, etc. They allow external code to interact with objects.
- **Example**: In the example above, `sayHello` is an instance method used to print a greeting.
