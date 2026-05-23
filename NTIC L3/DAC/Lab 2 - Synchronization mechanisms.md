# 🧪 Lab Session 2 — Synchronization mechanisms

**Tags:** `#concurrency` `#threads` `#data-race` `#synchronization`

---

## ⚠️ Data race (سباق بيانات)

**Definition:** happens when

1. two or more threads access the same **shared variable**,
    
2. at least one thread **writes** to it, and
    
3. there is **no synchronization** (تزامن).  
    Result → **lost updates** and non-deterministic (غير حتمي) results.
    

**Mini example**

```java
// two threads increment a shared counter without sync
class Shopper extends Thread {
  static int garlicCount = 0;
  public void run() {
    for (int i=0; i<10_000_000; i++) garlicCount++;
  }
}
```

You expect `20_000_000` but get a smaller, different number each run.

---

## 🔍 Why it happens (atomicity issue)

`garlicCount++` is **not atomic** — it is 3 steps:

1. read value, 2. add 1, 3. write back.  
    If two threads interleave these steps, one update can overwrite the other → **lost update**.
    

---

## 🛠️ Fixes / Synchronization techniques (طرق التزامن)

### 1) Synchronized statement — class-level lock (قفل على مستوى الصنف)

```java
synchronized (Shopper.class) {
  garlicCount++;
}
```

- Locks the `Class` object (`Shopper.class`) → one lock shared by all instances.
    
- Ensures **mutual exclusion** (تبادلية المنع).
    

---

### 2) Synchronized statement — object-level lock (قفل كائن مشترك)

```java
static Object pencil = new Object();
synchronized (pencil) {
  garlicCount++;
}
```

- You create a dedicated lock object (`pencil`) and sync on it.
    
- Good practice: use a private static lock instead of synchronizing on `this` or public objects.
    

---

### 3) Synchronized method — method-level synchronization (تزامن على مستوى الدالة)

```java
private static synchronized void addGarlic() {
  garlicCount++;
}
```

- `static synchronized` → locks on `Class` object (`Shopper6.class`).
    
- `synchronized` (non-static) → locks on the instance (`this`).
    

---

### 4) Atomic variables (`AtomicInteger`) — lock-free atomic ops (عمليات ذرية بدون قفل)

```java
static AtomicInteger garlicCount = new AtomicInteger(0);
garlicCount.incrementAndGet();
```

- `incrementAndGet()` is atomic (ذرية).
    
- Faster than `synchronized` in many cases; great for simple counters.
    

---

### 5) ReentrantLock (explicit lock) — more control (قفل مع إمكانيات إضافية)

```java
ReentrantLock lock = new ReentrantLock();
lock.lock();
try {
  garlicCount++;
} finally {
  lock.unlock();
}
```

- Provides extra features: `tryLock()`, fairness policy, interruptible waits.
    

---

## 🔁 The `join()` remark (انتظار انتهاء الخيط)

- `t.join()` → main thread waits until `t` finishes.
    
- `join()` can throw `InterruptedException` → either `throws InterruptedException` or handle with `try/catch`.
    

---

## 🧾 Bank example (critical section) — summary

Critical section: code that **reads/writes shared data** — must be protected.  
Example critical lines:

- `balance += amount;`
    
- `balance -= amount;`
    

**Ways to protect**

- synchronized block on class / object
    
- synchronized methods
    
- Atomic types or ReentrantLock for fine control
    

---

## ✅ Quick decision guide

- Need a **simple counter** → use `AtomicInteger`.
    
- Need to protect **multiple related operations** (multiple fields) → use `synchronized` or `ReentrantLock`.
    
- Need **fairness** or `tryLock` → `ReentrantLock`.
    
- Avoid synchronizing on publicly accessible objects (risk of external interference).
    

---

## 🔁 Demonstration checklist (for the lab)

1. Run unsynchronized `Shopper` → observe < `20_000_000`.
    
2. Add `synchronized (Shopper.class)` → expect `20_000_000`.
    
3. Try `AtomicInteger` → expect `20_000_000` and better performance.
    
4. Show `join()` usage and `InterruptedException` handling.
    

---

## 🧠 Terminology quick translations (مصطلحات مهمة)

- Data race = سباق بيانات
    
- Synchronization = تزامن
    
- Atomic / atomicity = ذري / ذَرِيَّة
    
- Critical section = القسم الحرج
    
- Monitor lock = قفل المراقب
    
- Mutual exclusion (mutex) = تبادلية المنع
    

---

## ⚡ Short tips

- Prefer immutable data when possible.
    
- Minimize critical-section length (keep `synchronized` blocks small).
    
- Prefer `Atomic*` for single-variable counters.
    
- Use thread-safe collections (`ConcurrentHashMap`, etc.) when working with collections.
    

---
Great — let's solve both exercises clearly and simply, just like in your lab.

