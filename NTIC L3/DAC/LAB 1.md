# 🟨 **Exercise 01**

### 🎯 Goal

Create **two threads**:

- Thread 1 → prints **1 to 5** with 500ms pause.
    
- Thread 2 → prints **A to E** with 700ms pause.
    
- Start both threads → they run **in parallel (بالتوازي)**.
    

### ✅ Solution

```java
public class Ex1 {

    static class NumberThread extends Thread {
        public void run() {
            for(int i = 1; i <= 5; i++) {
                System.out.println(i);
                try { Thread.sleep(500); }  // sleep = توقف مؤقت
                catch(Exception e) {}
            }
        }
    }

    static class LetterThread extends Thread {
        public void run() {
            for(char c = 'A'; c <= 'E'; c++) {
                System.out.println(c);
                try { Thread.sleep(700); }
                catch(Exception e) {}
            }
        }
    }

    public static void main(String[] args) {
        new NumberThread().start(); // start() = تشغيل خيط جديد
        new LetterThread().start();
    }
}
```

---

# 🟩 **Exercise 02**

### 🎯 Goal

- Create a child thread that **calculates the sum between a and b (excluding them)**.
    
- The main thread waits using `join()` then prints the result.
    

### ✅ Solution

```java
public class Ex2 {

    static class SumThread extends Thread {
        int a, b, result = 0;

        public SumThread(int a, int b) { this.a = a; this.b = b; }

        public void run() {
            for(int i = a + 1; i < b; i++) result += i;
        }
    }

    public static void main(String[] args) throws Exception {
        int a = 3, b = 8;

        SumThread t = new SumThread(a, b);
        t.start();
        t.join(); // join() = انتظار انتهاء الخيط

        System.out.println("Result = " + t.result);
        System.out.println("Main thread ID = " + Thread.currentThread().getId());
        System.out.println("Child thread ID = " + t.getId());
    }
}
```

### 🧠 Notes

|Item|Explanation|
|---|---|
|Number of threads|**2** (main + child)|
|`join()`|Makes main wait for the child|
|`getId()`|Returns thread ID|

---

# 🟦 **Exercise 03**

### 🎯 Goal

- Parent prints its ID.
    
- Child prints its ID **and** parent's ID.
    

### ✅ Solution

```java
public class Ex3 {

    static class ChildThread extends Thread {
        long parentId;

        public ChildThread(long parentId) { this.parentId = parentId; }

        public void run() {
            System.out.println("Child ID = " + getId() + ", Parent ID = " + parentId);
        }
    }

    public static void main(String[] args) {
        long parentId = Thread.currentThread().getId();
        System.out.println("Parent ID = " + parentId);

        new ChildThread(parentId).start();
    }
}
```

---

# 🟧 **Exercise 04**

### 🎯 Goal

Compute the expression:

```
(a + b) / (c * d)
```

- Thread 1 (extends Thread) → computes `a + b`
    
- Thread 2 (implements Runnable) → computes `c * d`
    
- Main thread prints final result.
    

### ✅ Solution

```java
public class Ex4 {

    static class SumThread extends Thread {
        double a, b, result;
        public SumThread(double a, double b) { this.a = a; this.b = b; }
        public void run() { result = a + b; }
        public double getResult() { return result; }
    }

    static class ProductRunnable implements Runnable {
        double c, d, result;
        public ProductRunnable(double c, double d) { this.c = c; this.d = d; }
        public void run() { result = c * d; }
        public double getResult() { return result; }
    }

    public static void main(String[] args) throws Exception {
        double a = 10, b = 5, c = 2, d = 3;

        SumThread t1 = new SumThread(a, b);
        ProductRunnable pr = new ProductRunnable(c, d);
        Thread t2 = new Thread(pr);

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        double result = t1.getResult() / pr.getResult();
        System.out.println("Final result = " + result);
    }
}
```

---

# 🟥 **Exercise 05 — Data Race (تنافس على البيانات)**

### ⚠️ Definition

A **data race** happens when:

1. Two threads access the **same shared variable**.
    
2. At least one thread **modifies** it.
    
3. There is **no synchronization** → unpredictable results.
    

### ✅ Solution (Example)

```java
public class Ex5 {

    static int counter = 0; // Shared variable (متغير مشترك)

    static class Worker extends Thread {
        public void run() {
            for(int i = 0; i < 1_000_000; i++)
                counter++; // Not synchronized → data race
        }
    }

    public static void main(String[] args) throws Exception {
        Worker t1 = new Worker();
        Worker t2 = new Worker();

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Counter = " + counter);
    }
}
```

### 🔍 Why this is a Data Race?

- Both threads **change** the same variable **at the same time**.
    
- No `synchronized`, no lock → **lost updates** → incorrect result.
    

---

## ✅ Done

All 5 exercises explained clearly, clean code, no unnecessary output.

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAC/DAC|◀ DAC]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
