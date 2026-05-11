# **📘 Chapter 1 – Introduction to Concurrency Programming**

---

## **1. Background 🖥️**

In early computers, only **one program** could run at a time. Later, **multitasking** appeared.  
**Multitasking** = switching quickly between tasks 🌀  
This made it **look like** several tasks were running at once, even though the CPU was just switching rapidly.

But multitasking had limits when programs became complex.

Then came **multithreading (تعدد الخيوط)**.

### ✅ What is a thread?

A **thread** is a small execution unit inside a program that can run independently.

Multiple threads allow a program to:

- Do things **at the same time**
    
- Use CPU cores more efficiently
    
- Be more **responsive (استجابة أسرع)**
    

> **Definition:**  
> **Concurrency (التزامن)** = the ability to divide a program into several parts that can run independently, maybe in different orders, **without changing the final result**.

---

## **2. Concurrency vs Parallelism ⚖️**

|Concept|Meaning|Simple Example|Arabic (العربية)|
|---|---|---|---|
|**Concurrency** (التزامن)|Tasks progress in overlapping time|A single cashier switching between customers quickly|"التركيز على تنظيم الوقت"|
|**Parallelism** (التوازي)|Tasks run **at the same exact time**|Multiple cashiers serving different customers simultaneously|"التركيز على السرعة"|

### 🎯 In short:

- **Concurrency** → managing **multiple tasks efficiently**
    
- **Parallelism** → executing **multiple tasks simultaneously**
    

---

## **3. Why Concurrency? 🤔**

Concurrency helps software to be:

|Goal|Meaning|Arabic|
|---|---|---|
|**Responsive**|App reacts quickly to user|سريع الاستجابة|
|**Efficient**|Uses CPU resources well|فعّال في استغلال الموارد|
|**Scalable**|Can handle many users/tasks|قابل للتوسع|

💡 Example:  
When browsing the web 🌐:

- One thread loads the text
    
- Another loads the images
    
- Another plays sound/video
    

---

## **4. Threads and Their Role 🧵🐝**

Think of threads like **workers** inside a company (the process):

- They **share**:
    
    - Same memory 🧠 (الذاكرة)
        
    - Same code 📜
        
    - Same data 🧩
        

> **Definition:**  
> A **Thread (خيط التنفيذ)** is the smallest runnable sequence of instructions in a program.

---

## **5. Process vs Thread ⚙️ vs 🧵**

|Feature|**Process (عملية)**|**Thread (خيط)**|
|---|---|---|
|Memory|Has **its own** memory|Shares memory with others|
|Cost|Heavy ⚓|Very lightweight 🪶|
|Communication|Hard|Easy (shared memory)|
|Example|Running **Chrome**|Each **tab** in Chrome|

### 🎨 Analogy:

- **Process** = A house 🏠
    
- **Threads** = People living inside the same house 👨‍👩‍👧‍👦
    

They share everything.

---

## **6. Execution Scheduling 🕒**

The **Scheduler (الجدول)** in the OS decides:

- Which thread runs
    
- For how long
    
- In what order
    

### Key Concepts:

|Term|Meaning|Arabic|
|---|---|---|
|**Ready Queue**|List of ready threads|قائمة الانتظار|
|**Time Slice / Quantum**|CPU time given to thread|شريحة زمنية|
|**Context Switch**|Save/restore thread state when switching|تبديل السياق|
|**Preemptive Scheduling**|Interrupt a running thread for a more important one|جدولة استباقية|

---

## **7. Thread Lifecycle 🔄**

|State|Description|Arabic|
|---|---|---|
|**New**|Thread created but not started|جديد|
|**Runnable**|Ready and waiting for CPU|قابل للتشغيل|
|**Running**|Executing right now|قيد التنفيذ|
|**Blocked**|Waiting for a resource (e.g., file)|محجوب|
|**Waiting**|Waiting for another thread|انتظار|
|**Timed-Waiting**|Waiting for a fixed time|انتظار مؤقت|
|**Terminated**|Finished|منتهي|

---

## **8. Creating Threads in Java ☕**

### **✅ Method 1: Implement Runnable (preferred)**

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Hello from the thread!");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start();
    }
}
```

### **✅ Method 2: Extend Thread**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Hello from the thread!");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start();
    }
}
```

### Which is Better? 🤓

|Implement Runnable|Extend Thread|
|---|---|
|More flexible ✅|Less flexible ❌|
|Follows OOP composition 🎯|Uses inheritance 🧱|
|Recommended ✔️|Use only if necessary|

---
