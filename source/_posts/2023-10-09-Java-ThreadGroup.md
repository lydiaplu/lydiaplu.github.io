---
title: Java ThreadGroup
date: 2023-10-09 11:51:26
toc: true  
categories:  
- java  

---

# Java ThreadGroup

`ThreadGroup` is a container that is used to organize and manage threads. It acts like a folder that holds threads together.

### Key Features and Usage

1. **Creating a Thread Group**: You can create a new thread group just like creating a folder and give it a name.

   ```java
   ThreadGroup group = new ThreadGroup("MyThreadGroup");
   ```

2. **Adding Threads to a Thread Group**: When creating a thread, you can specify which thread group the thread belongs to.

   ```java
   Thread thread1 = new Thread(group, () -> {
       // Work of thread 1
       for (int i = 0; i < 5; i++) {
           System.out.println(Thread.currentThread().getName() + " is running.");
           try {
               Thread.sleep(1000);
           } catch (InterruptedException e) {
               System.out.println(Thread.currentThread().getName() + " was interrupted.");
           }
       }
   }, "Thread-1");
   ```

3. **Controlling the Thread Group**: You can perform operations on the entire thread group, such as interrupting all threads in the group.

   ```java
   group.interrupt(); // Interrupts all threads in the thread group
   ```

4. **Handling Exceptions**: You can set an uncaught exception handler for the thread group to handle exceptions from threads within the group.

   ```java
   group.uncaughtException(Thread thread, Throwable exception) {
       // Handle uncaught exceptions
       System.out.println(thread.getName() + " threw exception: " + exception);
   }
   ```

### Example Code

Below is a complete example demonstrating the creation of a thread group, adding threads to the group, and controlling the threads within the group:

```java
public class ThreadGroupExample {
    public static void main(String[] args) {
        // Create a thread group
        ThreadGroup group = new ThreadGroup("MyThreadGroup");
        
        // Set uncaught exception handler for the group
        group.setUncaughtExceptionHandler((t, e) -> {
            System.out.println(t.getName() + " threw exception: " + e);
        });

        // Create threads and add them to the thread group
        Thread thread1 = new Thread(group, () -> {
            for (int i = 0; i < 5; i++) {
                System.out.println(Thread.currentThread().getName() + " is running.");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    System.out.println(Thread.currentThread().getName() + " was interrupted.");
                }
            }
        }, "Thread-1");

        Thread thread2 = new Thread(group, () -> {
            for (int i = 0; i < 5; i++) {
                System.out.println(Thread.currentThread().getName() + " is running.");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    System.out.println(Thread.currentThread().getName() + " was interrupted.");
                }
            }
        }, "Thread-2");

        // Start the threads
        thread1.start();
        thread2.start();

        // Main thread sleeps for 2 seconds
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Interrupt all threads in the group
        group.interrupt();
    }
}
```

### Important Notes

- **Not Recommended for Advanced Concurrency**: `ThreadGroup` is not the best practice for thread management in advanced concurrent applications. It has limitations and lacks some features needed for modern concurrency control.
- **Use ExecutorService**: For better thread management, it is recommended to use `ExecutorService` or other concurrency utilities provided by the `java.util.concurrent` package.

`ThreadGroup` can be useful for basic thread grouping and simple thread management tasks, but for more robust and scalable solutions, prefer using higher-level concurrency frameworks.