---
title: Java Thread.join()
date: 2023-10-09 20:17:52
toc: true  
categories:  
- java  
---

# Java `Thread.join()`

The `join()` method in Java is used to wait for a thread to complete its execution. When one thread calls the `join()` method on another thread, it pauses its execution until the thread it called `join()` on has finished. This method is typically used to coordinate the execution order of multiple threads, ensuring that one thread continues only after another has finished.

### Basic Usage of `join()` Method

1. **Wait for a Thread to Finish**: If thread A calls the `join()` method on thread B, thread A will wait until thread B finishes its execution before resuming.

2. **Wait for a Specified Time**: The `join()` method can also take a timeout parameter, allowing the calling thread to wait for a specified amount of time. If the thread being joined does not finish within the timeout period, the calling thread will resume execution.

Below is a simple example to demonstrate the usage of the `join()` method:

```java
public class JoinExample {
    public static void main(String[] args) {
        Thread thread1 = new Thread(() -> {
            System.out.println("Thread 1 is running.");
            try {
                Thread.sleep(2000); // Simulate work with sleep
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 1 is done.");
        });

        Thread thread2 = new Thread(() -> {
            System.out.println("Thread 2 is running.");
            try {
                Thread.sleep(3000); // Simulate work with sleep
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 2 is done.");
        });

        thread1.start();
        thread2.start();

        try {
            thread1.join(); // Wait for thread1 to finish
            System.out.println("Thread 1 has finished.");
            
            thread2.join(1500); // Wait for thread2 to finish or timeout after 1.5 seconds
            System.out.println("Thread 2 has finished or timed out.");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Main thread is done.");
    }
}
```

### Explanation of the Example

1. **Creating Threads**: Two threads, `thread1` and `thread2`, are created. Each thread prints a message, sleeps for a specified time to simulate work, and then prints a completion message.

2. **Starting Threads**: Both threads are started using the `start()` method.

3. **Joining Threads**:
    - The main thread calls `thread1.join()`, causing it to wait until `thread1` finishes its execution.
    - After `thread1` completes, the main thread prints a message and then calls `thread2.join(1500)`, causing it to wait for `thread2` to finish or timeout after 1.5 seconds.
    - After waiting for `thread2`, the main thread prints another message indicating whether `thread2` has finished or the wait has timed out.

4. **Main Thread Completion**: Finally, the main thread prints a message indicating its completion.

### Practical Applications

- **Ensuring Order of Execution**: When you need to ensure that one thread completes its task before another thread starts or continues.
- **Dependency Management**: Managing dependencies between tasks running in different threads.
- **Resource Cleanup**: Ensuring that resources are released or cleaned up only after certain tasks have completed.

### Key Points

- **Thread State**: When a thread is waiting for another thread to complete, it is in a blocked state.
- **InterruptedException**: The `join()` method can throw an `InterruptedException` if the waiting thread is interrupted. It is essential to handle this exception appropriately.
- **Timeout**: The timeout versions of `join()` (`join(long millis)` and `join(long millis, int nanos)`) allow for more fine-grained control over how long a thread should wait.

The `join()` method is a powerful tool for thread synchronization and can be very useful in scenarios where the completion of one task depends on the completion of another.