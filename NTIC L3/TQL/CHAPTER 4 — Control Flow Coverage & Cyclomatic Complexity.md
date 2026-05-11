# 📘 **CHAPTER 4 — Control Flow Coverage & Cyclomatic Complexity (COMPLETE VERSION)**

---

## 🎯 **Purpose of Chapter 4**

This chapter answers **three exam-critical questions**:

1. How do we **structure control flow** into testable units?
    
2. How many **independent test paths** are required?
    
3. How do we **quantify complexity and test effort**?
    

Main concepts:

- **PLCS**
    
- **Independent paths**
    
- **Cyclomatic complexity (McCabe)**
    

---

## 1️⃣ **PLCS — Primitive Linear Code Sequence**

### 🔹 Definition

A **PLCS** is a **maximal linear sequence of instructions** that:

- Has **one entry**
    
- Has **one exit**
    
- Contains **no internal branching**
    

📌 A PLCS is the same idea as a **basic block**.

---

### 🔹 Jump Nodes (IMPORTANT)

A **jump node** is a node where control flow may change.

|Type|Examples|
|---|---|
|Entry|Start of program / function|
|Exit|`return`, program end|
|Decision source|`if`, `while`, `for`, `switch`|
|Decision target|Target of branch (`else`, loop body, case)|

📌 **Each PLCS starts and ends at jump nodes**.

---

### 🔹 Why PLCS Matters

PLCS allows us to:

- Simplify CFG analysis
    
- Group linear instructions together
    
- Ensure **all straight-line code is executed**
    

---

## 2️⃣ **PLCS Coverage Criterion**

### 🔹 Definition

A test suite satisfies **PLCS coverage** if:

> **Every PLCS is executed at least once**

📌 PLCS coverage is **stronger than statement coverage**  
📌 But **weaker than full path coverage**

---

### 🔹 Key Observation (Exam Favorite ⭐)

Even if a program contains **many PLCS**,  
➡️ **a small number of paths can cover all PLCS**

Example (from course):

- 9 PLCS
    
- Only **3 carefully chosen paths** cover them all
    

---

## 3️⃣ **From PLCS to Independent Paths**

PLCS alone is not enough for **decision logic**.  
We need **independent paths**.

---

## 4️⃣ **Independent Paths**

### 🔹 Definition

An **independent path** is a path that:

- Introduces **at least one new edge**
    
- Has not appeared in any previous path
    

📌 Independent paths form a **basis set**.

---

### 🔹 Why Independent Paths Matter

|Property|Meaning|
|---|---|
|Completeness|All decisions exercised|
|Minimality|No redundant paths|
|Test basis|One test per independent path|

---

## 5️⃣ **Cyclomatic Complexity (McCabe)**

### 🔹 Definition

**Cyclomatic complexity V(G)** measures:

- Logical complexity of a program
    
- Number of **independent paths**
    
- Minimum number of **test cases**
    

Introduced by **McCabe**.

---

## 6️⃣ **Cyclomatic Complexity Formulas**

### 🔹 Main Formula (CFG-based)

|Formula|Meaning|
|---|---|
|**V(G) = E − N + 2**|E = edges, N = nodes|

---

### 🔹 Equivalent Formulas (EXAM TRAP)

|Formula|When used|
|---|---|
|**V(G) = number of regions**|Visual CFG|
|**V(G) = number of decisions + 1**|Structured code|

📌 All formulas give the **same V(G)**.

---

## 7️⃣ **Regions in CFG**

### 🔹 Definition

A **region** is an area bounded by edges in a CFG.

|Region type|Description|
|---|---|
|Internal|Inside the graph|
|External|Outside (infinite region)|

📌 **Number of regions = Cyclomatic complexity**

---

## 8️⃣ **Interpreting Cyclomatic Complexity**

|V(G)|Interpretation|
|---|---|
|1–10|Simple, testable|
|11–20|Moderate complexity|
|21–40|High risk|
|> 40|Very complex, hard to maintain|

📌 High V(G) ⇒ more tests, higher fault probability

---

## 9️⃣ **Designing Test Cases with Cyclomatic Complexity**

### 🔹 Standard Method (VERY IMPORTANT)

1. Draw the **CFG**
    
2. Compute **V(G)**
    
3. Identify **independent paths**
    
4. Design **one test case per path**
    

📌 **Minimum test cases = V(G)**

---

## 🔟 **PLCS vs Independent Paths vs Coverage**

|Concept|Ensures|
|---|---|
|Statement coverage|Each instruction executed|
|PLCS coverage|Each linear block executed|
|Independent paths|All decisions exercised|
|Cyclomatic complexity|Minimum test count|

---

## 1️⃣1️⃣ **Advantages of Cyclomatic Complexity**

- Objective & quantitative
    
- Language-independent
    
- Early detection of risky code
    
- Improves maintainability & testability
    

---

## 🎓 **FINAL EXAM CHEAT SHEET**

- PLCS = linear block between jump nodes
    
- PLCS starts & ends at jump nodes
    
- Independent path = introduces a new edge
    
- Cyclomatic complexity = **# independent paths**
    
- **V(G) = E − N + 2**
    
- **V(G) = decisions + 1**
    
- Minimum test cases = **V(G)**
    
- Regions = V(G)
    

---

# ✅ **QCM — Chapter 4**

### **QCM 1**

A PLCS is:

A. A loop  
B. A linear instruction sequence without branches  
C. A complete execution path  
D. A condition

✅ **Answer:** **B**

---

### **QCM 2**

A PLCS always starts and ends at:

A. Any node  
B. Loop nodes  
C. Jump nodes  
D. Conditions only

✅ **Answer:** **C**

---

### **QCM 3**

PLCS coverage guarantees:

A. All paths executed  
B. All loops infinite  
C. All linear code blocks executed  
D. All conditions true

✅ **Answer:** **C**

---

### **QCM 4**

An independent path must:

A. Be the shortest path  
B. Avoid loops  
C. Introduce at least one new edge  
D. Have no conditions

✅ **Answer:** **C**

---

### **QCM 5**

Cyclomatic complexity measures:

A. Memory usage  
B. Execution speed  
C. Logical complexity  
D. Code size

✅ **Answer:** **C**

---

### **QCM 6**

Who introduced cyclomatic complexity?

A. Pressman  
B. McCall  
C. McCabe  
D. ISO

✅ **Answer:** **C**

---

### **QCM 7**

Which formula is correct?

A. V(G) = N − E + 2  
B. V(G) = E − N + 2  
C. V(G) = conditions − 1  
D. V(G) = E + N

✅ **Answer:** **B**

---

### **QCM 8**

If a program has 5 decisions, V(G) equals:

A. 4  
B. 5  
C. 6  
D. 7

✅ **Answer:** **C**

---

### **QCM 9**

Cyclomatic complexity equals the number of:

A. Nodes  
B. PLCS  
C. Independent paths  
D. Statements

✅ **Answer:** **C**

---

### **QCM 10**

A program with V(G) > 40 is:

A. Well structured  
B. Easy to test  
C. Very complex and risky  
D. Optimal

✅ **Answer:** **C**

---

