---
title: Java Thread States
date: 2023-10-09 17:37:09
toc: true  
categories:  
- java  

---

# Java Thread States

The `Thread` class in Java represents a thread of execution in a program. Throughout its lifecycle, a thread can be in one of several states, defined as constants in the `Thread` class.

### Thread States and Their Descriptions

1. **NEW**: 
   - The thread has been created but has not yet started.
   - The thread object is instantiated, but system resources are not yet allocated.

2. **RUNNABLE**: 
   - The thread is ready to run after the `start()` method is called.
   - It may be running or waiting for CPU time.
   - The exact timing of execution is determined by the operating system's thread scheduler.

3. **BLOCKED**: 
   - The thread is blocked, waiting to acquire a monitor lock.
   - It occurs when a thread attempts to access a synchronized block or method currently held by another thread.

4. **WAITING**: 
   - The thread is waiting indefinitely for another thread to perform a particular action.
   - This state is entered by calling methods like `Object.wait()`, `Thread.join()`, or `LockSupport.park()`.

5. **TIMED_WAITING**: 
   - The thread is waiting for another thread to perform an action for up to a specified waiting time.
   - This state is entered by calling methods like `Thread.sleep(long millis)`, `Object.wait(long timeout)`, `Thread.join(long millis)`, `LockSupport.parkNanos(long nanos)`, or `LockSupport.parkUntil(long deadline)`.

6. **TERMINATED**: 
   - The thread has completed its execution.
   - This occurs when the `run()` method has finished execution or the thread has been interrupted.

### Example to Demonstrate Thread States

Below is an example that demonstrates the transition of a thread through various states from creation to termination:

```java
public class ThreadStatesExample {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            try {
                // Entering TIMED_WAITING state
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread is running.");
        });

        // NEW state: Thread has been created but not started
        System.out.println("Thread state after creation: " + thread.getState());

        thread.start();

        // RUNNABLE state: Thread has been started
        System.out.println("Thread state after start(): " + thread.getState());

        try {
            // Give the thread some time to move to TIMED_WAITING state
            Thread.sleep(200);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // TIMED_WAITING state: Thread is sleeping
        System.out.println("Thread state after sleep(): " + thread.getState());

        try {
            thread.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // TERMINATED state: Thread has finished execution
        System.out.println("Thread state after join(): " + thread.getState());

        // At the end, the thread should be in TERMINATED state
        System.out.println("Thread state at the end: " + thread.getState());
    }
}
```

### Explanation of the Example

- **NEW**: The thread is in the `NEW` state after it is created but before `start()` is called.
- **RUNNABLE**: After calling `start()`, the thread moves to the `RUNNABLE` state.
- **TIMED_WAITING**: When `Thread.sleep(1000)` is called within the thread, it enters the `TIMED_WAITING` state for 1000 milliseconds.
- **TERMINATED**: After the thread finishes its execution or is interrupted, it moves to the `TERMINATED` state.

### Conclusion

The `Thread` class's states help in understanding and managing thread execution in a Java program. By using methods like `Thread.getState()`, developers can effectively debug and manage multi-threaded applications. Understanding these states and their transitions is crucial for writing efficient and reliable concurrent code in Java.