# 📘 **CHAPTER 5 — Data Flow Testing (COMPLETE & EXAM-READY)**

---

## 🎯 **Purpose of Data Flow Testing**

Control-flow testing (Ch.3–4) checks **where execution goes**.  
Data-flow testing checks **how variables are defined and used**.

👉 Goal:

- Detect errors like:
    
    - use of uninitialized variables
        
    - unused assignments
        
    - wrong variable redefinitions
        
- Strengthen structural testing using **variable behavior**
    

---

## 1️⃣ **Data Flow Graph (DFG)**

### 🔹 Principle

A **Data Flow Graph (DFG)** is:

> **CFG + information about variable definitions and uses**

So:

```
DFG = CFG + Def + Use information
```

---

### 🔹 Variable Sets in DFG

For each node `j`:

| Set            | Meaning                                                     |
| -------------- | ----------------------------------------------------------- |
| **Def(j)**     | Variables **defined** in node `j`                           |
| **C-use(j)**   | Variables **used in computations** in `j`                   |
| **P-use(j,k)** | Variables **used in a decision (predicate)** on arc `j → k` |

📌 C-use = computational use  
📌 P-use = predicate (decision) use

---

## 2️⃣ **Definition-Clear Path**

### 🔹 Definition

A path is **definition-clear for variable `x`** from node `i` to node `j` if:

> `x` is **not redefined** on the path between `i` and `j`

📌 This is the **core concept** of data-flow testing.

---

## 3️⃣ **DCU and DPU Sets**

Let `x` be a variable defined at node `i`.

### 🔹 DCU — Definition-Clear Computational Use

| Notation     | Meaning                                                      |
| ------------ | ------------------------------------------------------------ |
| **dcu(x,i)** | Nodes where `x` is **c-used**, reachable by a def-clear path |

---

### 🔹 DPU — Definition-Clear Predicate Use

|Notation|Meaning|
|---|---|
|**dpu(x,i)**|Arcs `(j,k)` where `x` is **p-used**, reachable by a def-clear path|

📌 DCU → computation  
📌 DPU → condition

---

## 4️⃣ **Definition-Use Path (DU-Path)**

### 🔹 Definition

A **DU-path** for variable `x` is a path:

```
i → … → j
```

Such that:

1. `x ∈ def(i)`
    
2. The path is **definition-clear for x**
    
3. Ends at:
    
    - a **c-use** of `x` (node), or
        
    - a **p-use** of `x` (arc)
        
4. Contains **no loops**
    

📌 DU-paths connect **definition → use** of a variable.

---

## 5️⃣ **Structural Data-Flow Coverage Criteria**

These criteria define **how many DU-paths must be tested**.

---

### 🔹 All-Definitions Criterion

| Rule                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------- |
| For each variable `x` and each definition of `x`, execute **at least one** def-clear path to **any** c-use or p-use. |

📌 Weakest data-flow criterion  
📌 Ensures every definition is used **at least once**

---

### 🔹 All-Uses Criterion

| Rule                                                                                                 |
| ---------------------------------------------------------------------------------------------------- |
| For each variable `x` and each definition, execute def-clear paths to **all** its c-uses and p-uses. |

📌 Stronger than all-definitions  
📌 Catches more data-flow errors

---

### 🔹 All DU-Paths Criterion

|Rule|
|---|
|Execute **all possible DU-paths** for every variable definition.|

📌 Strongest criterion  
📌 Often **impractical** due to loops and path explosion

---

## 6️⃣ **Strength Relationship Between Criteria**

### 🔹 “Stronger Than” Relation

Criterion **C₁ subsumes C₂** if:

> Every test set satisfying C₁ also satisfies C₂

Properties:

- Transitive
    
- Partial order
    

---

### 🔹 Data-Flow Criteria Hierarchy

```
All DU-Paths
      ↓
   All-Uses
      ↓
All-Definitions
```

📌 Stronger = more coverage, more cost

---

## 7️⃣ **Relationship with Control-Flow Criteria**

|Comparison|Result|
|---|---|
|All DU-Paths vs All Paths (CFG)|All Paths ⇒ All DU-Paths|
|All-Uses vs All Arcs|All-Uses ⇒ All Arcs|
|All-Definitions vs All Arcs|❌ Not comparable|

📌 Data-flow and control-flow criteria are **complementary**

---

## 8️⃣ **Why Data Flow Testing Is Powerful**

- Detects subtle bugs missed by branch coverage
    
- Focuses on **variable life cycle**
    
- Complements CFG-based testing
    
- Improves reliability of safety-critical software
    

---

## 🎓 **FINAL EXAM CHEAT SHEET**

- DFG = CFG + Def/Use info
    
- **Def**, **C-use**, **P-use**
    
- Definition-clear path = no redefinition
    
- **DCU** = computational use
    
- **DPU** = predicate use
    
- DU-path = def → use, no loop
    
- All-DU-Paths > All-Uses > All-Definitions
    
- All-Uses ⇒ All-Arcs
    
- All-Definitions ⟂ All-Arcs
    

---

# ✅ **QCM — Chapter 5: Data Flow Testing**

---

### **QCM 1**

A Data Flow Graph (DFG) is:

A. A graph of variables only  
B. A CFG enriched with variable definition and use information  
C. A graph without conditions  
D. A UML diagram

✅ **Answer:** **B**

---

### **QCM 2**

`Def(j)` represents:

A. Variables used in node `j`  
B. Variables tested in conditions  
C. Variables defined in node `j`  
D. Variables passed as parameters

✅ **Answer:** **C**

---

### **QCM 3**

A **C-use** corresponds to:

A. Variable used in a loop condition  
B. Variable used in a computation  
C. Variable redefinition  
D. Variable declaration

✅ **Answer:** **B**

---

### **QCM 4**

A **P-use** occurs:

A. In arithmetic expressions  
B. In output statements  
C. In decision predicates  
D. In assignments

✅ **Answer:** **C**

---

### **QCM 5**

A path is **definition-clear** for variable `x` if:

A. `x` is never used  
B. `x` is redefined on the path  
C. `x` is not redefined on the path  
D. The path contains loops

✅ **Answer:** **C**

---

### **QCM 6**

`dcu(x,i)` contains:

A. All definitions of `x`  
B. All nodes where `x` is c-used via a def-clear path  
C. All predicates using `x`  
D. All DU-paths

✅ **Answer:** **B**

---

### **QCM 7**

`dpu(x,i)` contains:

A. Nodes of computation  
B. Arcs where `x` is predicate-used via a def-clear path  
C. All definitions of `x`  
D. All paths in CFG

✅ **Answer:** **B**

---

### **QCM 8**

A DU-path must:

A. Contain loops  
B. End at a definition  
C. Be definition-clear and end at a use  
D. Start at a use

✅ **Answer:** **C**

---

### **QCM 9**

Which criterion is the **weakest**?

A. All-Uses  
B. All DU-Paths  
C. All-Definitions  
D. All-Arcs

✅ **Answer:** **C**

---

### **QCM 10**

Which relation is **correct**?

A. All-Definitions ⇒ All-Uses  
B. All-Uses ⇒ All-Definitions  
C. All-Arcs ⇒ All-Uses  
D. All-Definitions ⇒ All-Arcs

✅ **Answer:** **B**

---

## 🎯 **Score Guide**

- **8–10** → 🔥 Excellent
    
- **6–7** → 👍 Good
    
- **<6** → ⚠️ Re-read DCU / DPU / DU-paths
    

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TQL/TQL|◀ TQL]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
