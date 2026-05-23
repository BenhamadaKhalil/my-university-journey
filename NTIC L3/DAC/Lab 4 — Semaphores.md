# 🧵 Lab Session 4 — Semaphores

**Concurrency Programming — Constantine 2**

---

## 📘 0. Semaphore — Theory (Teacher Notes)

### Definition

A **semaphore** is a synchronization mechanism used to control access to shared resources in concurrent programs.

### Properties

- Integer counter
    
- Controls how many threads can access a resource
    
- Threads **wait automatically** when no permits are available
    

### Core Operations

- `acquire()` (P / wait)  
    → Decrements counter or blocks if zero
    
- `release()` (V / signal)  
    → Increments counter and wakes waiting threads
    

### Types

- **Binary Semaphore**
    
    - Value: 0 or 1
        
    - Used as a **mutex**
        
- **Counting Semaphore**
    
    - Value ≥ 0
        
    - Allows **N concurrent accesses**
        

📄 Source:

---

## 🧪 Exercise 1 — Basic Semaphore Usage (Mutex)

### Objective

Protect a shared variable using a **binary semaphore**

### Problem

- Shared counter
    
- 3 threads
    
- Each increments 1000 times
    

### Solution (Teacher)

```java
class CounterThread extends Thread {
    private static int counter = 0;
    private static Semaphore mutex = new Semaphore(1);

    public void run() {
        for (int i = 0; i < 1000; i++) {
            try {
                mutex.acquire();
                counter++;
            } finally {
                mutex.release();
            }
        }
    }

    public static int getCounter() {
        return counter;
    }
}
```

### Main

```java
Thread t1 = new CounterThread();
Thread t2 = new CounterThread();
Thread t3 = new CounterThread();
```

### Key Idea

- Semaphore ensures **mutual exclusion**
    
- Without it → race condition → wrong result
    

📄 Source:

---

## 🧪 Exercise 2 — Who Should Start First?

---

### 🔴 Part 1 — Without Semaphore (Incorrect)

#### Behavior

- Printer may execute **before increment finishes**
    

```java
static int counter = 0;

class Increment extends Thread {
    public void run() {
        for (int i = 0; i < 1_000_000; i++) {
            counter++;
        }
    }
}

class Print extends Thread {
    public void run() {
        System.out.println("Counter = " + counter);
    }
}
```

❌ Result: **Unpredictable**

📄 Source:

---

### 🟢 Part 2 — With Semaphore (Correct)

#### Idea

- Printer waits until increment finishes
    

### Solution

```java
static int counter = 0;
static Semaphore semaphore = new Semaphore(0);

class IncrementerThread extends Thread {
    public void run() {
        for (int i = 0; i < 1_000_000; i++) {
            counter++;
        }
        semaphore.release();
    }
}

class PrinterThread extends Thread {
    public void run() {
        try {
            semaphore.acquire();
            System.out.println("Counter = " + counter);
        } catch (InterruptedException e) {}
    }
}
```

### Key Point

- Semaphore used as **completion signal**
    

📄 Source:

---

## 🧪 Exercise 3 — Resource Limitation (Printers)

### Scenario

- 2 printers
    
- 5 people printing
    

### Semaphore

```java
static Semaphore printers = new Semaphore(2);
```

### Behavior

- Only **2 threads print simultaneously**
    
- Others wait automatically
    

```java
printers.acquire();
System.out.println(getName() + " imprime");
Thread.sleep(2000);
printers.release();
```

📄 Source:

---

## 🧪 Exercise 4 — Producer / Consumer

### Shared Data

- Buffer size = 5
    
- Circular buffer
    

### Semaphores Used

|Semaphore|Initial Value|Role|
|---|---|---|
|`empty`|5|empty slots|
|`full`|0|filled slots|
|`mutex`|1|critical section|

### Producer Logic

```java
empty.acquire();
mutex.acquire();
buffer[in] = item;
mutex.release();
full.release();
```

### Consumer Logic

```java
full.acquire();
mutex.acquire();
item = buffer[out];
mutex.release();
empty.release();
```

### Guarantees

- ❌ No overflow
    
- ❌ No underflow
    
- ✅ Safe concurrency
    

📄 Source:

---

## 🧪 Exercise 5 — Turn-Based Access

### Goal

Threads must execute **in order**:

```
Thread 0 → Thread 1 → Thread 2
```

### Semaphores

```java
Semaphore s0 = new Semaphore(1);
Semaphore s1 = new Semaphore(0);
Semaphore s2 = new Semaphore(0);
```

