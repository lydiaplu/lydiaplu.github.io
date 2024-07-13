---
title: Java Thread Synchronized
date: 2023-10-08 21:15:08
toc: true  
categories:  
- java  
---

# Java Thread Synchronized

| Name                       | Explanation and Usage                                        |
| -------------------------- | ------------------------------------------------------------ |
| Resource Sharing           | Multiple threads or processes need to access and use the same resources or data. In concurrent programming, it is essential to ensure the safe access to shared resources. |
| Critical Section           | A critical section is a block or region of code that accesses shared resources and needs to ensure that only one thread can enter. Locks or mutexes are often used to protect critical sections. |
| Mutual Exclusion           | Mutual exclusion is a synchronization mechanism used to ensure that only one thread can access shared resources at any given time. It is typically achieved using locks or mutexes. |
| Locking/Mutex              | A lock is a synchronization mechanism used to control the access of multiple threads to shared resources. Mutexes are often used to protect critical sections and prevent multiple threads from accessing them simultaneously. |
| Semaphore                  | A semaphore is a synchronization mechanism used to control the concurrent access of multiple threads. It can be used to limit the number of threads accessing shared resources simultaneously. |
| Monitor                    | A monitor is a high-level synchronization mechanism that includes locks and condition variables used to manage thread access to shared resources. It is typically provided by the programming language or library. |
| Race Condition             | A race condition occurs in a multithreaded environment when the program's outcome depends on the order of thread execution rather than the code logic. Race conditions can lead to unpredictable results and errors. |
| Inter-Thread Communication | Inter-thread communication refers to the process of passing information, sharing data, or collaborating on tasks between multiple threads. It typically requires synchronization mechanisms such as condition variables, semaphores, or queues. |

### 1. Resource Sharing

- **Meaning**: Multiple threads or processes need to access and use the same resources or data to ensure safe access to shared resources.
- **Example Code**: Multiple threads in a multithreaded program need to access a shared global counter.

```java
class SharedResource {
    private int count = 0;

    // Synchronized block ensures that multiple threads cannot enter simultaneously, ensuring correct incrementing of count
    public synchronized void increment() {
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}

public class ResourceSharingExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Create multiple threads to operate on shared resource
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        // Start threads
        thread1.start();
        thread2.start();

        try {
            // Wait for threads to finish execution
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Get the final value of the shared resource
        int finalCount = sharedResource.getCount();
        System.out.println("Final Count: " + finalCount);
    }
}
```

In this example, two threads (`thread1` and `thread2`) share a `SharedResource` instance and call the `increment()` method to increase the value of `count`. Since the `increment()` method is synchronized, multiple threads cannot enter it simultaneously, ensuring the correct incrementing of `count`. Finally, the final value of the shared resource is printed.

### 2. Critical Section

- **Meaning**: A critical section is a block or region of code that accesses shared resources and needs to ensure that only one thread can enter. Locks or mutexes are often used to protect critical sections.
- **Example Code**: In a multithreaded program, the code block accessing shared resources needs to be executed under the protection of a mutex.

```java
class SharedResource {
    private int count = 0;
    private final Object lock = new Object(); // Lock object to create a synchronized block

    public void increment() {
        synchronized (lock) {
            count++;
        }
    }

    public int getCount() {
        synchronized (lock) {
            return count;
        }
    }
}

public class CriticalSectionExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Create multiple threads to operate on shared resource
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        // Start threads
        thread1.start();
        thread2.start();

        try {
            // Wait for threads to finish execution
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Get the final value of the shared resource
        int finalCount = sharedResource.getCount();
        System.out.println("Final Count: " + finalCount);
    }
}
```

In this example, the `lock` object is used to create a synchronized block that ensures thread safety when accessing the `count` variable in a multithreaded environment.

### 3. Mutual Exclusion

- **Meaning**: Mutual exclusion is a synchronization mechanism used to ensure that only one thread can access shared resources at any given time.
- **Example Code**: Using Java's `synchronized` keyword to implement mutual exclusion.

```java
class SharedResource {
    private int count = 0;

    // Synchronized keyword ensures mutual exclusion for the increment() method
    public synchronized void increment() {
        count++;
    }

    // Synchronized keyword ensures mutual exclusion for the getCount() method
    public synchronized int getCount() {
        return count;
    }
}

public class MutexExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Create multiple threads to operate on shared resource
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        // Start threads
        thread1.start();
        thread2.start();

        try {
            // Wait for threads to finish execution
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Get the final value of the shared resource
        int finalCount = sharedResource.getCount();
        System.out.println("Final Count: " + finalCount);
    }
}
```

In this example, the `SharedResource` class contains a shared counter `count`, and both the `increment()` and `getCount()` methods use the `synchronized` keyword to ensure mutual exclusion. Two threads (`thread1` and `thread2`) operate on the `SharedResource` simultaneously, but due to the mutual exclusion, they do not access the `increment()` method at the same time, ensuring correct counting. Finally, the final value of the shared resource is printed.

### 4. Locking/Mutex

- **Meaning**: A lock is a synchronization mechanism used to control the access of multiple threads to shared resources.
- **Example Code**: Using Java's `ReentrantLock` class to create locks.

```java
import java.util.concurrent.locks.ReentrantLock;

class SharedResource {
    private int count = 0;
    private final ReentrantLock lock = new ReentrantLock();

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock();
        }
    }

    public int getCount() {
        lock.lock();
        try {
            return count;
        } finally {
            lock.unlock();
        }
    }
}

public class LockingExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Create multiple threads to operate on shared resource
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                sharedResource.increment();
            }
        });

        // Start threads
        thread1.start();
        thread2.start();

        try {
            // Wait for threads to finish execution
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Get the final value of the shared resource
        int finalCount = sharedResource.getCount();
        System.out.println("Final Count: " + finalCount);
    }
}
```

