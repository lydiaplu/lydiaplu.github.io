---
title: Nested Classes in Java
date: 2023-09-22 09:28:31
toc: true  
categories:  
- java  

---

# Nested Classes in Java

### 1. Static Nested Class

#### Features

- Defined as a static member of its outer class.
- Can access all static members and methods of the outer class, even if they are declared private.
- Does not hold a reference to an instance of its outer class.

```java
public class OuterClass {
    private static String staticVar = "Static Variable";

    public static class StaticNestedClass {
        public void display() {
            System.out.println(staticVar); // Access static variable of outer class
        }
    }
}

// Usage
OuterClass.StaticNestedClass nestedObj = new OuterClass.StaticNestedClass();
nestedObj.display();
```

### 2. Member Inner Class

#### Features

- Defined as a non-static member of the outer class.
- Can access all members and methods of the outer class, including private members.
- Holds an implicit reference to an instance of its outer class.

```java
public class OuterClass {
    private String instanceVar = "Instance Variable";

    public class InnerClass {
        public void display() {
            System.out.println(instanceVar); // Access instance variable of outer class
        }
    }
}

// Usage
OuterClass outer = new OuterClass();
OuterClass.InnerClass inner = outer.new InnerClass();
inner.display();
```

### 3. Local Class

#### Features

- Defined within a block, such as within a method body.
- Can access local variables of the block in which they are defined (must be final or effectively final).
- Cannot define or access static members.

```java
public class OuterClass {
    public void someMethod() {
        final int localVar = 100;

        class LocalClass {
            public void display() {
                System.out.println(localVar); // Access local variable
            }
        }

        LocalClass localClass = new LocalClass();
        localClass.display();
    }
}

// Usage
OuterClass outer = new OuterClass();
outer.someMethod();
```

### 4. Anonymous Class

#### Features

- Has no class name and is typically used to create one-time use classes.
- Can implement an interface or extend a class.
- Commonly used for GUI event handling and iterators.

```java
interface Greeting {
    void greet();
}

public class Example {
    public static void main(String[] args) {
        Greeting greeting = new Greeting() {
            @Override
            public void greet() {
                System.out.println("Hello, World!");
            }
        };

        greeting.greet();
    }
}

// Usage
Example.main(null);
```

### Use Cases

- **Static Nested Class**: Used when the inner class does not need to access instance members of the outer class. They are typically used to group class logic together without creating dependencies on an instance of the outer class.
- **Member Inner Class**: Used when the inner class needs to access instance members of the outer class. They can access all members of the outer class, including private ones.
- **Local Class**: Used when you need to define a class within a block and use it only within that block.
- **Anonymous Class**: Suitable for simple, one-time use implementations, especially when implementing interfaces or extending classes.

Each type of nested class has its specific use case and advantages. The choice of which to use depends on your particular needs and context.