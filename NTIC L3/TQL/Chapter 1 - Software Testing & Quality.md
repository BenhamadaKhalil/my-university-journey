# 📘 Software Testing & Quality

## Chapter 1 — Introduction to Software Engineering

---

## 1️⃣ Motivation: Hardware vs Software

### 🔹 Reality of Computer Systems

- **80% software**, **20% hardware**
    
- Hardware:
    
    - Produced by few manufacturers
        
    - Standardized & relatively reliable
        
- **Most IT problems come from software**, not hardware
    

👉 Conclusion: **Improving software quality is critical**.

---

### 🔹 Project Failure Statistics (1995)

A study by **Standish Group** on:

- 365 companies
    
- 8,380 applications
    

📊 Results:

- ✅ **16.2%** met initial expectations
    
- ⚠️ **52.7%** exceeded cost or schedule
    
- ❌ **31.1%** were abandoned
    

👉 Clear proof that **software development needs engineering discipline**.

---

## 2️⃣ What Is Software?

### 🔹 Definition

Software = **a set of programs** that allow a computer system to perform specific tasks.

### 🔹 Key Characteristics

- 🫥 **Intangible** (not physical)
    
- ❗ **Constrained**: works correctly or not at all
    
- 🧩 **Complex structure** (many interconnected parts)
    
- 🔄 **Evolves constantly**
    
- 💰 **Low reproduction cost** (only first version is expensive)
    
- 🎯 Often **custom-made** for specific users
    
- 🛠 Requires structured processes (Agile, Waterfall…)
    

---

## 3️⃣ Birth of Software Engineering

### 🔹 Origins

- **NATO Conference**, Garmisch (Germany), **1968**
    
- Observation:
    
    - Software projects were **expensive**
        
    - Poorly organized
        
    - Failed to meet expectations
        

➡️ The term **Software Engineering** was introduced.

### 🔹 Main Questions

- How do we **build quality software**?
    
- What **criteria define quality**?
    

---

## 4️⃣ Software Engineering: Definition & Goals

### 🔹 Definition

Software Engineering =  
A **set of methods, techniques, and tools** for:

- Specification
    
- Design
    
- Implementation
    
- Testing
    
- Maintenance
    

### 🎯 Goals

- Satisfy users
    
- Meet real needs
    
- Reduce maintenance cost
    
- Deliver on time & within budget
    

---

## 5️⃣ Fundamental Principles of Software Engineering

### 1️⃣ **Rigor**

- Work must be **precise and methodical**
    
- Use formal notations and rules
    

🧠 Example:  
Formal specifications or flow diagrams to verify correctness.

---

### 2️⃣ **Separation of Concerns**

- Split a complex system into **independent problems**
    

🧠 Example:  
Travel app:

- User management
    
- Flight search
    
- Payment  
    (each handled separately)
    

---

### 3️⃣ **Modularity**

- Divide software into **independent modules**
    
- High cohesion, low coupling
    

🧠 Example:  
Library system:

- Books module
    
- Users module
    
- Loans module
    
- Reports module
    

---

### 4️⃣ **Abstraction**

- Focus on **essential aspects**
    
- Hide unnecessary details
    

🧠 Example:  
Classes like `User`, `Product` in an API without exposing internals.

---

### 5️⃣ **Anticipation of Change**

- Software **will evolve**
    
- Design must support future changes
    

🧠 Example:  
E-commerce app with configurable promotions (no code changes).

---

### 6️⃣ **Genericity**

- Build **reusable solutions**
    

🧠 Example:  
Reusable UI components (buttons, forms).

---

### 7️⃣ **Incremental Construction**

- Build software **step by step**
    
- Each version improves the previous one
    

🧠 Example:  
Mobile app:

1. Login + list
    
2. Search
    
3. Comments
    

---

## 6️⃣ Expected Software Qualities

### 🔹 Usefulness

- Software must match **user needs**
    

✔️ Improve requirements analysis  
✔️ Communicate with users  
✔️ Work rigorously

---

### 🔹 Usability

- Easy to learn
    
- Easy to use
    

✔️ Study user behavior  
✔️ Adapt ergonomics

---

### 🔹 Reliability

- **Conformance**: matches specs
    
- **Robustness**: works in abnormal conditions
    

🧠 Example:  
Booking system works even with slow internet.

📏 Measures:

- MTBF
    
- Availability
    
- Error rate
    

---

### 🔹 Interoperability & Coupling

- Ability to work with other systems
    
- Low dependency between modules
    

✔️ APIs  
✔️ Middleware  
✔️ Standard formats (XML, JSON, HTTP)

---

### 🔹 Performance

- Meets response time constraints
    

✔️ Better algorithms  
✔️ Simpler design  
✔️ Better hardware

---

### 🔹 Portability

- Runs on multiple platforms
    

✔️ Environment independence  
✔️ Virtual machines

---

### 🔹 Reusability

- ~80% generic code, 20% specific
    

✔️ Abstraction  
✔️ Design Patterns  
✔️ Reusable components

---

### 🔹 Maintainability

- Easy to fix, modify, extend
    

🎯 Objectives:

- Reduce corrective maintenance
    
- Reduce cost of evolution
    

✔️ Modularity  
✔️ Automated tests

---

## 7️⃣ Software Life Cycle

📌 **Quality of process ⇒ Quality of product**

Software is developed through **successive controlled stages**.

---

## 8️⃣ Life Cycle Phases

### 1️⃣ Feasibility

- Is the project worth doing?
    
- Market & technical analysis
    

---

### 2️⃣ Specification

- Define functionalities
    
- Collect user requirements
    
- Analyze domain concepts
    

