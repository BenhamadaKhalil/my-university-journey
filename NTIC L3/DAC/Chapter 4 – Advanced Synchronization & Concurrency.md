# 🎓 **Chapter 4 – Advanced Synchronization & Concurrency**

In this chapter, we learn how to control **multiple threads** when they work on **shared data**, to avoid errors like **race conditions (تسابق البيانات)**.

---

## 🔐 1) **Monitors (المراقب)**

A **Monitor** ensures that **only one thread at a time** enters the **critical section (الجزء الحرج)** where shared data is used.  
It also allows threads to **wait** and **signal** each other.

---

## 🧱 2) **Object Monitor (المراقب الداخلي للكائن)**

Every Java object has a **built-in lock (قفل داخلي)** used with `synchronized`.

### Key Methods:

|Method|Meaning|ترجمة|
|---|---|---|
|`wait()`|Thread pauses and releases lock|ينتظر حتى يتم الإشعار|
|`notify()`|Wake **one** waiting thread|إشعار خيط واحد|
|`notifyAll()`|Wake **all** waiting threads|إشعار جميع الخيوط|

### Example 🧑‍🤝‍🧑

```java
class SharedData {
    synchronized void waitingMethod() throws InterruptedException {
        wait(); // (ينتظر)
    }

    synchronized void notifyMethod() {
        notify(); // (يوقظ خيط واحد)
    }
}
```

---

## 🛠 3) **Condition Variable Monitor (مراقب المتغير الشرطي)**

Condition Variable Monitors offer **more flexibility** compared to object monitors.  
They use **explicit locks** instead of intrinsic object locks.

✅ We use:

- `ReentrantLock` → القفل
    
- `Condition` → المتغير الشرطي (قائمة انتظار للخيوط)
    

You can have **multiple conditions on the same lock**.

### Main Methods:

|Method|Function|Description|
|---|---|---|
|`await()`|Wait|The thread waits until another thread signals the condition|
|`signal()`|Wake one|Notifies **one** waiting thread to re-check the condition|
|`signalAll()`|Wake all|Notifies **all** waiting threads to re-check the condition|

### Example 🔄

```java
ReentrantLock lock = new ReentrantLock();
Condition condition = lock.newCondition();

lock.lock();
try {
    while (!conditionMet()) {
        condition.await(); // Thread waits until signaled
    }
    // Code to execute when condition is met
} finally {
    lock.unlock();
}
```

### Object Monitor vs Condition Variable Monitor

|Feature|Object Monitor (`synchronized` + wait/notify)|Condition Variable Monitor (`Lock + Condition`)|
|---|---|---|
|Lock Type|Implicit|Explicit|
|Conditions|One wait queue|Multiple conditions allowed|
|Flexibility|Less flexible|More control over signaling|
|Usage|Simple synchronization|Fine-grained thread coordination|

---

## 🚦 4) **Semaphore (المسبار / إشارة التحكم)**

Controls **how many threads** can use a resource at the same time.

|Type|Meaning|مثال|
|---|---|---|
|**Counting Semaphore**|Allows _N_ threads|3 workers allowed|
|**Binary Semaphore**|Like a **mutex** (0 or 1)|1 worker allowed|

### Example 🚧

```java
Semaphore sem = new Semaphore(2);

sem.acquire();   // (يحجز)
System.out.println("Working...");
sem.release();   // (يفرج)
```

---

## 🍽 5) **Producer-Consumer Problem (مشكلة المنتج والمستهلك)**

|Role|Function|شرط|
|---|---|---|
|Producer (المنتج)|Adds items|Must wait if buffer is **full**|
|Consumer (المستهلك)|Removes items|Must wait if buffer is **empty**|

### Example using `wait()` / `notify()` 🛒

```java
class Buffer {
    private int item;
    private boolean available = false;

    public synchronized void produce(int value) throws InterruptedException {
        while(available) wait();
        item = value;
        available = true;
        notify();
    }

    public synchronized int consume() throws InterruptedException {
        while(!available) wait();
        available = false;
        notify();
        return item;
    }
}
```

---

## ⚠ 6) **Race Condition (حالة التسابق)**

Occurs when **two threads modify shared data at the same time**, causing **unexpected results (نتائج غير متوقعة)**.

**Solution:** Use synchronization tools:  
✅ `synchronized`  
✅ `Lock`  
✅ `Semaphore`

---

## 🧱 7) **Barrier (الحاجز)**

All threads reach a **meeting point**, then continue **together**.

```java
CyclicBarrier barrier = new CyclicBarrier(3);
barrier.await(); // (جميع الخيوط تنتظر)
```

---

## 🚪 8) **CountDownLatch (عدٍّ تنازلي انتظاري)**

Threads **wait** until a **counter reaches zero**.  
Unlike Barrier → **it cannot be reset**.

```java
CountDownLatch latch = new CountDownLatch(3);

latch.countDown(); // (يقترب للصفر)
latch.await();     // (ينتظر حتى الصفر)
```

---

# 🎯 **Quick Review Sheet**

|Concept|Purpose|Tool|
|---|---|---|
|Monitor|Mutual exclusion|`synchronized`|
|Condition Variable|Advanced waiting & signaling|`Lock + Condition`|
|Semaphore|Limit number of accessing threads|`Semaphore`|
|Producer-Consumer|Balanced data sharing|wait/notify / Condition|
|Race Condition|Wrong result due to timing|Synchronization|
|Barrier|Threads meet at checkpoint|`CyclicBarrier`|
|CountDownLatch|Wait until tasks finish|`countDown()` + `await()`|

---