---

## ✅ **Exercise 1 — Husband/Wife Bank Account**

### **Program (with synchronization using `synchronized` method)**

```java
class BankAccount {
    private int balance = 0; // shared variable

    // Critical section → only one thread may execute this at a time
    public synchronized void deposit(int amount) {
        balance += amount;
        System.out.println("Husband deposited: " + amount + " | Balance = " + balance);
    }

    // Critical section → protects shared balance
    public synchronized void withdraw(int amount) {
        balance -= amount;
        System.out.println("Wife withdrew: " + amount + " | Balance = " + balance);
    }

    public int getBalance() {
        return balance;
    }
}

class Husband extends Thread {
    private BankAccount account;

    public Husband(BankAccount account) {
        this.account = account;
    }

    public void run() {
        for(int i = 0; i < 5; i++)
            account.deposit(1000);
    }
}

class Wife extends Thread {
    private BankAccount account;

    public Wife(BankAccount account) {
        this.account = account;
    }

    public void run() {
        for(int i = 0; i < 5; i++)
            account.withdraw(1000);
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        BankAccount account = new BankAccount();
        Husband h = new Husband(account);
        Wife w = new Wife(account);

        h.start();
        w.start();

        h.join();
        w.join();

        System.out.println("\nFinal Balance = " + account.getBalance());
    }
}
```

---

### **1️⃣ Critical Section**

The **critical sections** are:

```java
balance += amount;   // in deposit()
balance -= amount;   // in withdraw()
```

These modify the shared resource (`balance`).

---

### **2️⃣ Synchronization Technique Used**

**Method-level synchronization (`synchronized` methods)**

- When a thread enters a synchronized method, it **locks the object**.
    
- No other thread can run **any** synchronized method on the same object until the lock is released.
    
- This ensures **mutual exclusion**, preventing data races.
    

---

### **3️⃣ What Happens Without Synchronization?**

If we remove `synchronized`, both threads update `balance` **at the same time**.  
The result becomes **incorrect and random**. Example outputs:

```
Husband deposited 1000 | Balance = 1000
Wife withdrew 1000 | Balance = 0
Husband deposited 1000 | Balance = 1000
Wife withdrew 1000 | Balance = 0
...
Final Balance = -1000   (Incorrect!)
```

Because:

```
balance++ and balance-- are NOT atomic
```

---

## ✅ **Exercise 2 — Readers & Writers (Library Problem)**

### **Shared Resource:**

```java
static String book = "Initial Content";
```

### **Best Lock to Use:**

✅ **ReentrantReadWriteLock**

Why?

|Threads|Access|
|---|---|
|Many Readers|Can read **together** (no conflict)|
|Writers|Must have **exclusive access**|

A **ReentrantLock** allows only one thread at a time → not efficient for many readers.

---

### **Difference Between ReentrantLock and ReadWriteLock**

|Feature|ReentrantLock|ReadWriteLock|
|---|---|---|
|Readers|Only **one reader** allowed at a time|**Multiple readers** can read together|
|Writers|Exclusive|Exclusive|
|Efficiency|Lower when mostly reading|**High efficiency** when many reads|

---

### **Code Example Using ReadWriteLock**

```java
import java.util.concurrent.locks.*;

public class Library {
    static String book = "Java Concurrency Basics";
    static ReadWriteLock lock = new ReentrantReadWriteLock();

    static class Reader extends Thread {
        public void run() {
            lock.readLock().lock();
            try {
                System.out.println(getName() + " is reading: " + book);
                Thread.sleep((int)(Math.random()*500));
            } catch (Exception e) {}
            finally {
                lock.readLock().unlock();
            }
        }
    }

    static class Writer extends Thread {
        public void run() {
            lock.writeLock().lock();
            try {
                book = "Updated by " + getName();
                System.out.println(getName() + " wrote in the book.");
                Thread.sleep((int)(Math.random()*800));
            } catch (Exception e) {}
            finally {
                lock.writeLock().unlock();
            }
        }
    }

    public static void main(String[] args) {
        for(int i=0; i<5; i++) new Reader().start();
        for(int i=0; i<2; i++) new Writer().start();
    }
}
```

---

### **If a Writer Has Another Task and Doesn’t Want to Block**

Use:

```
tryLock()
```

Example:

```java
if(lock.writeLock().tryLock()) {
    // write
} else {
    // do another task instead of waiting (non-blocking)
}
```

---

## 🎯 Summary

|Concept|Explanation|
|---|---|
|Critical Section|Shared variable update area|
|Synchronization Used|`synchronized` method|
|Without Sync|Incorrect results due to data race|
|Best Lock (Readers/Writers)|`ReadWriteLock`|
|Key Advantage|Allows many readers simultaneously|
|Avoid writer blocking|Use `tryLock()`|

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAC/DAC|◀ DAC]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
