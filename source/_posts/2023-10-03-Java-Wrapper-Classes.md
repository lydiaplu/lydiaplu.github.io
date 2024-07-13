---
title: Java Wrapper Classes
date: 2023-10-03 11:28:58
toc: true  
categories:  
- java  

---

# Java Wrapper Classes

In Java, wrapper classes are object representations of primitive data types (e.g., `int`, `char`, `boolean`, etc.). Java is an object-oriented language, and sometimes it is necessary to treat primitive data types as objects, which is where wrapper classes come in.

| Primitive Type | Corresponding Wrapper Class |
| -------------- | --------------------------- |
| `int`          | `Integer`                   |
| `char`         | `Character`                 |
| `boolean`      | `Boolean`                   |
| `long`         | `Long`                      |
| `double`       | `Double`                    |
| `float`        | `Float`                     |
| `short`        | `Short`                     |
| `byte`         | `Byte`                      |

#### Autoboxing and Unboxing

Java 5 introduced autoboxing and unboxing, which allow automatic conversion between primitive data types and their corresponding wrapper class objects.

- **Autoboxing**: Automatic conversion of a primitive type to its corresponding wrapper class.
- **Unboxing**: Automatic conversion of a wrapper class object to its corresponding primitive type.

```java
Integer wrapperInt = 5; // Autoboxing (int -> Integer)
int primitiveInt = wrapperInt; // Unboxing (Integer -> int)
```

#### Use in Collection Framework

In Java's collection framework, such as `ArrayList` and `HashMap`, only object references can be stored. Therefore, if you need to store primitive data types, you must use their corresponding wrapper classes.

```java
ArrayList<Integer> intList = new ArrayList<>();
intList.add(3); // Autoboxing
int number = intList.get(0); // Unboxing
```

#### Points to Note

1. **Null Handling**: Wrapper classes can be `null`, whereas primitive data types cannot. When using unboxing, if the wrapper class reference is `null`, it will throw a `NullPointerException`.

2. **Performance Considerations**: Although autoboxing and unboxing are convenient, they can impact performance. Frequent boxing and unboxing operations can lead to additional performance overhead.

3. **Equality Comparison**: Be careful when comparing wrapper class objects. Using the `==` operator compares object references, not values. To compare values, use the `.equals()` method.

   ```java
   // Using Integer wrapper class
   Integer num1 = 100;
   Integer num2 = 100;
   Integer num3 = new Integer(100);
   
   // Using == for comparison
   System.out.println("num1 == num2: " + (num1 == num2)); // May be true due to autoboxing cache
   System.out.println("num1 == num3: " + (num1 == num3)); // False, because num3 is created with new
   
   // Using .equals() for comparison
   System.out.println("num1.equals(num2): " + num1.equals(num2)); // True, values are equal
   System.out.println("num1.equals(num3): " + num1.equals(num3)); // True, values are equal
   ```

4. **Caching Mechanism**: Certain wrapper classes (e.g., `Integer` and `Byte`) cache a range of commonly used objects. For example, `Integer` caches objects in the range `-128` to `127`, so comparisons of these objects may have unexpected results (as shown above).

   ```java
   Integer a = 127;
   Integer b = 127;
   System.out.println(a == b); // True, because the value is within the [-128, 127] range
   
   Integer c = 128;
   Integer d = 128;
   System.out.println(c == d); // False, because the value is outside the [-128, 127] range
   ```

Wrapper classes in Java provide a way to treat primitive types as objects, enabling them to be used in collections, support null values, and utilize object methods. However, developers must be aware of the potential performance costs and nuances of using these classes to ensure efficient and correct code.