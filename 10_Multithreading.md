# 📚 JAVA NOTES - CHAPTER 10
## Multithreading

---

### ⭐ What is Multithreading?

**Multithreading:** Ability to execute multiple threads simultaneously within a single program

🔹 **Key Concepts:**
• **Process:** Independent program in execution
• **Thread:** Lightweight sub-process within a process
• **Multitasking:** Multiple processes running simultaneously
• **Multithreading:** Multiple threads within same process

**Benefits:**
• Better CPU utilization
• Improved performance
• Concurrent execution
• Responsive user interfaces

---

### 🔹 Thread vs Process

| Thread | Process |
|--------|---------|
| Lightweight | Heavyweight |
| Shares memory with other threads | Independent memory space |
| Fast context switching | Slow context switching |
| Low overhead | High overhead |
| Communication is easy | Communication is complex |
| If one thread crashes, others may be affected | If one process crashes, others are unaffected |

---

### ⭐ Thread Life Cycle

### 📊 Thread Life Cycle Diagram

```
Thread Life Cycle States:

    NEW
     │
     │ start()
     ↓
   RUNNABLE ←──────────────┐
     │                    │
     │ run()              │ notify()
     ↓                    │ notifyAll()
   RUNNING ────────────────┤
     │                    │
     │ sleep()            │
     │ wait()             │
     │ join()             │
     │ I/O operation      │
     ↓                    │
   BLOCKED/WAITING ───────┘
     │
     │ run() completes
     │ exception occurs
     ↓
 TERMINATED

Detailed State Transitions:

NEW ──start()──→ RUNNABLE ──scheduler──→ RUNNING
                     ↑                      │
                     │                      │
                     │                      ├─sleep()─→ TIMED_WAITING
                     │                      │              │
                     │                      │              │timeout
                     │                      │              ↓
                     │                      ├─wait()──→ WAITING
                     │                      │              │
                     │                      │              │notify()
                     │                      │              ↓
                     └──────────────────────┴──────────────┘
                                           │
                                           │run() ends
                                           ↓
                                      TERMINATED
```

### 🔹 Thread States Explained

1. **NEW:** Thread created but not started
2. **RUNNABLE:** Thread ready to run or running
3. **BLOCKED:** Thread blocked waiting for monitor lock
4. **WAITING:** Thread waiting indefinitely for another thread
5. **TIMED_WAITING:** Thread waiting for specified time
6. **TERMINATED:** Thread execution completed

---

### ⭐ Creating Threads

### 🔹 Method 1: Extending Thread Class

```java
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(1000);  // Sleep for 1 second
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted");
            }
        }
    }
}

public class ThreadExample1 {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        
        t1.setName("Thread-1");
        t2.setName("Thread-2");
        
        t1.start();  // Start thread 1
        t2.start();  // Start thread 2
    }
}
```

### 🔹 Method 2: Implementing Runnable Interface

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted");
            }
        }
    }
}

