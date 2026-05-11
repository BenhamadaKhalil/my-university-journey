# 📚 **Software Project Management — Clean Lesson Notes 

## 1️⃣ **What Is a Project?**

A **project** is:

- ⏳ **Temporary** → has a **start and an end**
    
- 🎯 **Unique** → not repeated exactly the same way
    
- ✅ **Goal-oriented** → aims to produce a **specific result**
    
- 💰 **Constrained** → limited by **time, cost, resources, and quality**
    

📌 If an activity is **repetitive and continuous**, it is **NOT** a project (it is **production**).

---

## 🔹 Why Is a Project **Unique**?

|Aspect|Meaning|Example|
|---|---|---|
|**Type Uniqueness**|Different types → different activities|Website ≠ Mobile game|
|**Instance Uniqueness**|Even similar projects differ|Two websites for two clients are never identical|

---

## 2️⃣ **Examples of Projects**

| Project                   | Final Result           |
| ------------------------- | ---------------------- |
| 📱 Mobile app development | Functional application |
| 🏠 Building a house       | Completed building     |
| 🎉 Organizing an event    | Successful event       |

---

## 3️⃣ **Engineering Project vs Product Project**

| Type                            | Purpose             | Result               | Example                      |
| ------------------------------- | ------------------- | -------------------- | ---------------------------- |
| **Engineering Project**         | One specific client | Customized solution  | University Management System |
| **Product Project(Production)** | Multiple clients    | Standardized product | Spotify-like app             |

📌 **Key difference (EXAM):**

- Engineering = **customized**
    
- Product = **reusable / mass-produced**
    

---

## 4️⃣ **Why Do Projects Start? (Initiation Causes)**

A project may start because of:

- 💡 New idea or innovation
    
- 📈 Market or economic demand
    
- 🏢 Internal process improvement
    
- 🧑‍💼 Client request
    
- ⚖️ Legal or regulatory obligation
    
- 🌍 Social need
    

---

## 5️⃣ **Project Stakeholders**

Stakeholders are people or organizations that **affect or are affected by the project**.

| Role     | Name                                   | Responsibility              |
| -------- | -------------------------------------- | --------------------------- |
| Client   | **MOA** (Project Owner)                | Defines **WHAT** is needed  |
| Executor | **MOE** (Project Manager / Contractor) | Defines **HOW** to build it |
| Users    | End-users                              | Use the final system        |

### 🔄 Relationship Between Actors

```
MOA → defines WHAT
        ↓
MOE → defines HOW and executes
        ↓
Users → use the delivered system
```

⚠️ **Very important (EXAM):**  
👉 **The system is NOT an actor** in UML use case diagrams.

---

## 6️⃣ **Project Manager (Inside MOE)**

The **Project Manager** is responsible for:

- 🗓️ Planning tasks
    
- 👥 Assigning responsibilities
    
- ⏱️ Managing deadlines
    
- 💰 Controlling budget
    
- 📊 Monitoring progress and risks
    
- 🗣️ Communicating with MOA
    

🎼 **Analogy:**  
The project manager is like an **orchestra conductor** 🎶  
→ doesn’t play instruments, but ensures harmony.

---

## 7️⃣ **Project Life Cycle**

```
1️⃣ Initiation   → identify need & feasibility
2️⃣ Planning    → tasks, resources, cost, schedule
3️⃣ Execution   → develop / build the solution
4️⃣ Monitoring  → control progress, risks, quality
5️⃣ Closure     → delivery, validation, documentation
```

📌 Each phase **depends on the previous one**.

---

# 📌 **UML Use Case Diagrams**

## 🔹 Main Symbols (Correct UML)

| Symbol        | Meaning                        |
| ------------- | ------------------------------ |
| 🧍 Actor      | External user (NOT the system) |
| ⭕ Use Case    | Functionality                  |
| — Association | Interaction                    |
| `<<include>>` | **Mandatory** sub-use case     |
| `<<extend>>`  | **Optional** behavior          |

⚠️ **Correction:**  
Always write **`<<include>>` and `<<extend>>` explicitly** (this is checked in exams).

---

## ✅ **Simple Use Case Example**

```
🧍 Student
     |
 (Register Account)
```

---

## ✅ **<> Example (Mandatory)**

```
(Enroll in Course)
        |
   <<include>>
        |
 (Verify Payment)
```

✔ Payment verification **always happens**.

---

## ✅ **<> Example (Optional)**

```
 (Place Order)
       ^
       |
  <<extend>>
       |
 (Apply Discount)
```

✔ Happens **only if a condition is true** (promotion exists).

---

# 📍 **Sequence Diagram — Text Example**

### Scenario: Customer Buys an Item

```
Customer → Cashier : gives items
Cashier → System   : scans items
System → Cashier   : total price
Cashier → Customer : requests payment
Customer → Cashier : pays
Cashier → Customer : gives receipt
```

📌 Message order matters  
📌 Shows **interaction flow over time**

---

## ✅ **Final Exam Checklist (MEMORIZE)**

✔ Project = **temporary + unique**  
✔ MOA = defines **WHAT**  
✔ MOE = defines **HOW**  
✔ `<<include>>` = mandatory  
✔ `<<extend>>` = optional  
✔ System ≠ actor  
✔ Project ≠ production

---
