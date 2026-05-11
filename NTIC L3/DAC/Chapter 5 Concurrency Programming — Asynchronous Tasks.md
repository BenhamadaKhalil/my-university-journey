# 🧵 Concurrency Programming — Asynchronous Tasks (Lesson Summary)

## 1️⃣ What Are Asynchronous Tasks?

An **asynchronous task** is a task that can run **independently** of other tasks, **without waiting** for them to finish.

👉 Multiple tasks can execute **in parallel**, depending on available processors (CPU cores).

### Simple Analogy (Salad Example)

- Chopping lettuce, tomatoes, cucumbers, onions…
    
- Each action is a **separate task**
    
- Tasks **do not need strict order**
    
- Each person = **thread**
    
- Knives/processors = **CPU cores**
    

➡ Tasks run **asynchronously** and possibly **in parallel**

---

## 2️⃣ Threads and Resource Limitations

- Programs may create **many threads**
    
- But the system has **limited processors**
    
- Excess threads will:
    
    - Wait for execution
        
    - Consume **memory**
        
    - Add **context-switching overhead**
        

⚠️ Creating a thread is **not free** (time + memory cost)

---

## 3️⃣ Thread Pool Concept

### ❓ Why Thread Pools?

Instead of creating a **new thread per task**, we:

- Create a **fixed number of worker threads**
    
- Reuse them for multiple tasks
    

### ✅ Advantages

- Reduces thread creation overhead
    
- Improves responsiveness
    
- Better CPU utilization
    
- Prevents resource exhaustion
    

🧠 **Rule**:

> If `task execution time < thread creation time`, use a **thread pool**

### How It Works

- Tasks are placed in a **queue**
    
- Worker threads:
    
    - Take a task
        
    - Execute it
        
    - Take the next one
        

---

## 4️⃣ ExecutorService (Java)

### ExecutorService Interface

- Located in `java.util.concurrent`
    
- High-level API for managing asynchronous tasks
    
- Abstracts thread creation and management
    

### Responsibilities

- Submit tasks
    
- Manage thread lifecycle
    
- Shut down executors gracefully
    

📌 You submit **tasks**, not threads

---

## 5️⃣ Runnable vs Callable

### Runnable

```java
public interface Runnable {
    void run();
}
```

- Does **not return a value**
    
- Cannot throw checked exceptions
    

### Callable

```java
public interface Callable<V> {
    V call() throws Exception;
}
```

- **Returns a result**
    
- Can throw exceptions
    

### Key Difference

|Runnable|Callable|
|---|---|
|No result|Returns a value|
|No exception|Can throw exception|

📌 Use **Callable** when you need a result from an async task

---

## 6️⃣ Future Interface

### ❓ Why Future?

When a task runs asynchronously:

- The result is **not immediately available**
    

➡ `Future` acts as a **placeholder** for the result.

### Characteristics

- Represents a **result that will be available later**
    
- Allows:
    
    - Checking if task is done
        
    - Waiting for the result
        
    - Retrieving the result
        

### IOU Analogy

- Thread A promises Thread B a result
    
- Thread B continues working
    
- Later, it checks the “IOU” (Future)
    

---

## 7️⃣ Divide and Conquer Algorithms

### Definition

A strategy where a problem is:

1. **Divided** into smaller subproblems
    
2. **Conquered** (solved recursively)
    
3. **Combined** to form the final solution
    

### Generic Algorithm

```text
If problem is simple:
    solve directly
Else:
    divide problem
    solve subproblems recursively
    combine results
```

### Applications

- Merge Sort
    
- Quick Sort
    
- Min / Max search
    
- Matrix multiplication
    
- Parallel computing
    

---

## 8️⃣ Fork/Join Framework (Java 7)

### Purpose

- Efficient **parallel execution**
    
- Designed for **divide-and-conquer algorithms**
    

### ForkJoinPool

- Specialized implementation of `ExecutorService`
    
- Uses **worker threads**
    
- Maximizes CPU utilization
    

### Core Operations

- **fork()** → Execute task asynchronously
    
- **join()** → Wait and retrieve result
    

---

## 9️⃣ ForkJoinTask Types

### 1. RecursiveTask

- Returns a result
    
- Implements `compute()`
    

### 2. RecursiveAction

- Does NOT return a result
    
- Implements `compute()`
    

📌 Choose based on whether a result is needed

---

## 🔟 Summary Table

|Concept|Purpose|
|---|---|
|Thread|Unit of execution|
|Thread Pool|Reuse threads efficiently|
|ExecutorService|Manage async tasks|
|Runnable|Task without result|
|Callable|Task with result|
|Future|Result placeholder|
|Divide & Conquer|Parallel problem-solving|
|ForkJoinPool|Parallel execution engine|

---

If you want next:

- ✅ **Java code examples**
    
- ✅ **Exam questions**
    
- ✅ **Comparison diagrams**
    
- ✅ **Obsidian-friendly flashcards**
    

Just tell me 👍