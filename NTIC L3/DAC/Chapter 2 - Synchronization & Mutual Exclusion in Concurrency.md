# **🧵 Chapter: Synchronization & Mutual Exclusion in Concurrency**

---

## **1. Data Race (سباق البيانات) ⚠️**

A **Data Race** happens when:

- **Multiple threads** access the **same variable**
    
- **At the same time**
    
- And **at least one thread modifies it**
    

This causes **wrong / unpredictable results** ❌

### 🎯 Example Situation:

```text
Thread 1 is increasing counter
Thread 2 is also increasing counter
Both read the same value before update
Final result becomes incorrect
```

### 💬 Real Example:

```java
counter = counter + 1;
```

If two threads do this at the same time → result becomes **inconsistent (غير ثابت)**.

### ✅ How to Fix?

Use **Synchronization (المزامنة)** like:

- **Locks (الأقفال)**
    
- **Semaphores (السبمافور)**
    

These ensure **only one thread** updates the shared value at a time.

---

## **2. Critical Section (القسم الحرج) 🔒**

A **Critical Section** is a part of code where the program accesses **shared data**.

If **multiple threads** enter this section → **data corruption (فساد البيانات)** may happen.

### 🎯 Goal:

➡️ Allow **only ONE** thread at a time to enter this section.

Think of it like **one person bathroom 🚪**:  
If someone is inside → others must **wait**.

---

## **3. Mutual Exclusion (الاستبعاد المتبادل) 🚫🤝**

**Mutual Exclusion** means:

> Only **one thread** can access the **Critical Section** at any given time.

This idea was introduced by **Edsger Dijkstra** 🧠

### 🧠 Why is it necessary?

To prevent:

- Data inconsistency (عدم تناسق البيانات)
    
- Data race conditions
    
- Program errors
    

---

## **4. Locks (الأقفال) 🔐 — Implementing Mutual Exclusion**

A **Lock** acts like the **key to a private room**:

- If a thread holds the lock → It enters the **critical section**
    
- Other threads must **wait**
    

### 🎯 Key Concepts:

| Term                               | Meaning                                       | Arabic      |
| ---------------------------------- | --------------------------------------------- | ----------- |
| **lock()**                         | Request the lock                              | طلب القفل   |
| **unlock()**                       | Release the lock                              | تحرير القفل |
| **Atomic Operation (عملية ذرّية)** | Operation that happens entirely or not at all | لا تتجزأ    |

---

## **5. Reentrant Lock (القفل القابل لإعادة الدخول) 🔁**

Normally, **if a thread locks a mutex twice → DEADLOCK (تعليق)**.

But a **Reentrant Lock** allows the **same thread** to lock the same lock **multiple times** safely ✅

### ✅ Example (Java):

```java
Lock lock = new ReentrantLock();

lock.lock();
try {
    // critical code
    recursiveCall(); // function calls itself and locks again safely
} finally {
    lock.unlock();
}
```

---

## **6. `tryLock()` (قفل المحاولة) 🤞**

This is like **knocking on a door** 🚪

- If the lock is **available** → Take it → returns **true**
    
- If the lock is **busy** → Don’t wait → returns **false**
    

### ✅ Example:

```java
if (lock.tryLock()) {
    try {
        // Work safely
    } finally {
        lock.unlock();
    }
} else {
    System.out.println("Lock is busy, doing something else...");
}
```

This **prevents deadlock** and improves performance.

---

## **7. Read-Write Lock (قفل القراءة والكتابة) 📖✍️**

### 🧠 When is this useful?

When threads need to **read** shared data **more often** than writing.

|Operation|Allowed Threads|Arabic|
|---|---|---|
|**Read**|Many threads at the same time ✅|القراءة المتزامنة|
|**Write**|Only **one** thread at a time ❌|الكتابة المنفردة|

### ✅ Java Example:

```java
ReentrantReadWriteLock rwLock = new ReentrantReadWriteLock();
rwLock.readLock().lock();
// reading code
rwLock.readLock().unlock();

rwLock.writeLock().lock();
// writing code
rwLock.writeLock().unlock();
```

---

## **8. Atomic Variables (المتغيرات الذرّية) ⚡**

Instead of locking, we can use built-in **atomic types**:

- `AtomicInteger`
    
- `AtomicLong`
    
- `AtomicReference`
    

### ✅ Example:

```java
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet(); // Thread-safe ✔️
```

No locks needed → Faster ⚡

---

## **9. synchronized (متزامن) in Java 🔑**

Every Java object has an **intrinsic lock (قفل داخلي)**.

### **(A) Synchronized Method**

Only one thread can execute this **method** at a time.

```java
public synchronized void increment() {
    count++;
}
```

### **(B) Synchronized Block**

Synchronize only a **part** of code:

```java
synchronized (this) {
    count++;
}
```

This is **more efficient** as it locks less code.

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAC/DAC|◀ DAC]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
