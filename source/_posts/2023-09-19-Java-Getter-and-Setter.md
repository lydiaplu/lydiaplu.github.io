---
title: Java Getter and Setter
date: 2023-09-19 10:31:10
toc: true  
categories:  
- java  

---

# Java Getter and Setter

Getter and setter methods are public methods used to access and modify the private variables of a class.

**Getter Method**:  
A getter method's name starts with "get" followed by the field name and it does not have any parameters.

For example, if there is a private field `name`, create a getter method `getName()` to get the value of `name`:

```java
public class Person {
    private String name;

    // Getter method to get the value of the name field
    public String getName() {
        return name;
    }
}
```

**Setter Method**:  
A setter method's name starts with "set" followed by the field name, and it has a parameter to pass the new value to be set.

For example, to set the value of the `name` field, create a setter method `setName()`:

```java
public class Person {
    private String name;

    // Setter method to set the value of the name field
    public void setName(String newName) {
        name = newName;
    }
}
```

**Usage**

By using getter and setter methods, you can access and modify private fields from outside the class while adding validation logic and control to ensure data consistency and security.

```java
public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        
        // Use setter method to set the value of the name field
        person.setName("Alice");
        
        // Use getter method to get the value of the name field
        String name = person.getName();
        System.out.println("Name: " + name); // Outputs "Name: Alice"
    }
}
```

In the example above, the `Person` class has a private field `name`, and public getter and setter methods `getName()` and `setName()`. The `Main` class demonstrates how to use these methods to set and get the value of the `name` field, ensuring encapsulation and providing a way to control the access and modification of the private field.