### Logic

Each thread:

1. Acquires its semaphore
    
2. Prints
    
3. Releases next semaphore
    

```java
current.acquire();
System.out.println("Thread " + id);
next.release();
```

---

# 🧵 Lab Session 4 — Semaphores

**PART 2: Exercises 6 → 12**

---

## 🧪 Exercise 6 — Parking Lot Simulation

### Scenario

- 10 parking spots
    
- 20 cars arrive randomly
    

### Semaphore

```java
Semaphore parking = new Semaphore(10);
```

### Car Behavior

1. Try to park → `acquire()`
    
2. Stay parked (sleep)
    
3. Leave → `release()`
    

### Key Idea

- When parking is full → cars **wait automatically**
    
- No car can park without a permit
    

📄 Source:

---

## 🧪 Exercise 7 — Restaurant with Limited Tables (VIP Priority)

### Scenario

- 5 normal tables
    
- 2 VIP tables
    
- VIP customers have priority
    

### Semaphores

```java
Semaphore tables = new Semaphore(5);
Semaphore vipTables = new Semaphore(2);
```

### Logic

- VIP customers acquire `vipTables`
    
- Normal customers acquire `tables`
    
- Each customer releases after eating
    

### Concept

- **Multiple semaphores = priority management**
    

📄 Source:

---

## 🧪 Exercise 8 — Airport Runway Management (Low Fuel Priority)

### Scenario

- 2 runways
    
- 10 planes
    
- Low-fuel planes have priority
    

### Semaphores

```java
Semaphore runways = new Semaphore(2);
Semaphore lowFuelMutex = new Semaphore(1);
```

### Priority Rule

- Low-fuel plane blocks normal planes
    
- Normal planes wait if priority active
    

### Pattern

- **Semaphore used as priority lock**
    

📄 Source:

---

## 🧪 Exercise 9 — Database Connection Pool

### Scenario

- N = 3 database connections
    
- 10 clients
    

### Semaphore

```java
Semaphore connections = new Semaphore(3);
```

### Client Steps

1. Acquire connection
    
2. Execute query
    
3. Release connection
    

### Guarantee

- Max **3 concurrent queries**
    
- No starvation
    

📄 Source:

---

## 🧪 Exercise 10 — Printer Pool (Multiple Documents)

### Scenario

- 3 printers
    
- Employees print **multiple documents**
    

### Semaphore

```java
Semaphore printers = new Semaphore(3, true); // FIFO
```

### Important Point

- Each document:
    
    - acquires printer
        
    - prints
        
    - releases printer
        
- FIFO ensures **fairness**
    

📄 Source:

---

## 🧪 Exercise 11 — Train Station Platform Management (Express Priority)

### Scenario

- 2 platforms
    
- Express trains have priority
    

### Semaphores

```java
Semaphore platforms = new Semaphore(2, true);
Semaphore expressMutex = new Semaphore(1);
```

### Behavior

- Express train:
    
    - blocks normal trains
        
    - acquires platform immediately
        
- Normal train:
    
    - waits if express is present
        

### Pattern

- **Priority using binary semaphore**
    

📄 Source:

---

## 🧪 Exercise 12 — Multi-Stage Factory Production Line

### Scenario

Items pass through **3 stages**, each with limited machines

|Stage|Machines|
|---|---|
|Stage 1|2|
|Stage 2|3|
|Stage 3|1|

### Semaphores

```java
Semaphore s1 = new Semaphore(2, true);
Semaphore s2 = new Semaphore(3, true);
Semaphore s3 = new Semaphore(1, true);
```

### Item Logic

Each item:

1. Acquire stage 1 → work → release
    
2. Acquire stage 2 → work → release
    
3. Acquire stage 3 → work → release
    

### Guarantee

- No stage overload
    
- Correct pipeline behavior
    

📄 Source:


---

## ✅ Summary Table

| Exercise | Pattern                  |
| -------- | ------------------------ |
| Exo 1    | Mutex (Binary Semaphore) |
| Exo 2    | Thread Ordering          |
| Exo 3    | Resource Limitation      |
| Exo 4    | Producer–Consumer        |
| Exo 5    | Turn-Based Execution     |

| 6   | Resource counting     |
| --- | --------------------- |
| 7   | Priority (VIP)        |
| 8   | Priority (Low fuel)   |
| 9   | Connection pool       |
| 10  | Fair resource sharing |
| 11  | Express priority      |
| 12  | Multi-stage pipeline  |

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAC/DAC|◀ DAC]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
