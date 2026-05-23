# 📘 Software Quality — **BEST FINAL VERSION (Exam-Ready)**

## 🧩 1️⃣ Errors, Faults, and Failures (FOUNDATION)

- **Error** → Human mistake (misunderstanding, bad decision, omission).
    
- **Fault (Bug / Defect)** → Incorrect element in code or design caused by an error.
    
- **Failure** → Observable incorrect behavior **during execution**.
    

### 🔁 Fundamental Chain (VERY IMPORTANT)

```
Error (human) → Fault (software) → Failure (runtime)
```

📌 Key points:

- Every **fault** originates from a **human error**
    
- A **failure** appears only when the software runs
    

---

## 🔥 2️⃣ Nine Sources of Software Errors

1. **Poor requirement definition**  
    → Unclear, incomplete, or incorrect user needs.
    
2. **Communication problems**  
    → Misunderstandings between users, developers, stakeholders.
    
3. **Deliberate deviation from requirements**  
    → Skipping or modifying features due to time, cost, or strategy pressure.
    
4. **Design (logic) errors**  
    → Wrong architecture, algorithms, or component interactions.
    
5. **Programming errors**  
    → Syntax mistakes and logical coding errors.
    
6. **Non-conformance to standards/documentation**  
    → Ignoring coding rules or not updating documentation.
    
7. **Insufficient testing**  
    → Missing test cases, edge cases not covered.
    
8. **User interface or procedure errors**  
    → Poor UI design or unclear procedures causing user mistakes.
    
9. **Documentation errors**  
    → Incorrect, outdated, or missing user/technical documentation.
    

### 💡 Critical Insight (EXAM FAVORITE)

- **Most defects are introduced early** (requirements & design).
    
- **Cost of fixing defects increases dramatically** if found late.
    

---

## 🎯 3️⃣ What Is Software Quality?

### Core Definition

> **Software quality = Conformance to requirements**

It also implies:

- Low defect rate
    
- High reliability
    
- Correct behavior in real usage
    
- User satisfaction
    

📏 Reliability indicator:

- **MTTF (Mean Time To Failure)**
    

---

## 🏛️ 4️⃣ Definitions of Software Quality (MEMORIZE)

- **ISO**  
    → Quality = all features and characteristics that satisfy **expressed or implicit needs**.
    
- **IEEE**  
    → Quality = degree to which software possesses desired **attributes**  
    (reliability, usability, security, etc.).
    
- **Crosby**  
    → Quality = degree to which the **client feels expectations are met**.
    
- **Pressman ⭐ (MOST IMPORTANT)**  
    → Quality = conformance to:
    
    - Functional requirements
        
    - Performance requirements
        
    - Documented standards
        
    - Implicit professional expectations
        

---

## 📦 5️⃣ McCall’s Software Quality Model

### 🔵 Product Operation (During Use)

|Factor|Meaning|
|---|---|
|Correctness|Output accuracy & completeness|
|Reliability|Failure tolerance|
|Efficiency|Resource usage|
|Integrity|Security|
|Usability|Ease of learning & use|

---

### 🟡 Product Revision (During Maintenance)

|Factor|Meaning|
|---|---|
|Maintainability|Ease of fixing defects|
|Flexibility|Ease of adapting to change|
|Testability|Ease of testing|

---

### 🟢 Product Transition (During Evolution)

|Factor|Meaning|
|---|---|
|Portability|Works in new environments|
|Reusability|Components reusable|
|Interoperability|Works with other systems|

🧠 **Mnemonic (Exam Trick)**  
**C R E I U / M F T / P R I**

---

## 🛠️ 6️⃣ Software Quality Assurance (SQA)

### Definition

> **SQA = Planned and systematic activities** ensuring that software meets technical and quality requirements.

It also evaluates:

- Development process
    
- Maintenance process
    

---

### 🎯 Objectives of SQA

#### During Development

- Ensure functional & technical correctness
    
- Respect deadlines and budget
    
- Improve quality continuously
    

#### During Maintenance

- Ensure correct maintenance actions
    
- Control time and cost
    
- Improve efficiency of maintenance activities
    

---

### 📏 Three Core Principles of SQA (VERY IMPORTANT)

1. **Know what you are doing**
    
2. **Know what you should do**
    
3. **Know how to measure the difference**
    

---

## 🔍 7️⃣ Verification vs Validation (CLASSIC QUESTION)

|Concept|Question|Meaning|
|---|---|---|
|**Verification**|“Are we building the product right?”|Conformance to specifications|
|**Validation**|“Are we building the right product?”|Meeting real user needs|

📌 Verification = process correctness  
📌 Validation = product usefulness

---

## 🧪 8️⃣ Static Code Verification Techniques

|Technique|Who|Purpose|
|---|---|---|
|**Review**|Project leader + team|Logic & consistency check|
|**Inspection**|Expert|Deep defect detection|
|**Audit**|Internal or external authority|Formal compliance verification|

---

## 🧠 🎯 FINAL EXAM CHEAT SHEET

- **Error → Fault → Failure**
    
- Most defects appear **early**
    
- Fixing late = **very expensive**
    
