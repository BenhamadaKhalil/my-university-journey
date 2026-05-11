# CHAPTER 3 — DYNAMIC TESTING (Best Version)

## 1) Dynamic Testing

Dynamic testing = **executing / evaluating** a program (manual or automatic) to:

- verify it meets specifications
    
- detect differences between **expected** and **actual** results
    

⚠️ **Testing can show the presence of defects, never their absence.**

### Key terms (quick recall)

|Term|Meaning|Mini example|
|---|---|---|
|Error|Human mistake|misunderstood requirement|
|Fault (bug)|defect in code/design caused by error|wrong `if` condition|
|Failure|incorrect behavior at runtime|crash / wrong output|

**Oracle** = reference that gives the **expected result** during execution.

---

## 2) Two Test Families

|Family|Also called|Based on|Goal|Example|
|---|---|---|---|---|
|Functional testing|Black-box|specifications|check required behavior|wrong password → refuse login|
|Structural testing|White-box|code/structure|exercise internal logic|cover both branches of an `if`|

---

## 3) Structural Testing Methods (What the course lists)

- **Control-flow coverage** (nodes/statements, arcs/branches, paths)
    
- **Data-flow coverage** (definitions/uses of variables)
    
- **Fault-based (mutation) testing**
    

---

## 4) Control Flow Graph (CFG)

CFG models all possible executions of a method.

|Element|Meaning|
|---|---|
|Node|instruction or block of instructions|
|Arc/Edge|transfer of control|
|Basic block|sequence executed together (no branching inside)|

### CFG rules that often appear in exams

- **Return**: each `return` is a **distinct node**; no arcs between separate return nodes
    
- **Loops**: may require extra “control/dummy” nodes (flow control only)
    
- **Switch/case**: each case is a branch; ends with `break`; has `default`
    

---

## 5) Paths, exec(P,X), and Infeasible Paths

**Activated path**:  
`exec(P, X)` = sequence of CFG nodes traversed when program `P` runs with input `X`.

|Path type|Definition|
|---|---|
|Executable path|∃ input X such that path = exec(P,X)|
|Non-executable (infeasible) path|no input satisfies conditions → cannot be covered by tests|

⚠️ Key theorem (Weyuker 76): deciding executability of a node/arc/path is **undecidable in general**.

---

## 6) Coverage Criteria (Core of Chapter)

### Main control-flow criteria

| Criterion                           | What must be covered                | Measure                     | Notes                                          |
| ----------------------------------- | ----------------------------------- | --------------------------- | ---------------------------------------------- |
| **All nodes** (statement coverage)  | every node reached ≥ 1 time         | covered_nodes / total_nodes | if satisfied → **TER1**                        |
| **All arcs** (branch/edge coverage) | every edge executed ≥ 1 time        | covered_arcs / total_arcs   | if satisfied → **TER2** and TER2 includes TER1 |
| **All paths**                       | all possible paths                  | —                           | impractical with loops (∞ paths)               |
| **All i-paths**                     | loops executed from 0 up to i times | —                           | usually i = 1 or 2 in practice                 |

### Strength relation (course)

**All-paths > All-edges (arcs) > All-nodes.**

### Limits you should mention in exams

|Criterion|What it can miss (course idea)|
|---|---|
|All nodes|may miss an error hidden in a branch not taken (e.g., division by zero)|
|All arcs|loops/special cases may still hide errors (example: error if `inf > sup` leading to division by zero)|

---

## 7) Condition Coverage (logic-focused)

**Condition coverage**: each **atomic condition** must be true and false at least once.

Why it matters (course):

- detects subtle logical errors in compound predicates
    
- ensures each sub-condition has real impact
    

### Branch vs condition (classic)

For `if (A && B)`:

|Coverage type|What you need|
|---|---|
|Branch/arc coverage|2 tests: decision true once, false once|
|Full condition coverage|test A and B separately true/false (stronger)|

⚠️ Course warning: a test set can satisfy condition coverage yet never make the **global predicate true**, so some statements still don’t execute.

---

## 8) Combined Condition Coverage

|Type|Requirement|Problem|
|---|---|---|
|Full combined condition coverage|all T/F combinations of atomic conditions|exponential: n conditions → 2ⁿ tests|
|Optimized combined coverage|keep only combinations that **influence the final decision**|reduces explosion|

Example: `if (A && (B || C))` → 3 conditions → 8 combinations.

---

## 9) Mutation Testing (Fault-based)

|Idea|Meaning|
|---|---|
|Mutant|program version with a small deliberate change|
|Killed mutant ✅|test fails → tests detected the fault|
|Surviving mutant ❌|tests pass → test suite is weak|

---

## 10) Exam Application (Course Exercise)

Program:

```
Lire(a,b,x)
if (a > 1 and b = 0) x := x / a ;
if (a = 2 or x > 1) x := x + 1 ;
ecrire(x)
```

Course result:  
A sequence that satisfies **condition coverage** but **not full statement coverage**:

- (a=1, b=0, x=3)
    
- (a=2, b=1, x=1)
    

---

## 🎓 Final “Must-Memorize” Lines

- Oracle = expected output reference.
    
- `exec(P,X)` = activated path in CFG.
    
- Infeasible paths exist; feasibility is undecidable.
    
- Strength: **All paths > All arcs > All nodes**.
    
- Loops → infinite paths → use **i-paths** (i=1 or 2).
    