public class ThreadExample2 {
    public static void main(String[] args) {
        MyRunnable runnable = new MyRunnable();
        
        Thread t1 = new Thread(runnable, "Thread-1");
        Thread t2 = new Thread(runnable, "Thread-2");
        
        t1.start();
        t2.start();
    }
}
```

### 🔹 Method 3: Using Lambda Expression (Java 8+)

```java
public class ThreadExample3 {
    public static void main(String[] args) {
        // Using lambda expression
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Lambda Thread: " + i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    System.out.println("Thread interrupted");
                }
            }
        });
        
        t1.start();
    }
}
```

---

### ⭐ Thread Methods

### 🔹 Important Thread Methods

| Method | Description | Example |
|--------|-------------|---------|
| `start()` | Starts thread execution | `thread.start()` |
| `run()` | Contains thread logic | Override this method |
| `sleep(ms)` | Pauses thread for specified time | `Thread.sleep(1000)` |
| `join()` | Wait for thread to complete | `thread.join()` |
| `interrupt()` | Interrupts thread | `thread.interrupt()` |
| `isAlive()` | Check if thread is alive | `thread.isAlive()` |
| `getName()` | Get thread name | `thread.getName()` |
| `setName()` | Set thread name | `thread.setName("MyThread")` |
| `getPriority()` | Get thread priority | `thread.getPriority()` |
| `setPriority()` | Set thread priority | `thread.setPriority(5)` |
| `currentThread()` | Get current thread reference | `Thread.currentThread()` |

### 🔹 Thread Methods Example

```java
public class ThreadMethodsExample {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            System.out.println("Thread started: " + Thread.currentThread().getName());
            for (int i = 1; i <= 3; i++) {
                System.out.println("Count: " + i);
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    System.out.println("Thread was interrupted");
                    return;
                }
            }
            System.out.println("Thread completed");
        }, "WorkerThread");
        
        System.out.println("Thread state before start: " + t1.getState());
        t1.start();
        System.out.println("Thread state after start: " + t1.getState());
        
        try {
            t1.join();  // Wait for t1 to complete
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Thread state after completion: " + t1.getState());
        System.out.println("Main thread completed");
    }
}
```

---

### 🔹 Thread Priority

**Priority Levels:**
• `MIN_PRIORITY` = 1
• `NORM_PRIORITY` = 5 (default)
• `MAX_PRIORITY` = 10

```java
public class ThreadPriorityExample {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("High Priority Thread: " + i);
            }
        }, "HighPriorityThread");
        
        Thread t2 = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Low Priority Thread: " + i);
            }
        }, "LowPriorityThread");
        
        t1.setPriority(Thread.MAX_PRIORITY);  // 10
        t2.setPriority(Thread.MIN_PRIORITY);  // 1
        
        t1.start();
        t2.start();
    }
}
```

---

### ⭐ Thread Synchronization

**Problem:** Multiple threads accessing shared resources can cause data inconsistency

**Solution:** Synchronization ensures only one thread accesses shared resource at a time

### 🔹 Synchronized Method

```java
class Counter {
    private int count = 0;
    
    // Synchronized method
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

public class SynchronizedExample {
    public static void main(String[] args) {
        Counter counter = new Counter();
        
        // Create multiple threads that increment counter
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });
        
        t1.start();
        t2.start();
        
        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Final count: " + counter.getCount());  // Should be 2000
    }
}
```

### 🔹 Synchronized Block

```java
class BankAccount {
    private double balance = 1000.0;
    
    public void withdraw(double amount) {
        synchronized (this) {  // Synchronized block
            if (balance >= amount) {
                System.out.println(Thread.currentThread().getName() + 
                    " is withdrawing " + amount);
                balance -= amount;
                System.out.println("Remaining balance: " + balance);
            } else {
                System.out.println("Insufficient balance for " + 
                    Thread.currentThread().getName());
            }
        }
    }
    
    public double getBalance() {
        return balance;
    }
}
```

---

### 🔹 Inter-Thread Communication

**Methods for thread communication:**
• `wait()` - Thread waits until notified
• `notify()` - Wakes up one waiting thread
• `notifyAll()` - Wakes up all waiting threads

```java
class SharedResource {
    private int data;
    private boolean hasData = false;
    
    public synchronized void produce(int value) {
        while (hasData) {
            try {
                wait();  // Wait until data is consumed
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        
        data = value;
        hasData = true;
        System.out.println("Produced: " + value);
        notify();  // Notify consumer
    }
    
    public synchronized int consume() {
        while (!hasData) {
            try {
                wait();  // Wait until data is produced
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        
        hasData = false;
        System.out.println("Consumed: " + data);
        notify();  // Notify producer
        return data;
    }
}

public class ProducerConsumerExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        
        // Producer thread
        Thread producer = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                resource.produce(i);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        });
        
        // Consumer thread
        Thread consumer = new Thread(() -> {
            for (int i = 1; i <= 5; i++) {
                resource.consume();
                try {
                    Thread.sleep(1500);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        });
        
        producer.start();
        consumer.start();
    }
}
```

---

### ⭐ Thread Pool (Executor Framework)

**Benefits of Thread Pool:**
• Reuses existing threads
• Controls number of threads
• Better performance
• Easy thread management

```java
import java.util.concurrent.*;

public class ThreadPoolExample {
    public static void main(String[] args) {
        // Create thread pool with 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);
        
        // Submit tasks to thread pool
        for (int i = 1; i <= 10; i++) {
            final int taskId = i;
            executor.submit(() -> {
                System.out.println("Task " + taskId + " executed by " + 
                    Thread.currentThread().getName());
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            });
        }
        
        executor.shutdown();  // Shutdown thread pool
        
        try {
            if (!executor.awaitTermination(60, TimeUnit.SECONDS)) {
                executor.shutdownNow();
            }
        } catch (InterruptedException e) {
            executor.shutdownNow();
        }
    }
}
```

---

### 🔹 Common Thread Problems

### **1. Deadlock**
```java
class DeadlockExample {
    private static Object lock1 = new Object();
    private static Object lock2 = new Object();
    
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (lock1) {
                System.out.println("Thread 1: Holding lock 1");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized (lock2) {
                    System.out.println("Thread 1: Holding lock 1 & 2");
                }
            }
        });
        
