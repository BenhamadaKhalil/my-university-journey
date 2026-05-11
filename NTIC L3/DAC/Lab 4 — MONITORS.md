# 🧵 Lab Session 4 — MONITORS (Summary + Code)

---

## 🧠 Monitor — Core Pattern

### Explanation

A monitor combines:

- Mutual exclusion (one thread at a time)
    
- Condition variables (`await`, `signal`)
    

All shared data is accessed **only inside monitor methods**.

### Code Pattern

```java
Lock lock = new ReentrantLock();
Condition condition = lock.newCondition();

lock.lock();
try {
    while (!conditionSatisfied)
        condition.await();
    // critical section
    condition.signal();
} finally {
    lock.unlock();
}
```

---

## 🧪 Exo 1 — Computer Workshop Monitor (Priority Students)

### Explanation

- Suppliers add parts
    
- Employees assemble laptops
    
- Students buy laptops with **priority**
    
- Other clients wait if students are waiting
    

Priority is implemented using **shared state**, not semaphores.

---

### Monitor Code

```java
class WorkshopMonitor {

    private int stockParts = 0;
    private int stockLaptops = 0;
    private int waitingStudents = 0;

    private Lock lock = new ReentrantLock();
    private Condition partsAvailable = lock.newCondition();
    private Condition laptopsAvailable = lock.newCondition();

    // Supplier
    public void deliverParts(int qty) {
        lock.lock();
        try {
            stockParts += qty;
            partsAvailable.signalAll();
        } finally {
            lock.unlock();
        }
    }

    // Employee
    public void assembleLaptop() throws InterruptedException {
        lock.lock();
        try {
            while (stockParts == 0)
                partsAvailable.await();

            stockParts--;
            stockLaptops++;
            laptopsAvailable.signalAll();
        } finally {
            lock.unlock();
        }
    }

    // Student (priority)
    public void buyLaptopStudent() throws InterruptedException {
        lock.lock();
        try {
            waitingStudents++;
            while (stockLaptops == 0)
                laptopsAvailable.await();

            stockLaptops--;
            waitingStudents--;
            laptopsAvailable.signalAll();
        } finally {
            lock.unlock();
        }
    }

    // Other client
    public void buyLaptopClient() throws InterruptedException {
        lock.lock();
        try {
            while (stockLaptops == 0 || waitingStudents > 0)
                laptopsAvailable.await();

            stockLaptops--;
            laptopsAvailable.signalAll();
        } finally {
            lock.unlock();
        }
    }
}
```

---

## 🧪 Exo 2 — Restaurant Monitor (Plates & Sinks)

### Explanation

- Plates (P) limit number of students eating
    
- Sinks (S) limit number washing hands
    
- Students must wash **before and after eating**
    

---

### Monitor Code

```java
class RestaurantMonitor {

    private int plates;
    private int sinks;

    private Lock lock = new ReentrantLock();
    private Condition plateAvailable = lock.newCondition();
    private Condition sinkAvailable = lock.newCondition();

    public RestaurantMonitor(int P, int S) {
        plates = P;
        sinks = S;
    }

    // Request Plate
    public void RP() throws InterruptedException {
        lock.lock();
        try {
            while (plates == 0)
                plateAvailable.await();
            plates--;
        } finally {
            lock.unlock();
        }
    }

    // Request Sink
    public void RS() throws InterruptedException {
        lock.lock();
        try {
            while (sinks == 0)
                sinkAvailable.await();
            sinks--;
        } finally {
            lock.unlock();
        }
    }

    // Release Sink
    public void RelS() {
        lock.lock();
        try {
            sinks++;
            sinkAvailable.signal();
        } finally {
            lock.unlock();
        }
    }

    // Release Plate
    public void RelP() {
        lock.lock();
        try {
            plates++;
            plateAvailable.signal();
        } finally {
            lock.unlock();
        }
    }
}
```

---

## 🧪 Exo 3 — Producer Consumer (Monitor Logic)

### Explanation

Must guarantee:

- Producer waits if buffer full
    
- Consumer waits if buffer empty
    
- Mutual exclusion
    

---

## 🧪 Exo 4 — Producer Consumer (Monitor Version)

### Explanation

- `notFull` → producer waits
    
- `notEmpty` → consumer waits
    
- Lock ensures exclusive access
    

---

### Monitor Code

```java
class SharedBuffer {

    private Queue<String> buffer = new LinkedList<>();
    private final int MAX = 5;

    private Lock lock = new ReentrantLock();
    private Condition notFull = lock.newCondition();
    private Condition notEmpty = lock.newCondition();

    public void push(String item) throws InterruptedException {
        lock.lock();
        try {
            while (buffer.size() == MAX)
                notFull.await();

            buffer.add(item);
            notEmpty.signal();
        } finally {
            lock.unlock();
        }
    }

    public String pop() throws InterruptedException {
        lock.lock();
        try {
            while (buffer.isEmpty())
                notEmpty.await();

            String item = buffer.remove();
            notFull.signal();
            return item;
        } finally {
            lock.unlock();
        }
    }

    public void doSmth(String item) {
        System.out.println("Processing " + item);
    }
}
```

---

## 🧪 Exo 4 — Producer Consumer (Semaphore Version)

### Explanation

Same logic, but implemented with semaphores instead of conditions.

---

### Code

```java
class SharedBufferSem {

    private Queue<String> queue = new LinkedList<>();
    private final int MAX = 5;

    private Semaphore mutex = new Semaphore(1);
    private Semaphore emptySlots = new Semaphore(MAX);
    private Semaphore fullSlots = new Semaphore(0);

    public void push(String item) throws InterruptedException {
        emptySlots.acquire();
        mutex.acquire();

        queue.add(item);

        mutex.release();
        fullSlots.release();
    }

    public String pop() throws InterruptedException {
        fullSlots.acquire();
        mutex.acquire();

        String item = queue.remove();

        mutex.release();
        emptySlots.release();
        return item;
    }
}
```

---

## 🧪 Condition Variable Demo — Turn-Based Execution

### Explanation

- Threads wait until it is **their turn**
    
- Condition variable controls execution order
    

---

### Code

```java
class HungryPerson extends Thread {

    private int id;
    private static int servings = 11;
    private static Lock lock = new ReentrantLock();
    private static Condition soupTaken = lock.newCondition();

    public HungryPerson(int id) {
        this.id = id;
    }

    public void run() {
        while (servings > 0) {
            lock.lock();
            try {
                while (id != servings % 5 && servings > 0)
                    soupTaken.await();

                if (servings > 0) {
                    servings--;
                    soupTaken.signalAll();
                }
            } catch (InterruptedException e) {
            } finally {
                lock.unlock();
            }
        }
    }
}
```

---

## 🔍 Obsidian Search Tips

Use keywords like:

```text
monitor
condition
await
signal
producer consumer
priority
```

---

If you want next:

- 📄 **Semaphore vs Monitor (code side-by-side)**
    
- 🧠 **Ultra-short exam memory sheet**
    
- ✍️ **Exam questions with model answers**
    

Just tell me 👌