---

### 3️⃣ Project Organization

- Planning
    
- Cost estimation
    
- Quality assurance
    
- Task allocation
    

---

### 4️⃣ Design

- Architecture
    
- Interfaces
    
- Algorithms
    
- Detailed models
    

---

### 5️⃣ Implementation & Testing

- Coding
    
- Tests:
    
    - Unit
        
    - Integration
        
    - Validation
        
    - System
        

---

### 6️⃣ Delivery & Maintenance

- Installation
    
- User training
    
- Support
    
- Updates & improvements
    

⚠️ Fixing errors early costs **much less** than later.

---

## 9️⃣ Common Software Documents

- Requirements specification
    
- Object model
    
- Use cases
    
- Project schedule
    
- Test plan
    
- Quality plan
    
- User manual
    
- Source code
    
- Test reports
    

---

## 🔟 Software Development Models

### 🔹 Tunnel Model

- No real structure
    
- ❌ Avoid except for very small projects
    

### 🔹 Waterfall Model

- Sequential phases
    
- Testing comes late
    

### 🔹 V-Model ⭐ (Most Used)

- Testing linked to each development phase
    
- Better quality control
    

### 🔹 Spiral Model

- Iterative cycles:
    
    - Planning
        
    - Risk analysis
        
    - Design
        
    - Implementation
        
    - Testing
        

---

## 🧠 Exam Tips (Very Important)

- Memorize **7 principles**
    
- Know **software qualities**
    
- Understand **life cycle phases**
    
- Compare **development models**
    
- Expect **QCM + short definitions**
    

---
Perfect 👍  
Here is the **QCM for Chapter 1 – Introduction to Software Engineering**, **exam-oriented**, clean, and not overloaded.

---

# ✅ **QCM — Chapter 1: Introduction to Software Engineering**

---

## **QCM 1 — Software vs Hardware**

Which statement is **correct**?

A. Computer systems are mostly hardware  
B. Software represents about 80% of computer systems  
C. Hardware problems are more frequent than software problems  
D. Hardware has a higher reproduction cost than software

✅ **Correct answer:** **B**

---

## **QCM 2 — Software Crisis (1960s)**

The software crisis was mainly due to:

A. Lack of powerful hardware  
B. Poor programming languages  
C. Poor organization and lack of structured methods  
D. Too many developers

✅ **Correct answer:** **C**

---

## **QCM 3 — Software Characteristics**

Which of the following is **NOT** a software characteristic?

A. Intangible  
B. Low reproduction cost  
C. Independent of physical medium  
D. Wears out physically over time

✅ **Correct answer:** **D**

---

## **QCM 4 — Software Engineering Definition**

Software Engineering is best defined as:

A. Programming with modern languages  
B. Writing code faster  
C. A set of methods, tools, and techniques to develop software  
D. Hardware and software integration

✅ **Correct answer:** **C**

---

## **QCM 5 — Main Goals of Software Engineering**

Which is **NOT** a goal of Software Engineering?

A. Satisfy user needs  
B. Reduce maintenance costs  
C. Deliver software within reasonable time  
D. Eliminate all software bugs forever

✅ **Correct answer:** **D**

---

## **QCM 6 — Fundamental Principles**

How many **fundamental principles** of Software Engineering are defined in the course?

A. 5  
B. 6  
C. 7  
D. 8

✅ **Correct answer:** **C**

---

## **QCM 7 — Separation of Concerns**

The principle of **separation of concerns** means:

A. Separating developers from users  
B. Dividing a complex system into manageable parts  
C. Writing independent programs  
D. Avoiding documentation

✅ **Correct answer:** **B**

---

## **QCM 8 — Modularity**

A good modular design should have:

A. High coupling, low cohesion  
B. Low coupling, high cohesion  
C. High coupling, high cohesion  
D. No interaction between modules

✅ **Correct answer:** **B**

---

## **QCM 9 — Abstraction**

Abstraction consists of:

A. Showing all implementation details  
B. Ignoring important features  
C. Focusing on essential aspects and hiding details  
D. Eliminating documentation

✅ **Correct answer:** **C**

---

## **QCM 10 — Incremental Construction**

Incremental construction means:

A. Building the entire system at once  
B. Adding features step by step  
C. Writing code without testing  
D. Avoiding early versions

✅ **Correct answer:** **B**

---

## **QCM 11 — Software Quality**

In Chapter 1, software quality mainly depends on:

A. The programming language used  
B. The quality of the process  
C. The number of developers  
D. Hardware performance

✅ **Correct answer:** **B**

---

## **QCM 12 — Software Life Cycle**

Which phase comes **first** in the software life cycle?

A. Design  
B. Implementation  
C. Feasibility  
D. Testing

✅ **Correct answer:** **C**

---

## **QCM 13 — Testing Phase**

Which type of test checks individual components?

A. Validation test  
B. System test  
C. Integration test  
D. Unit test

✅ **Correct answer:** **D**

---

## **QCM 14 — Software Development Models**

Which model is considered an **improved version of the Waterfall model**?

A. Tunnel model  
B. Spiral model  
C. Agile model  
D. V-Model

✅ **Correct answer:** **D**

---

## **QCM 15 — Spiral Model**

The Spiral model is characterized by:

A. Linear phases  
B. No testing  
C. Iterative cycles with risk analysis  
D. One final delivery

✅ **Correct answer:** **C**

---

## 🎯 **Quick Exam Tip**

If you can answer **12+ / 15 correctly**, you’re **exam-ready** for Chapter 1.

---

---
## 🔗 Navigation
- **Module:** [[NTIC L3/TQL/TQL|◀ TQL]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
