## ⚙️ Liveness (الحيوية في التنفيذ)

**Liveness** means the program continues to work and does **not get stuck**.  
In concurrent programming, some threads might block each other → causing problems.

---

## 🔒 Deadlock (تعارض وانتظار دائم)

Deadlock happens when **two or more threads are waiting for each other** and **no one continues**.

### 🧠 Example (Simple)

- Thread A needs Resource 1 and waits for Resource 2
    
- Thread B needs Resource 2 and waits for Resource 1  
    → Both **wait forever** ❌
    

### 🍽️ Dining Philosophers Problem

5 philosophers sitting around a table, each needs **two chopsticks** to eat.  
If **everyone picks one chopstick**, nobody can get the second → **deadlock**.

**Solution:** Use **locks, semaphores**, or protocol that forces **one philosopher to wait** before picking.

---

## 😔 Starvation (حرمان من الموارد)

Starvation occurs when **a thread never gets the resource it needs** because another thread **keeps using it**.

### 🧠 Example

A _greedy_ thread always gets CPU time → a small thread **never runs**.

---

## 🔁 Livelock (حركة بدون تقدم)

In **livelock**, threads are **not blocked**, they **keep responding to each other**, but **make no progress**.

### 🧠 Example

Two people in a hallway both move left → block → both move right → block → repeat forever 😅

> They are **active**, but **stuck**.

---

## 🛠️ Prevention Techniques (طرق الوقاية)

|Technique|Meaning|مثال (Example)|
|---|---|---|
|**Lock Ordering**|Always acquire locks in the **same order**|Always lock A → then B|
|**Timeouts**|Stop waiting after certain time|If lock not available → release + retry|
|**Limit Resource Requests**|A thread must **release before requesting more**|Prevent greedy threads|
|**Resource Preemption**|Take resource from lower priority thread to free system|Higher priority continues|

---

## 🎯 Quick Memory Recap

|Problem|Description|Threads Active?|Result|
|---|---|---|---|
|**Deadlock**|Threads wait forever|❌ No progress|Program stuck|
|**Starvation**|Some threads never get resource|⚠️ Partial progress|Unfair execution|
|**Livelock**|Threads move but make no progress|✅ Active but stuck|Endless loop|

---

### ✅ Very Short Summary (TL;DR)

- **Deadlock** → Threads **waiting forever**.
    
- **Starvation** → Some thread **ignored forever**.
    
- **Livelock** → Threads **keep acting but never progress**.
    
- **Prevention** → Lock ordering, timeouts, limit requests, preemption.
    

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DAC/DAC|◀ DAC]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
