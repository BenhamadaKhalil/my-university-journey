# 🧪 PART 4: SOFTWARE QUALITY – TESTING

## 🎯 1. Introduction

Software testing ensures that a program works **correctly and reliably** before delivery.

In **white-box testing**, we analyze the _internal structure_ of the code. Two key techniques are:

- 🔀 **Control Flow Coverage (PLCS)**
    
- 🧮 **Cyclomatic Complexity (McCabe)**
    

Both techniques rely on the **Control Flow Graph (CFG)** of a program.

---

## 🔷 2. Control Flow Graph (CFG)

A **Control Flow Graph** shows **all possible execution paths** of a program.

### 🔹 Nodes

There are two types of nodes:

- 🟥 **Type A – Jump Nodes**
    
    - Entry point
        
    - Exit point
        
    - Destination of a branch (`IF`, `GOTO`, `LOOP`)
        
- 🟦 **Type B – Normal Nodes**
    
    - Sequential instructions (assignments, calculations, prints)
        

### 🔹 Edges

➡️ Edges represent the flow of control between instructions.

---

## 🧩 3. PLCS – Program Linear Code Sequence

### 📌 Definition

A **PLCS** is:

> A _linear sequence of instructions_ between two **jump nodes**.

### ✅ Rules

- Starts at a **jump node**
    
- Ends at a **jump node**
    
- Contains **only one jump**, at the very end
    

🔍 **Why PLCS?**  
PLCS helps us ensure that **all logical flows** of a program are tested.

---

## 🧪 4. Example Program

```text
005 INPUT A, C
010 B = 2*A
020 A = A + 1
030 IF A < 0 THEN GOTO 60
040 B = -A
050 PRINT A + B
060 IF B = 2*C THEN GOTO 80
070 A = 1 : GOTO 90
080 A = -2 : GOTO 20
090 PRINT A
100 END
```

---

## 🚦 5. Jump Nodes Identification

Jump nodes are instructions that **change the normal flow**:

- ▶️ **5** – Entry
    
- ❓ **30** – IF condition
    
- ❓ **60** – IF condition
    
- 🔁 **70** – GOTO 90
    
- 🔁 **80** – GOTO 20
    
- 🖨️ **90** – PRINT
    
- ⏹️ **100** – END (Exit)
    

---

## 🧱 6. PLCS List (with Explanation)

The program contains **9 PLCS**:

1. `[5 → 20 → 30 → 60]`  
    🟢 Direct path without entering inner blocks
    
2. `[5 → 20 → 30 → 40 → 60 → 80]`  
    🔁 Goes to loop at line 20
    
3. `[5 → 20 → 30 → 40 → 60 → 70 → 90]`  
    🖨️ Ends with printing
    
4. `[20 → 30 → 60]`
    
5. `[20 → 30 → 40 → 60 → 80]`
    
6. `[20 → 30 → 40 → 60 → 70 → 90]`
    
7. `[60 → 80]`
    
8. `[60 → 70 → 90]`
    
9. `[80 → 20]`
    

⚠️ The last **6 PLCS are included** in the first **3 main PLCS**.

---

## 🤖 7. Automated PLCS Coverage (Execution Paths)

Instead of executing **all 9 PLCS**, we can automate testing using **3 paths**:

### ✅ Automated Test Paths

- **B1** ➜ `[5,20,30,60,70,90,100]`
    
- **B2** ➜ `[5,20,30,40,60,80,20,30,60,70,90,100]`
    
- **B3** ➜ `[5,20,30,40,60,70,90,100]`
    

🧠 **Automation Idea:**

```pseudo
for each testPath in {B1, B2, B3}:
    execute program with suitable inputs
    verify output
```

✔️ These 3 automated tests cover **100% of PLCS**.

---

## 🧮 8. Cyclomatic Complexity (McCabe)

### 📖 Definition

**Cyclomatic Complexity** measures the **logical complexity** of a program.

It tells us:

- 🔢 Number of **independent paths**
    
- 🧪 Minimum number of **test cases** required
    

---

## 📐 9. Cyclomatic Complexity Calculation

### ✏️ Formula 1 – Graph Based

```
V(G) = Edges − Nodes + 2
V(G) = 11 − 9 + 2 = 4
```

### 🗺️ Formula 2 – Regions

```
V(G) = Number of regions = 4
```

### ❓ Formula 3 – Decisions

```
V(G) = Number of conditions + 1
V(G) = 3 + 1 = 4
```

✅ **Cyclomatic Complexity = 4**

---

## 📊 10. Meaning of Cyclomatic Number

|Complexity|Code Quality|Testability|Cost|
|---|---|---|---|
|🟢 1–10|Simple & structured|High|Low|
|🟡 10–20|Complex|Medium|Medium|
|🔴 20–40|Very complex|Low|High|
|⚫ >40|Not testable|Very Low|Very High|

---

## 🧪 11. Test Cases Based on Independent Paths

### 🪜 Steps

1. Draw the CFG
    
2. Compute cyclomatic complexity
    
3. Identify **independent paths**
    
4. Create **automated test cases**
    

---

## 📚 12. Example: AVERAGE Procedure (Pressman)

### 📝 Description

The program:

- Accepts up to **100 values**
    
- Stops when **-999** is entered
    
- Accepts values only in `[min, max]`
    
- Outputs **sum and average**
    

---

## 🧭 13. Independent Paths (Automated View)

1. `1-2-3-4-5-6-7-8-9-2-3-10-11-13`
    
2. `1-2-3-4-5-6-7-8-9-2-10-11-13`
    
3. `1-2-3-4-5-6-8-9-2-10-12-13`
    
4. `1-2-3-4-5-8-9-2-10-12-13`
    
5. `1-2-3-10-12-13`
    
6. `1-2-10-12-13`
    

---

## 🤖 14. Automated Test Case Examples

### ✅ Test Case 1

🧪 **Input:** 100 valid values

🎯 **Expected:** Correct sum & average

---

### ✅ Test Case 2

🧪 **Input:** Valid values then `-999`

🎯 **Expected:** Correct sum & average

---

### ❌ Test Case 3

🧪 **Input:** Value > max

🎯 **Expected:** `average = -999`

---

### ❌ Test Case 4

🧪 **Input:** Value < min

🎯 **Expected:** `average = -999`

---

### ❌ Test Case 5

🧪 **Input:** 100 invalid values

🎯 **Expected:** `average = -999`

---

### ❌ Test Case 6

🧪 **Input:** First value = `-999`

🎯 **Expected:** `average = -999`

---

## 🧠 15. Final Summary

- 🔀 **PLCS** ensures linear flow coverage
    
- 🧮 **Cyclomatic Complexity** defines test effort
    
- 🤖 Automation reduces number of required tests
    
- ✅ Independent paths = reliable software
    

---

📌 _Perfect for Obsidian notes, exams, and teaching._