- Condition coverage tests atomic conditions T/F; combined is 2ⁿ → optimize.
    

---

---

# ✅ **QCM — Chapter 3: Dynamic Testing**

---

## **QCM 1 — Definition**

Dynamic testing mainly consists of:

A. Reviewing documentation  
B. Executing the program to detect failures  
C. Proving correctness mathematically  
D. Analyzing source code without execution

✅ **Correct answer:** **B**

---

## **QCM 2 — Fundamental Rule**

Which statement is **true**?

A. Testing proves the absence of bugs  
B. Testing eliminates all errors  
C. Testing shows the presence of defects, not their absence  
D. Testing replaces formal verification

✅ **Correct answer:** **C**

---

## **QCM 3 — Oracle**

In software testing, an **oracle** is:

A. A database system  
B. A debugging tool  
C. A mechanism to determine expected results  
D. A test execution environment

✅ **Correct answer:** **C**

---

## **QCM 4 — Test Families**

Which pair represents the **two main testing families**?

A. Unit testing & Integration testing  
B. Static testing & Dynamic testing  
C. Functional testing & Structural testing  
D. Manual testing & Automated testing

✅ **Correct answer:** **C**

---

## **QCM 5 — Functional Testing**

Functional (black-box) testing is based on:

A. Source code structure  
B. Control flow graphs  
C. Program specifications  
D. Algorithm complexity

✅ **Correct answer:** **C**

---

## **QCM 6 — Structural Testing**

Structural (white-box) testing focuses on:

A. User satisfaction  
B. Code execution paths and logic  
C. External interfaces  
D. Documentation quality

✅ **Correct answer:** **B**

---

## **QCM 7 — Control Flow Graph (CFG)**

In a CFG, an **arc (edge)** represents:

A. A basic block  
B. A loop  
C. A transfer of control  
D. A return instruction

✅ **Correct answer:** **C**

---

## **QCM 8 — Path Activation**

The notation **exec(P, X)** represents:

A. Compilation of program P  
B. All possible paths of P  
C. The path executed by program P with input X  
D. The test oracle

✅ **Correct answer:** **C**

---

## **QCM 9 — Infeasible Paths**

A non-executable (infeasible) path is:

A. A path with many nodes  
B. A path not covered by tests yet  
C. A path that cannot be executed by any input  
D. A path inside a loop

✅ **Correct answer:** **C**

---

## **QCM 10 — Decidability**

Determining whether a path is executable is:

A. Easy in all cases  
B. Decidable with enough tests  
C. Undecidable in the general case  
D. Always decidable using CFG

✅ **Correct answer:** **C**

---

## **QCM 11 — Node Coverage**

Node coverage requires:

A. Executing all edges  
B. Executing all paths  
C. Executing all nodes at least once  
D. Executing all conditions

✅ **Correct answer:** **C**

---

## **QCM 12 — Test Effectiveness Ratio**

When **all nodes** are covered, the Test Effectiveness Ratio is:

A. TER = 0  
B. TER = 1  
C. TER = 2  
D. TER = 3

✅ **Correct answer:** **B**

---

## **QCM 13 — Arc Coverage**

Which statement is correct?

A. Arc coverage is weaker than node coverage  
B. Arc coverage includes node coverage  
C. Arc coverage ignores decision branches  
D. Arc coverage is impossible with loops

✅ **Correct answer:** **B**

---

## **QCM 14 — Path Coverage**

Full path coverage is usually impractical because:

A. Programs are too simple  
B. Oracles are unavailable  
C. Loops create an infinite number of paths  
D. Paths are easy to generate

✅ **Correct answer:** **C**

---

## **QCM 15 — i-Path Coverage**

i-Path coverage means:

A. Executing loops exactly i times  
B. Executing all paths once  
C. Executing loops from 0 up to i times  
D. Ignoring loops

✅ **Correct answer:** **C**

---

## **QCM 16 — Strength Relation**

Which relation is **correct**?

A. All nodes > All arcs > All paths  
B. All arcs > All nodes > All paths  
C. All paths > All arcs > All nodes  
D. All nodes > All paths > All arcs

✅ **Correct answer:** **C**

---

## **QCM 17 — Condition Coverage**

Condition coverage requires that:

A. Each branch is executed once  
B. Each atomic condition is true and false at least once  
C. All combinations of conditions are tested  
D. Only global predicates are tested

✅ **Correct answer:** **B**

---

## **QCM 18 — Combined Condition Coverage**

For a condition with **n atomic predicates**, full combined condition coverage requires:

A. n tests  
B. n² tests  
C. 2ⁿ tests  
D. n! tests

✅ **Correct answer:** **C**

---

## **QCM 19 — Optimized Combined Coverage**

Optimized combined condition coverage aims to:

A. Eliminate condition testing  
B. Reduce the number of test cases while preserving effectiveness  
C. Test only true conditions  
D. Replace branch coverage

✅ **Correct answer:** **B**

---

## **QCM 20 — Mutation Testing**

A mutant is **killed** when:

A. The program crashes  
B. The test suite detects the injected fault  
C. The compiler rejects the code  
D. The oracle is missing

✅ **Correct answer:** **B**

---

## 🎯 **Score Guide**

- **17–20** → 🔥 Excellent (very exam-ready)
    
- **13–16** → 👍 Good (revise coverage & conditions)
    
- **<13** → ⚠️ Re-read CFG & coverage criteria
    

---
