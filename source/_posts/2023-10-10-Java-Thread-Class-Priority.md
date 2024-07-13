---
title: Java Thread Class Priority
date: 2023-10-10 18:55:07
toc: true  
categories:  
- java  
---

# Java Thread Class Priority

The `priority` attribute in the `Thread` class is used to set and get the priority of a thread. Thread priority is an integer value, typically ranging from 1 to 10, where 1 represents the lowest priority and 10 represents the highest priority. By default, a thread's priority is set to 5.

### Usage

1. **Setting Thread Priority**: You can set a thread's priority using the `setPriority(int priority)` method. The parameter passed to this method should be an integer representing the thread's new priority. Note that a thread's priority must be within the supported range of the operating system.

   ```java
   Thread thread = new Thread(() -> {
       // Task for the thread
   });
   thread.setPriority(Thread.MAX_PRIORITY); // Set the thread's priority to the highest
   thread.start();
   ```

2. **Getting Thread Priority**: You can get a thread's current priority using the `getPriority()` method.

   ```java
   int priority = thread.getPriority();
   System.out.println("Thread Priority: " + priority);
   ```

### Example Code

Here's an example that demonstrates setting and getting thread priorities:

```java
public class ThreadPriorityExample {
    public static void main(String[] args) {
        // Create a thread with default priority
        Thread thread1 = new Thread(() -> {
            System.out.println("Thread 1 is running with priority: " + Thread.currentThread().getPriority());
            try {
                Thread.sleep(1000); // Simulate work
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 1 is done.");
        });

        // Create a thread with maximum priority
        Thread thread2 = new Thread(() -> {
            System.out.println("Thread 2 is running with priority: " + Thread.currentThread().getPriority());
            try {
                Thread.sleep(1000); // Simulate work
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 2 is done.");
        });

        // Set thread priorities
        thread1.setPriority(Thread.MIN_PRIORITY); // Set thread1 to minimum priority
        thread2.setPriority(Thread.MAX_PRIORITY); // Set thread2 to maximum priority

        // Start threads
        thread1.start();
        thread2.start();
    }
}
```

### Important Considerations

1. **Relative Concept of Priority**: Thread priority affects the likelihood of a thread being scheduled but does not strictly determine the execution order. The actual behavior depends on the operating system and thread scheduler, and can vary between platforms.

2. **Avoid Over-reliance on Priority**: Thread priority should not be relied upon to ensure the correctness of the program. Correctness should be ensured through proper synchronization and mutual exclusion mechanisms, not just by adjusting thread priorities.

3. **Cross-platform Behavior**: Thread priority behavior can differ across operating systems. When writing cross-platform code, use thread priority cautiously.

4. **Do Not Abuse Thread Priority**: Excessive use of thread priority can lead to unstable program behavior and race conditions. Typically, the default thread priority should be sufficient, and manual priority adjustments should be reserved for special cases.

### Summary

Thread priority is a mechanism for adjusting the scheduling behavior of threads but should be used with caution. Proper concurrent control should rely on synchronization, mutual exclusion, and other concurrent programming principles rather than solely on thread priority.