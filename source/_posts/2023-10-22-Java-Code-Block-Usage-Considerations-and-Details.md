---
title: Java Code Block Usage Considerations and Details
date: 2023-10-22 18:37:25
toc: true  
categories:  
- java  
---

# Java Code Block Usage Considerations and Details

### 1. static code block

- **Static Code Block**: The static code block, also known as the static initializer, is used to initialize the class.
- **Execution**: It executes when the class is loaded and runs only **once**.
- **Difference from Instance Initializer Block**: Unlike instance initializer blocks, which run each time an object is created, static blocks run only once.

### Example:

```java
class Example {
    private static int count;

    static {
        count = 10;
        System.out.println("Static block executed.");
    }

    public Example() {
        System.out.println("Constructor executed.");
    }

    public static void main(String[] args) {
        System.out.println("Main method executed.");
        Example ex1 = new Example();
        Example ex2 = new Example();
    }
}
```

**Output**:
```
Static block executed.
Main method executed.
Constructor executed.
Constructor executed.
```

### 2. When is a class loaded? [Important to remember]

1. **When creating an instance of the class (`new`)**
   ```java
   Example ex = new Example();
   ```
2. **When creating an instance of a subclass, the parent class is also loaded**
   ```java
   class Parent {}
   class Child extends Parent {}
   Child c = new Child(); // Both Parent and Child classes will be loaded
   ```
3. **When accessing static members of the class (static attributes, static methods)**
   ```java
   Example.count; // Accessing a static variable
   ```

### 3. Instance Initializer Block

- **Execution**: The instance initializer block runs when an instance of the class is created.
- **Execution Frequency**: It is executed each time an object is created.
- **Non-execution with Static Members**: If only the class's static members are accessed, the instance initializer block will not execute.

### Example:

```java
class Example {
    {
        System.out.println("Instance initializer block executed.");
    }

    public Example() {
        System.out.println("Constructor executed.");
    }

    public static void main(String[] args) {
        System.out.println("Main method executed.");
        Example ex1 = new Example();
        Example ex2 = new Example();
    }
}
```

**Output**:
```
Main method executed.
Instance initializer block executed.
Constructor executed.
Instance initializer block executed.
Constructor executed.
```

### Demonstration Case: Class A extends Class B with static block

```java
class A {
    private int n1 = 10;
    static {
        System.out.println("A");
    }
}

class B extends A {
    private int n2 = 20;
    public static int totalNum = 100;
    static {
        System.out.println("B");
    }
}

public class Test {
    public static void main(String[] args) {
        System.out.println("Main method");
        B b = new B();
    }
}
```

**Output**:
```
A
B
Main method
Instance initializer block executed.
Constructor executed.
```

In this example, the static block of class A will execute first, followed by the static block of class B when class B is loaded. Then, the main method is executed. When an instance of class B is created, the instance initializer block (if any) and constructor of class A will execute first, followed by those of class B.