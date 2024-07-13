---
title: Java Thread and Runnable
date: 2023-10-08 15:29:33
toc: true  
categories:  
- java  

---

# Java Thread and Runnable

In Java, you can use the `Thread` class and the `Runnable` interface to create multi-threaded programs. Both methods allow you to execute multiple tasks concurrently within a single program, but there are important differences between them.

Using the `Runnable` interface to create threads is recommended in Java because it offers better flexibility and organization of code. The `Thread` class should only be used in specific scenarios, such as when you need to directly control the lifecycle of a thread.

### Using the `Thread` Class

The `Thread` class represents a thread in Java. You can create a thread by extending the `Thread` class.

```java
class MyThread extends Thread {
    public void run() {
        // Code to be executed by the thread
        for (int i = 0; i < 5; i++) {
            System.out.println("Thread: " + i);
        }
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread();
        MyThread thread2 = new MyThread();

        thread1.start(); // Start thread 1
        thread2.start(); // Start thread 2
    }
}
```

**Points to Note**:

- Extending the `Thread` class limits your class to only be a thread, as Java does not support multiple inheritance.
- The `run` method contains the code that the thread will execute. You need to override the `run` method to define the thread's behavior.
- Use the `start()` method to start the thread. Each call to `start()` creates a new thread and executes the `run` method in a new thread.

### Using the `Runnable` Interface

The `Runnable` interface is a functional interface that you can implement to create a thread. This approach is more flexible because you can implement multiple interfaces and are not restricted by single inheritance. Here is an example of creating a thread using the `Runnable` interface:

```java
class MyRunnable implements Runnable {
    public void run() {
        // Code to be executed by the thread
        for (int i = 0; i < 5; i++) {
            System.out.println("Runnable: " + i);
        }
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();

        Thread thread1 = new Thread(myRunnable); // Create thread 1 and pass the runnable object
        Thread thread2 = new Thread(myRunnable); // Create thread 2 and pass the runnable object

        thread1.start(); // Start thread 1
        thread2.start(); // Start thread 2
    }
}
```

**Points to Note**:

- Implementing the `Runnable` interface does not restrict your class to being a single thread because you can pass the runnable object to multiple threads.
- The `run` method contains the code that the thread will execute. You need to implement the `run` method to define the thread's behavior.
- When creating a `Thread` object, pass the `Runnable` object to the thread's constructor.
- Use the `start()` method to start the thread.

### Summary

- **Thread Class**:
  - Extend the `Thread` class.
  - Override the `run` method.
  - Create an instance of your class and call `start()` to run the thread.

- **Runnable Interface**:
  - Implement the `Runnable` interface.
  - Implement the `run` method.
  - Create an instance of `Thread` by passing the `Runnable` object to its constructor.
  - Call `start()` to run the thread.

Using the `Runnable` interface is generally preferred for creating threads in Java because it promotes better design by separating the task from the thread management, making the code more flexible and easier to maintain.