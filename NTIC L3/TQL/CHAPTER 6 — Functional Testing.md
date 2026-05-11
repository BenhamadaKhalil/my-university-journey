# 📘 **CHAPTER 6 — Functional Testing (COMPLETE & EXAM-READY)**

---

## 🎯 **Objective of Functional Testing**

Functional testing verifies that the software:

- **Complies with its specification**
    
- Produces the **expected outputs** for given inputs
    
- Behaves correctly from the **user’s point of view**
    

📌 It focuses on **what the system does**, not **how it is implemented**

---

## 1️⃣ **What Is Functional Testing?**

### 🔹 Definition

Functional testing is a **black-box testing** technique that:

- Does **not require knowledge of internal code**
    
- Is based on **interface and functional specifications**
    
- Compares **expected results (oracle)** with **execution results**
    

---

### 🔹 Functional Testing Process

|Element|Role|
|---|---|
|Specification|Defines expected behavior|
|Test data|Inputs derived from specification|
|Program|System under test|
|Oracle|Determines correct results|
|Execution results|Observed outputs|

📌 Few oracle problems, but **test data generation is difficult**

---

## 2️⃣ **Characteristics of Functional Testing**

|Property|Description|
|---|---|
|Black-box|Internal structure ignored|
|Spec-based|Derived from requirements|
|Blind to code faults|May miss dead code|
|Flexible|Used at unit, integration, system levels|

📌 Ensures **specification–code adequacy**, not internal correctness

---

## 3️⃣ **Main Black-Box Test Design Techniques**

Functional testing relies on several techniques:

- **Equivalence Classes**
    
- **Boundary Value Testing**
    
- **Cause–Effect Graphs**
    
- Combinatorial testing
    
- Ad-hoc testing (error guessing)
    
- Specification coverage
    

This chapter focuses mainly on the **first three**.

---

## 4️⃣ **Equivalence Class Testing**

### 🔹 Principle

The input domain is divided into **equivalence classes** such that:

> The program behaves the **same** for all values in the same class.

📌 Only **one representative value per class** needs to be tested

---

### 🔹 Types of Classes

| Class Type    | Description                     |
| ------------- | ------------------------------- |
| Valid class   | Inputs that satisfy constraints |
| Invalid class | Inputs that violate constraints |

📌 **Never mix invalid classes together in one test case**

---

### 🔹 Example (5-digit number)

|Class|Condition|
|---|---|
|Invalid|N < 10 000|
|Valid|10 000 ≤ N ≤ 99 999|
|Invalid|N ≥ 100 000|

---

## 5️⃣ **Partitioning Rules (EXAM FAVORITE)**

| Situation           | How to Partition              |
| ------------------- | ----------------------------- |
| Range [a…b]         | Below a, inside, above b      |
| Finite set          | Empty, valid values, too many |
| Constraint / format | Satisfied vs violated         |

---

## 6️⃣ **Multivariable Equivalence Classes**

With multiple inputs, defining tests becomes harder.

---

### 🔹 Approach 1 — Cartesian Product

| Idea                                 | Result          |
| ------------------------------------ | --------------- |
| Combine all classes of all variables | Many test cases |

📌 Problem: **combinatorial explosion**  
📌 May violate constraints between variables

---

### 🔹 Approach 2 — Union of Partitions

| Idea                                            | Result    |
| ----------------------------------------------- | --------- |
| Test each class once with representative values | Few tests |

📌 Risk: relations between variables may be missed

---

### 🔹 Approach 3 — Partition the Total Domain (IMPORTANT)

|Idea|
|---|
|Create equivalence classes over the **combined input space**|

✔ Respects constraints between variables  
❌ Harder to define

---

### 🔹 Approach 4 — Pairwise Combination

| Idea                                    |
| --------------------------------------- |
| Cover all **pairs** of variable classes |

✔ Fewer tests than Cartesian product  
❌ Some combinations may still be missed

---

## 7️⃣ **Boundary Value Testing**

### 🔹 Principle

Errors tend to occur at **boundaries**, so test:

- Values **just below**
    
- Values **on**
    
- Values **just above** boundaries
    

---

### 🔹 Common Boundary Examples

| Data Type         | Boundary Tests           |
| ----------------- | ------------------------ |
| Interval [a…b]    | a-1, a, a+1, b-1, b, b+1 |
| String length ≤ n | 0, 1, n-1, n, n+1        |
| Array size ≤ n    | 0, 1, n-1, n             |

---

## 8️⃣ **Cause–Effect Graph Testing**

