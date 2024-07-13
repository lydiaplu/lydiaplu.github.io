---
title: Java Built-in Exception Classes
date: 2023-09-15 13:20:32  
toc: true  
categories:  
- java  

---

# Java Built-in Exception Classes

In Java, the root class for exception hierarchy is `Throwable`, which is divided into two subclasses: `Error` and `Exception`.

`Exception` is divided into `RuntimeException` (runtime exceptions) and non-runtime exceptions.

## Runtime Exceptions (subclasses of `RuntimeException`)

| Exception Class                    | Description                                                  |
| ---------------------------------- | ------------------------------------------------------------ |
| **ArithmeticException**            | Thrown when an exceptional arithmetic condition occurs, such as division by zero. |
| **NullPointerException**           | Thrown when attempting to access a member of or call a method on a null object. |
| **ArrayIndexOutOfBoundsException** | Thrown when trying to access an array element with an illegal index. |
| **IndexOutOfBoundsException**      | Thrown to indicate that an index is out of range; parent class of `ArrayIndexOutOfBoundsException`. |
| **NumberFormatException**          | Thrown when attempting to convert a string to a number of invalid format. |
| **IllegalArgumentException**       | Thrown when a method receives an argument that is not appropriate. |
| **ClassCastException**             | Thrown when attempting to cast an object to a subclass it is not an instance of. |
| **NoSuchElementException**         | Thrown when attempting to access an element that does not exist. |

## Non-runtime Exceptions

| Exception Class            | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| **IOException**            | Thrown during general input/output operations.               |
| **FileNotFoundException**  | Thrown when an attempt to open a file denoted by a specified pathname has failed. |
| **EOFException**           | Thrown when the end of a file or stream is unexpectedly reached. |
| **ClassNotFoundException** | Thrown when an application tries to load a class through its string name but no definition for the class with the specified name could be found. |
| **NoSuchMethodException**  | Thrown when a particular method cannot be found.             |
| **InterruptedException**   | Thrown when a thread is waiting, sleeping, or otherwise occupied, and the thread is interrupted. |
| **SQLException**           | Thrown during database operations; commonly associated with Java's database connectivity. |
| **SecurityException**      | Thrown by the security manager to indicate a security violation. |
| **IllegalStateException**  | Thrown to indicate that a method has been invoked at an illegal or inappropriate time. |

These are some common built-in exception classes. Java provides many other exception classes, each representing a specific type of exceptional condition.

When writing Java programs, you can use `try-catch` blocks to catch and handle these exceptions.