This code uses `ReentrantLock` to provide explicit locking and unlocking mechanisms, allowing more flexible control over the lock's granularity and behavior compared to the `synchronized` keyword.

### 5. Semaphore

- **Meaning**: A semaphore is a synchronization mechanism used to control the concurrent access of multiple threads.
- **Example Code**: Using Java's `Semaphore` class to limit access to a resource.

```java
import java.util.concurrent.Semaphore;

class SharedResource {
    private int count = 0;
    private final Semaphore semaphore = new Semaphore(1);

    public void increment() throws InterruptedException {
       

 semaphore.acquire();
        try {
            count++;
        } finally {
            semaphore.release();
        }
    }

    public int getCount() throws InterruptedException {
        semaphore.acquire();
        try {
            return count;
        } finally {
            semaphore.release();
        }
    }
}

public class SemaphoreExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Create multiple threads to operate on shared resource
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                try {
                    sharedResource.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                try {
                    sharedResource.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        // Start threads
        thread1.start();
        thread2.start();

        try {
            // Wait for threads to finish execution
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Get the final value of the shared resource
        int finalCount = sharedResource.getCount();
        System.out.println("Final Count: " + finalCount);
    }
}
```

In this example, a semaphore with a single permit (value of 1) is used to ensure that only one thread accesses the shared resource at a time.

### 6. Monitor

- **Meaning**: A monitor is a high-level synchronization mechanism that includes locks and condition variables used to manage thread access to shared resources.
- **Example Code**: Java's object monitors are composed of the `synchronized` keyword and the `wait()`, `notify()`, `notifyAll()` methods.

```java
class SharedResource {
    private int count = 0;

    public synchronized void increment() throws InterruptedException {
        while (count >= 100) {
            wait(); // Wait for condition to be satisfied
        }
        count++;
        notifyAll(); // Notify waiting threads
    }

    public synchronized void decrement() throws InterruptedException {
        while (count <= 0) {
            wait(); // Wait for condition to be satisfied
        }
        count--;
        notifyAll(); // Notify waiting threads
    }

    public synchronized int getCount() {
        return count;
    }
}

public class MonitorExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Producer thread
        Thread producer = new Thread(() -> {
            try {
                for (int i = 0; i < 100; i++) {
                    sharedResource.increment();
                    System.out.println("Produced: " + sharedResource.getCount());
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        // Consumer thread
        Thread consumer = new Thread(() -> {
            try {
                for (int i = 0; i < 100; i++) {
                    sharedResource.decrement();
                    System.out.println("Consumed: " + sharedResource.getCount());
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        producer.start();
        consumer.start();

        try {
            producer.join();
            consumer.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

This example uses the `synchronized` keyword and wait-notify mechanism to implement thread synchronization and coordination. The `wait()` and `notifyAll()` methods allow threads to wait for specific conditions to be met and to notify other waiting threads when conditions are met.

### 7. Race Condition

- **Meaning**: A race condition occurs in a multithreaded environment when the program's outcome depends on the order of thread execution rather than the code logic.
- **Example Code**: Multiple threads concurrently modifying shared resources without proper synchronization can lead to race conditions.

```java
class RaceConditionExample {
    private static int sharedValue = 0;

    public static void main(String[] args) {
        Runnable incrementTask = () -> {
            for (int i = 0; i < 100000; i++) {
                synchronized (RaceConditionExample.class) {
                    sharedValue++;
                }
            }
        };

        Thread thread1 = new Thread(incrementTask);
        Thread thread2 = new Thread(incrementTask);

        thread1.start();
        thread2.start();

        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final sharedValue: " + sharedValue);
    }
}
```

To solve the race condition, use the `synchronized` keyword to lock the shared resource, ensuring only one thread accesses the critical section at a time.

### 8. Inter-Thread Communication

- **Meaning**: Inter-thread communication refers to the process of passing information, sharing data, or collaborating on tasks between multiple threads.
- **Example Code**: Using Java's `Lock` and `Condition` interfaces to implement thread communication.

```java
import java.util.concurrent.locks.*;

class SharedResource {
    private int sharedCounter = 0;
    private final Lock lock = new ReentrantLock();
    private final Condition condition = lock.newCondition();

    public void increment() throws InterruptedException {
        lock.lock();
        try {
            while (sharedCounter >= 100) {
                condition.await(); // Wait for condition to be satisfied
            }
            sharedCounter++;
            condition.signalAll(); // Notify waiting threads
        } finally {
            lock.unlock();
        }
    }

    public void decrement() throws InterruptedException {
        lock.lock();
        try {
            while (sharedCounter <= 0) {
                condition.await(); // Wait for condition to be satisfied
            }
            sharedCounter--;
            condition.signalAll(); // Notify waiting threads
        } finally {
            lock.unlock();
        }
    }

    public int getSharedCounter() {
        return sharedCounter;
    }
}

public class InterThreadCommunicationExample {
    public static void main(String[] args) {
        SharedResource sharedResource = new SharedResource();

        // Producer thread
        Thread producer = new Thread(() -> {
            try {
                for (int i = 0; i < 100; i++) {
                    sharedResource.increment();
                    System.out.println("Produced: " + sharedResource.getSharedCounter());
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        // Consumer thread
        Thread consumer = new Thread(() -> {
            try {
                for (int i = 0; i < 100; i++) {
                    sharedResource.decrement();
                    System.out.println("Consumed: " + sharedResource.getSharedCounter());
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        producer.start();
        consumer.start();

        try {
            producer.join();
            consumer.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

This example uses the `Lock` and `Condition` interfaces to achieve inter-thread communication, ensuring that threads coordinate access to shared resources and avoid race conditions and unpredictable results.