- Quality = **conformance to requirements**
    
- **Pressman definition** = safest in exams
    
- McCall model = **3 aspects + 11 factors**
    
- Verification ≠ Validation
    
- SQA = prevention + control + improvement
    

---
# ✅ **QCM — Chapter 2: Software Quality**

---

## **QCM 1 — Error, Fault, Failure**

Which sequence is **correct**?

A. Fault → Error → Failure  
B. Failure → Error → Fault  
C. Error → Fault → Failure  
D. Error → Failure → Fault

✅ **Correct answer:** **C**

---

## **QCM 2 — Error Definition**

An **error** is:

A. A crash during execution  
B. A defect in the source code  
C. A human mistake during development  
D. A system malfunction

✅ **Correct answer:** **C**

---

## **QCM 3 — Failure**

A **failure** occurs when:

A. Code violates standards  
B. A requirement is unclear  
C. The software behaves incorrectly during execution  
D. A bug exists in the source code

✅ **Correct answer:** **C**

---

## **QCM 4 — Sources of Errors**

How many **main sources of software errors** are identified in the course?

A. 6  
B. 7  
C. 8  
D. 9

✅ **Correct answer:** **D**

---

## **QCM 5 — Early Defects**

Most software defects are introduced during:

A. Testing and maintenance  
B. Implementation only  
C. Requirements and design phases  
D. Deployment

✅ **Correct answer:** **C**

---

## **QCM 6 — Cost of Fixing Defects**

The cost of fixing defects:

A. Decreases over time  
B. Remains constant  
C. Increases when defects are found late  
D. Depends only on hardware

✅ **Correct answer:** **C**

---

## **QCM 7 — Software Quality (Core Definition)**

Software quality mainly means:

A. High performance  
B. User satisfaction only  
C. Conformance to requirements  
D. Use of modern tools

✅ **Correct answer:** **C**

---

## **QCM 8 — Reliability Measure**

Which metric measures software reliability?

A. MTBF  
B. MTTF  
C. CPU usage  
D. Throughput

✅ **Correct answer:** **B**

---

## **QCM 9 — ISO Definition of Quality**

According to **ISO**, quality is:

A. User satisfaction level  
B. Number of defects  
C. Features that satisfy expressed and implicit needs  
D. Compliance with standards only

✅ **Correct answer:** **C**

---

## **QCM 10 — Pressman Definition**

Pressman defines quality as conformance to:

A. Functional requirements only  
B. Functional + performance requirements + standards + implicit expectations  
C. User opinions only  
D. Hardware constraints

✅ **Correct answer:** **B**

---

## **QCM 11 — McCall Model**

How many **main aspects** are in McCall’s quality model?

A. 2  
B. 3  
C. 5  
D. 11

✅ **Correct answer:** **B**

---

## **QCM 12 — Product Operation**

Which factor belongs to **Product Operation**?

A. Portability  
B. Maintainability  
C. Reliability  
D. Reusability

✅ **Correct answer:** **C**

---

## **QCM 13 — Product Revision**

Which factor is related to **maintenance**?

A. Integrity  
B. Efficiency  
C. Testability  
D. Portability

✅ **Correct answer:** **C**

---

## **QCM 14 — Product Transition**

Which factor helps software work in different environments?

A. Usability  
B. Flexibility  
C. Portability  
D. Reliability

✅ **Correct answer:** **C**

---

## **QCM 15 — Software Quality Assurance (SQA)**

SQA is best defined as:

A. Testing the software only  
B. Writing documentation  
C. Planned and systematic activities ensuring quality  
D. Debugging after deployment

✅ **Correct answer:** **C**

---

## **QCM 16 — Objective of SQA**

Which is **NOT** an objective of SQA?

A. Ensure software meets requirements  
B. Respect time and budget  
C. Improve development efficiency  
D. Eliminate all future maintenance

✅ **Correct answer:** **D**

---

## **QCM 17 — SQA Core Principles**

How many **main principles** of SQA are defined?

A. 2  
B. 3  
C. 4  
D. 5

✅ **Correct answer:** **B**

---

## **QCM 18 — Verification**

Verification answers which question?

A. Are we building the right product?  
B. Are users satisfied?  
C. Are we building the product right?  
D. Does the system perform fast?

✅ **Correct answer:** **C**

---

## **QCM 19 — Validation**

Validation focuses on:

A. Internal code structure  
B. User needs and expectations  
C. Coding standards  
D. System architecture

✅ **Correct answer:** **B**

---

## **QCM 20 — Static Verification**

Which technique is the **most formal**?

A. Review  
B. Inspection  
C. Audit  
D. Debugging

✅ **Correct answer:** **C**

---

## 🎯 **Score Guide**

- **16–20 correct** → 🔥 Excellent (exam-ready)
    
- **12–15 correct** → 👍 Good (revise weak points)
    
- **<12** → ⚠️ Revisit definitions & McCall model
    

---

When you’re ready, just say:

- **“Chapter 3 QCM”**  
    or
    
- **“Mixed QCM (Ch 1–2)”**
    

I’ve got you 💪

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TQL/TQL|◀ TQL]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