        Thread t2 = new Thread(() -> {
            synchronized (lock2) {
                System.out.println("Thread 2: Holding lock 2");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized (lock1) {
                    System.out.println("Thread 2: Holding lock 1 & 2");
                }
            }
        });
        
        t1.start();
        t2.start();
    }
}
```

### **2. Race Condition**
```java
class RaceConditionExample {
    private static int counter = 0;
    
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter++;  // Not thread-safe
            }
        });
        
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter++;  // Not thread-safe
            }
        });
        
        t1.start();
        t2.start();
        
        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Counter: " + counter);  // May not be 2000
    }
}
```

---

### 📊 Thread Synchronization Mechanisms

```
Synchronization Mechanisms:

1. synchronized keyword
   ├── synchronized methods
   └── synchronized blocks

2. volatile keyword
   └── ensures visibility of changes

3. Locks (java.util.concurrent.locks)
   ├── ReentrantLock
   ├── ReadWriteLock
   └── StampedLock

4. Atomic classes (java.util.concurrent.atomic)
   ├── AtomicInteger
   ├── AtomicBoolean
   └── AtomicReference

5. Concurrent Collections
   ├── ConcurrentHashMap
   ├── CopyOnWriteArrayList
   └── BlockingQueue
```

---

### ⭐ Real-World Example: Download Manager

```java
import java.util.concurrent.*;

class FileDownloader implements Runnable {
    private String fileName;
    private int fileSize;
    
    public FileDownloader(String fileName, int fileSize) {
        this.fileName = fileName;
        this.fileSize = fileSize;
    }
    
    @Override
    public void run() {
        System.out.println("Starting download: " + fileName);
        
        for (int i = 0; i <= fileSize; i += 10) {
            try {
                Thread.sleep(100);  // Simulate download time
                int progress = Math.min(i, fileSize);
                System.out.println(fileName + " - Progress: " + 
                    (progress * 100 / fileSize) + "%");
            } catch (InterruptedException e) {
                System.out.println("Download interrupted: " + fileName);
                return;
            }
        }
        
        System.out.println("Download completed: " + fileName);
    }
}

public class DownloadManager {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);
        
        // Submit download tasks
        executor.submit(new FileDownloader("video.mp4", 100));
        executor.submit(new FileDownloader("music.mp3", 50));
        executor.submit(new FileDownloader("document.pdf", 30));
        executor.submit(new FileDownloader("image.jpg", 20));
        
        executor.shutdown();
        
        try {
            executor.awaitTermination(30, TimeUnit.SECONDS);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("All downloads completed!");
    }
}
```

---

**📝 Important Points:**
• Always use `start()` to begin thread execution, not `run()`
• Thread priority is just a hint to scheduler
• Synchronization prevents race conditions but can cause deadlocks
• Use thread pools for better resource management
• `volatile` keyword ensures visibility of variable changes
• `join()` method waits for thread completion
• Daemon threads terminate when all user threads finish

---

**⭐ Quick Tips for Exams:**
• Draw thread lifecycle diagram
• Remember thread states and transitions
• Know difference between `start()` and `run()`
• Understand synchronization concepts
• Practice producer-consumer problems
• Know common thread problems (deadlock, race condition)
• Remember thread pool benefits
• Practice inter-thread communication examples

---
*End of Chapter 10* ✅