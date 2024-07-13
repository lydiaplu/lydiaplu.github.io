---
title: Java's Thread Methods
date: 2023-10-10 10:28:51
toc: true  
categories:  
- java  

---

# Java's `Thread` Methods

## Get and Set Methods

### 1. `Thread.getThreadGroup()`

The `getThreadGroup()` method is used to get the thread group to which the thread belongs. For example:

```java
ThreadGroup threadGroup = Thread.currentThread().getThreadGroup();
System.out.println("Thread Group Name: " + threadGroup.getName());
```

### 2. `Thread.setDaemon()`

The `setDaemon(boolean on)` method is used to set the thread as a daemon thread. Daemon threads automatically exit when the main thread finishes. For example:

```java
Thread daemonThread = new Thread(() -> {
    while (true) {
        // Do some work
    }
});

// Set as a daemon thread
daemonThread.setDaemon(true);
daemonThread.start();
```

## Enquiry Methods

### `Thread.isAlive()`

The `isAlive()` method is used to check if the thread is alive (not yet terminated). For example:

```java
Thread myThread = new Thread(() -> {
    // Do some work
});

myThread.start();
boolean isAlive = myThread.isAlive();
System.out.println("Is thread alive: " + isAlive);
```

## Action Methods

### 1. `Thread.interrupt()`

The `interrupt()` method is used to interrupt a thread. It sets the thread's interrupt status but does not immediately terminate the thread. The thread needs to check its interrupt status and respond appropriately to exit safely. For example:

```java
Thread myThread = new Thread(() -> {
    while (!Thread.currentThread().isInterrupted()) {
        // Do some work
    }
    // Handle thread interruption logic
});

myThread.start();

// Interrupt the thread at some point
myThread.interrupt();
```

## Static Methods

### 1. `Thread.currentThread()`

The `currentThread()` method is used to get the currently executing thread. For example:

```java
Thread currentThread = Thread.currentThread();
System.out.println("Current Thread: " + currentThread.getName());
```

### 2. `Thread.activeCount()`

The `activeCount()` method is used to get the number of active threads in the current thread group. For example:

```java
ThreadGroup threadGroup = Thread.currentThread().getThreadGroup();
int activeThreadCount = threadGroup.activeCount();
System.out.println("Active Thread Count: " + activeThreadCount);
```

### 3. `Thread.dumpStack()`

The `dumpStack()` method prints the stack trace of the current thread to the standard error stream (`System.err`). This is useful for debugging and analyzing problems such as exceptions or deadlocks. For example:

```java
Thread.dumpStack();
```

## Example Code Demonstrating All Methods

Below is a comprehensive example that demonstrates the usage of various `Thread` methods:

```java
public class ThreadMethodsExample {
    public static void main(String[] args) {
        // Creating and starting a thread
        Thread thread1 = new Thread(() -> {
            System.out.println("Thread 1 is running.");
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                System.out.println("Thread 1 was interrupted.");
            }
            System.out.println("Thread 1 is done.");
        });

        // Setting thread1 as a daemon thread
        thread1.setDaemon(true);
        thread1.start();

        // Getting thread group of the current thread
        ThreadGroup threadGroup = Thread.currentThread().getThreadGroup();
        System.out.println("Thread Group Name: " + threadGroup.getName());

        // Checking if thread1 is alive
        boolean isAlive = thread1.isAlive();
        System.out.println("Is Thread 1 alive: " + isAlive);

        // Interrupting thread1
        thread1.interrupt();

        // Getting the current thread
        Thread currentThread = Thread.currentThread();
        System.out.println("Current Thread: " + currentThread.getName());

        // Getting active thread count in the current thread group
        int activeThreadCount = threadGroup.activeCount();
        System.out.println("Active Thread Count: " + activeThreadCount);

        // Printing stack trace of the current thread
        Thread.dumpStack();

        // Wait for thread1 to finish
        try {
            thread1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Main thread is done.");
    }
}
```

This example demonstrates how to:

1. Create and start a thread.
2. Set a thread as a daemon thread.
3. Get the thread group of the current thread.
4. Check if a thread is alive.
5. Interrupt a thread.
6. Get the current thread.
7. Get the number of active threads in the current thread group.
8. Print the stack trace of the current thread.
9. Wait for a thread to finish using `join()`.

Using these methods effectively can help manage and control the behavior of threads in a Java application.