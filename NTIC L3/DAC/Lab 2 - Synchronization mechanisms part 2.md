# 🧵 **Synchronization in Java (Part 2) — Atomic Variables & Producer–Consumer**

## 1) What is Synchronization? 🤔

When two or more threads share a resource (like a variable), their actions can overlap and cause **incorrect results**.  
Synchronization ensures **threads don’t conflict** when accessing shared data.

---

## 2) Atomic Variables ⚛️

Java gives us special classes in  
`java.util.concurrent.atomic`  
that allow **thread-safe operations without using `synchronized`**.

### ⭐ Example: `AtomicInteger`

```java
AtomicInteger garlicCount = new AtomicInteger(0);
garlicCount.incrementAndGet();   // Increases value safely
```

### ✅ Why it’s safe

`incrementAndGet()` does 3 steps **in one uninterruptible action**:

|Step|Action|
|---|---|
|1️⃣|Read the current value|
|2️⃣|Add 1|
|3️⃣|Store the new value|

No thread can interrupt this sequence → **No race condition** 🎉

---

# 🧑‍🌾 Two Shoppers Example (Recap)

```java
class Shopper extends Thread {
    static AtomicInteger garlicCount = new AtomicInteger(0);

    public void run() {
        for(int i = 0; i < 10_000_000; i++)
            garlicCount.incrementAndGet();
    }
}
```

Two threads add garlic at the same time → still accurate result ✅

---

# 🏭 Producer–Consumer Problem

## Scenario 🎬

We have a **warehouse** that can hold **up to 5 items**.

- **Producer** ➕ Adds items
    
- **Consumer** ➖ Removes items
    

They both run at the same time, so we must avoid:

- Adding when full ❌
    
- Removing when empty ❌
    
- Incorrect values ❌
    

---

# ✅ **Correct Solution Using `AtomicInteger`**

```java
package LAB2;
import java.util.concurrent.atomic.AtomicInteger;

class Warehouse {
    static final int CAPACITY = 5; 
    static AtomicInteger stock = new AtomicInteger(0); // shared counter
}

// Producer thread
class Producer extends Thread {
    public void run() {
        for (int i = 0; i < 10; i++) {
            if (Warehouse.stock.get() < Warehouse.CAPACITY) {
                int newStock = Warehouse.stock.incrementAndGet();
                System.out.println("👷 Producer added a product | Items = " + newStock);
            } else {
                System.out.println("⏳ Warehouse FULL! Producer waiting...");
            }

            try { Thread.sleep(100); } catch (InterruptedException e) {}
        }
    }
}

// Consumer thread
class Consumer extends Thread {
    public void run() {
        for (int i = 0; i < 10; i++) {
            if (Warehouse.stock.get() > 0) {
                int newStock = Warehouse.stock.decrementAndGet();
                System.out.println("🧾 Consumer removed a product | Items = " + newStock);
            } else {
                System.out.println("⏳ Warehouse EMPTY! Consumer waiting...");
            }

            try { Thread.sleep(120); } catch (InterruptedException e) {}
        }
    }
}

public class ProducerConsumerAtomicV1 {
    public static void main(String[] args) throws InterruptedException {
        Producer producer = new Producer();
        Consumer consumer = new Consumer();

        producer.start();
        consumer.start();

        producer.join();
        consumer.join();

        System.out.println("\n✅ Final items in warehouse = " + Warehouse.stock.get());
    }
}
```

---

# 🧩 Critical Section (Important!)

These lines modify shared data → **they must be protected**:

```java
Warehouse.stock.incrementAndGet();
Warehouse.stock.decrementAndGet();
```

---

# 🛡️ Synchronization Technique Used

**Technique:** `AtomicInteger`  
**How it works:** Uses **low-level CPU instructions (CAS)** to ensure updates happen **atomically** → no two threads can corrupt the value.

---

# 🧪 What Happens _Without_ Synchronization?

If we used:

```java
static int stock = 0;
stock++; // ❌ not atomic
```

We could get:

```
Producer added product | Items = 1
Consumer removed product | Items = 1  ← ❌ should be 0
Producer added product | Items = 3  ← ❌ capacity exceeded!
Final stock = 2  ← ❌ incorrect result
```

This is called a **race condition** 🏎️💥

---

# 🎯 Summary

|Concept|Meaning|
|---|---|
|AtomicInteger|Allows safe variable updates without locks|
|Critical Section|Code that changes shared data|
|Producer/Consumer Problem|Two threads sharing warehouse storage|
|Without Synchronization|Data becomes inconsistent|

---

If you'd like, I can now:  
✅ Convert this into a **PowerPoint**  
✅ Make a **diagram**  
✅ Create a **quiz** to study  
✅ Or rewrite it in **French / Arabic**

Which do you want? 😊

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAC/DAC|◀ DAC]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