### 🔹 Purpose

Cause–effect graphs analyze **relationships between inputs (causes)** and **outputs (effects)**.

📌 Improvement of equivalence class testing  
📌 Helps detect **missing or inconsistent specifications**

---

### 🔹 Basic Concepts

|Element|Meaning|
|---|---|
|Cause (C)|Input condition|
|Effect (E)|Output or system action|
|Graph|Logical relation between causes & effects|

---

### 🔹 Logical Operators

|Symbol|Meaning|
|---|---|
|AND (∧)|All must be true|
|OR (∨)|At least one true|
|NOT (¬)|Negation|

---

## 9️⃣ **Cause Constraints (VERY IMPORTANT)**

|Constraint|Meaning|
|---|---|
|PT (Total partition)|Exactly one cause is true|
|PP (Partial partition)|0 or 1 cause true|
|NE (Necessity)|At least one true|
|CA (Causality)|C1 ⇒ C2|
|EX (Exclusion)|C1 ⇒ ¬C2|

📌 These constraints **reduce impossible test cases**

---

## 🔟 **Effect Constraint**

|Constraint|Meaning|
|---|---|
|Mask (M)|If E1 is true, E2 must be false|

📌 Applies to **effects**, not causes

---

## 1️⃣1️⃣ **From Cause–Effect Graph to Decision Table**

### 🔹 Steps

1. Identify **causes and effects**
    
2. Build cause–effect graph
    
3. Apply constraints
    
4. Convert graph into a **decision table**
    
5. Each column → **one test case**
    

---

## 1️⃣2️⃣ **Functional vs Structural Testing**

|Aspect|Functional|Structural|
|---|---|---|
|View|External|Internal|
|Detects dead code|❌|✔|
|Detects missing functionality|✔|❌|

📌 They are **complementary**  
📌 At unit level: **functional first**, then structural

---

## 🎓 **FINAL EXAM CHEAT SHEET**

- Functional testing = black-box, spec-based
    
- Equivalence classes = 1 test per class
    
- Never mix invalid classes
    
- Boundary testing = focus on limits
    
- Multivariable testing needs strategy
    
- Cause–effect graphs → decision tables
    
- Functional + structural = best coverage
    

---

# ✅ **QCM — Chapter 6: Functional Testing**

### **QCM 1**

Functional testing is:

A. Code-based testing  
B. Black-box testing  
C. Data-flow testing  
D. Mutation testing

✅ **Answer:** **B**

---

### **QCM 2**

Functional testing is based on:

A. Source code  
B. Control flow graph  
C. Specifications  
D. Variables

✅ **Answer:** **C**

---

### **QCM 3**

Equivalence class testing assumes:

A. All inputs behave differently  
B. One value represents an entire class  
C. Boundaries are irrelevant  
D. Only invalid inputs matter

✅ **Answer:** **B**

---

### **QCM 4**

How many values are needed per equivalence class?

A. All values  
B. Two values  
C. One representative  
D. None

✅ **Answer:** **C**

---

### **QCM 5**

Boundary testing focuses on:

A. Random inputs  
B. Middle values  
C. Extreme and limit values  
D. Internal variables

✅ **Answer:** **C**

---

### **QCM 6**

Which approach may cause combinatorial explosion?

A. Union of partitions  
B. Total domain partition  
C. Pairwise testing  
D. Cartesian product

✅ **Answer:** **D**

---

### **QCM 7**

Cause–effect graphs are used to:

A. Measure complexity  
B. Analyze input–output relations  
C. Detect dead code  
D. Optimize performance

✅ **Answer:** **B**

---

### **QCM 8**

Which constraint means “exactly one cause true”?

A. PP  
B. NE  
C. PT  
D. EX

✅ **Answer:** **C**

---

### **QCM 9**

The **mask** constraint applies to:

A. Causes  
B. Effects  
C. Inputs  
D. Variables

✅ **Answer:** **B**

---

### **QCM 10**

Functional and structural testing are:

A. Redundant  
B. Opposite  
C. Complementary  
D. Identical

✅ **Answer:** **C**

---

## 🎯 **Score Guide**

- **8–10** → 🔥 Excellent
    
- **6–7** → 👍 Good
    
- **<6** → ⚠️ Revise equivalence classes & cause–effect graphs
    

---

If you want next:

- **Hard QCM (Chapter 6 traps only)**
    
- **Full TQL revision (Ch 1 → 6)**
    
- **Decision table exercises with correction**
    

Just tell me 💪