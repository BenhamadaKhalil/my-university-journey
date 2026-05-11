# 🛠️ Software Maintenance & Evolution — Exam Summary

> 💡 **Core Idea**: Maintenance is not "bug fixing". It is the **entire life** of a software after delivery — and it costs **more** than the initial development.

---

## 📘 Chapter 1 — Introduction to Maintenance

### 🔖 Definitions (cite these in the exam!)

|Source|Definition|
|---|---|
|**IEEE 610.12 (1993)**|Modification of software _after delivery_ to correct faults, improve its attributes, or adapt it to a changing environment|
|**SWEBOK / ISO 14764**|**Totality of activities** required to provide cost-effective support — includes activities **before** delivery!|

> 🧠 **Key Difference**: IEEE = restrictive view (post-delivery). SWEBOK = broader view (full lifecycle, including designing for maintainability from the start).

**Maintenance ≈ Evolution**: Lehman says it is "continuous evolutionary development" on a pre-existing system. We often prefer "evolution" because "maintenance" evokes too strongly the idea of simple mechanical repair.

---

### 💸 Why is it so expensive?

- 📊 Maintenance accounts for **60 to 90%** of the total cost of ownership of software
- ⚡ The **majority** of costs come from evolution (perfective + adaptive), **not bugs**
- 🏗️ Poorly designed software at the start will cost **much** more to maintain

**Concrete example** 🏠: it's like a house. Building it costs X€. But over 30 years, upkeep, renovations, adapting to new standards... costs 2 to 4 times more!

---

### 😤 The Main Challenges

|Challenge|Consequence|
|---|---|
|🏗️ Poor initial design (technical debt)|Every change risks breaking everything|
|📄 Absent or outdated documentation|You have to read the code line by line|
|🧩 Difficult comprehension|**40–60%** of maintenance time = just understanding the code|
|👋 Turnover (developers leaving)|Implicit knowledge disappears with them|
|🌐 Heterogeneous environment|Regression testing becomes very complex|

> 💡 **Exam tip**: if asked why maintenance is difficult → think of these 5 factors!

---

### ⚖️ Lehman's Laws _(very likely to appear in the exam)_

> Lehman observed hundreds of software systems since the 1970s. His laws describe why maintenance is **inevitable**.

| Law     | Name                  | What it says                                                          | Example                                                               |
| ------- | --------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **I**   | Continuing Change     | A software in use MUST be adapted or it progressively becomes useless | Windows XP abandoned → incompatible with the modern web               |
| **II**  | Increasing Complexity | Without active effort, each change adds complexity                    | Adding exceptions to business logic until nobody understands anything |
| **III** | Self Regulation       | The rate of evolution remains relatively stable over time             | A team can only absorb X changes per month                            |
| **IV**  | Declining Quality     | Perceived quality drops if active maintenance is not performed        | Users find the software "increasingly slow and buggy"                 |

> 🎯 **For the exam**: Laws I + II are the **most important**. Law II directly justifies **preventive** maintenance and **re-engineering**.

---

## 🔧 Chapter 2 — The 4 Types of Maintenance

> 🎯 **Method to identify the type**: ask yourself these questions in order:
> 
> 1. Is the software **broken**? → Corrective
> 2. Has the **environment** changed? → Adaptive
> 3. Do we want to **improve** it? → Perfective
> 4. Do we want to **prevent** failures? → Preventive

---

### ❌ 1. Corrective Maintenance

**Trigger**: something is broken (bug, crash, security flaw) **Nature**: **reactive** — we fix what no longer works **Goal**: restore the expected behavior

|Concrete Example|Detail|
|---|---|
|🔐 SQL injection patch|An attacker can access the DB via the login field → we fix it|
|💾 Memory leak|The app slows down after 2 hours of use → we find and fix it|
|💰 Incorrect VAT calculation|The financial module calculates 19% instead of 20% → urgent fix|
|🖥️ Crash on Windows 11|The app crashes at startup on the new OS → fix|

> ⚠️ This is what people associate most with "maintenance" — but it is often the **smallest** part of the actual budget!

---

### 🔄 2. Adaptive Maintenance

**Trigger**: the **environment** has changed, but the software itself is not "broken" **Nature**: reactive or planned — maintaining **compatibility** **Goal**: keep the software working in its new environment

|Trigger|Concrete Example|
|---|---|
|🖥️ New operating system|Migration from Windows 7 to Windows 11 → test and fix incompatibilities|
|🗄️ DBMS update|MySQL 5.7 → MySQL 8.0 → some SQL queries no longer work|
|📜 New regulation|GDPR 2018 → obligation to add cookie consent and right to erasure|
|🔌 Partner API change|The Stripe payment API changes version → adapt the calls|
|☁️ Cloud migration|On-premise application → AWS → architecture to be revised|

> 💡 **Remember**: the software is not broken, it's its **context** that has changed.

---

### ✨ 3. Perfective Maintenance (= Evolutionary)

**Trigger**: we want to make the software **better** or **more suited to needs** **Nature**: proactive or reactive (following user request) **Goal**: increase the value of the software

> 📊 This is often the **largest share** of maintenance costs in the long run!

|Sub-type|Concrete Example|
|---|---|
|➕ New feature|Adding PDF export in an existing report|
|⚡ Performance optimization|An SQL query takes 10s → optimized to 0.3s|
|🎨 UX improvement|Redesigning the login interface to current standards|
|🧹 Refactoring|Splitting a 500-line function into 10 understandable functions|
|🌍 Internationalization|Adding Arabic language to the application|
|🗑️ Removing obsolete features|Removing a feature that 0% of users use|

---

### 🛡️ 4. Preventive Maintenance

**Trigger**: audits, static analysis, identification of future risks **Nature**: **proactive** — act before the failure occurs **Goal**: increase robustness, reduce future costs

|Concrete Example|Why it's preventive|
|---|---|
|🔄 Updating a library|It still works, but a flaw will be discovered in 6 months|
|📝 Improving documentation|Nobody understands this module → document before the author leaves|
|🧪 Adding unit tests|The code "works" but without tests, every change is a risk|
|🧹 Preventive refactoring|Complex module identified by static analysis before it causes bugs|

> ⚠️ Preventive maintenance is often **neglected** due to lack of time/budget — and that's why complexity increases (Lehman's Law II)!

---

### 📊 Summary Table

|Type|Trigger|Nature|Typical Priority|
|---|---|---|---|
|❌ Corrective|Bug, crash, flaw|Reactive|🚨 Urgent|
|🔄 Adaptive|Environment changes|Reactive/planned|📅 Planned|
|✨ Perfective|Need for evolution|Proactive/reactive|📈 Important|
|🛡️ Preventive|Identified future risk|Proactive|🔮 Long-term|

> 🎯 **Trick question**: a security patch = ❌ Corrective (fixes a flaw) AND 🛡️ Preventive (prevents future exploitation). The important thing = identify the **main intention**!

---

## 📏 Chapter 3 — Maintenance Metrics

> **Why measure?** "You can't improve what you don't measure." Metrics transform subjective impressions ("the code is complex") into objective data ("V(G) = 24").

---

### 🏗️ Product Metrics (code quality)

#### LOC / SLOC — Lines of Code

- **What it is**: simply counting lines (physical, logical, or non-empty)
- **Usefulness**: normalizing other metrics (e.g., bugs per KLOC)
- ⚠️ **Trap**: 1000 lines of Java ≠ 1000 lines of Python ≠ 1000 lines of assembly. LOC alone says nothing about complexity!

#### V(G) — McCabe's Cyclomatic Complexity ⭐

> **The most important metric to know for the exam!**

**Formula 1** (easy): `V(G) = number of decisions + 1` **Formula 2** (graph): `V(G) = E − N + 2P`

- E = edges of the control flow graph
- N = nodes
- P = connected components (often = 1)

**What we count**: `if`, `else if`, `while`, `for`, `foreach`, `case`, `&&`, `||`, `?:`

```java
// V(G) calculation example
public String classify(int x, int y) {
    if (x > 0 && y > 0) {     // if = +1, && = +1
        return "both positive";
    } else if (x < 0) {        // else if = +1
        while (y-- > 0) {      // while = +1
            process();
        }
        return "x negative";
    }
    return "other";
}
// V(G) = 4 + 1 = 5
```

**Interpretation**:

- V(G) ≤ 10 → ✅ Simple, easy to test
- 10 < V(G) ≤ 15 → ⚠️ Watch out, notable complexity
- V(G) > 15 → 🚨 Complex, hard to test, high bug risk

> 💡 V(G) also indicates the **minimum number of test cases** to cover all paths!

#### Maintainability Index (MI)

**Formula**: combines average V(G) + average LOC + Halstead Volume (+ sometimes comment rate) **Scale**: 0 to 100

|MI Score|Interpretation|
|---|---|
|> 85|✅ Highly maintainable|
|65–85|⚠️ Average maintainability|
|< 65|🚨 Difficult to maintain|

#### Object-Oriented Metrics

|Metric|Meaning|Good / Bad|
|---|---|---|
|**DIT** (Depth of Inheritance Tree)|Inheritance depth|High = fragile|
|**CBO** (Coupling Between Objects)|Coupling between classes|High = 🚨|
|**LCOM** (Lack of COhesion in Methods)|Lack of cohesion|High = 🚨|
|**NOC** (Number Of Children)|Number of sub-classes|High = strong impact|

> 🎯 OO golden rule: **low coupling + high cohesion** = maintainable code

---

### ⚡ Process Metrics (maintenance efficiency)

#### MTTR — Mean Time To Repair

**Definition**: average time between _detection_ of a bug and its _resolved deployment to production_

**Example**: Bug detected Monday 9am → analyzed → fixed → tested → deployed Thursday 2pm = MTTR of ~77h

- Low MTTR = 🎉 reactive team, efficient process
- High MTTR = 🚨 bottleneck somewhere (analysis? tests? deployment?)

#### Code Churn (Rate of Change)

**Definition**: frequency at which files/modules are modified

- A module modified every week for 6 months = 🚨 instability or unclear requirements
- Combine with V(G): complex module + high churn = **ticking time bomb**

#### Change Failure Rate

**Definition**: % of deployments that cause an incident in production

**Example**: 20 deployments this month, 4 required a rollback = 20% failure rate → 🚨

---

### 🔗 Relationship between product and process metrics

```
High V(G) (product)
    → Difficult comprehension
    → Longer MTTR (process)
    → More reintroduced bugs (process)
    → Higher change failure rate (process)
```

> 💡 **Practical use**: identify modules with V(G) > 15 AND high churn → priority candidates for preventive refactoring!

---

## 🔮 Chapter 4 — Maintenance Forecasting

### 🎯 Why forecast?

- 💰 **Budgeting**: correctly allocate resources
- 🧭 **Strategic decision**: continue / re-engineer / replace?
- ⚠️ **Risk management**: anticipate overruns
- 📋 **SLA contracts**: define realistic service levels

---

### 📐 Effort Estimation Methods

#### Percentage of Development Cost Method

```
Annual maintenance cost ≈ 15% to 25% of initial development cost
```

**Example**: Application developed for 200,000€ → maintenance ≈ 30,000 to 50,000€/year

- ✅ Very quick to calculate
- ❌ Ignores code quality, age, actual complexity

#### COCOMO II (Constructive Cost Model)

Parametric model that takes into account:

- Size (KSLOC = thousands of lines)
    
- Product complexity
    
- Team capabilities
    
- Process maturity
    
- Level of reuse
    
- ✅ More accurate, based on real factors
    
- ❌ Requires historical data for calibration
    

#### Benchmarking

Compare with similar already-completed projects:

- ✅ Based on reality
- ❌ Requires a database of comparable projects

#### Expert Judgment

- ✅ Takes qualitative factors into account
- ❌ Subjective, depends on expert availability

> 💡 **In practice**: 2–3 methods are often combined to cross-check estimates.

---

### ⭐ Impact Analysis — Critical Point!

> **Definition**: process of identifying all potential consequences of a proposed change on the entire system **before** approving and implementing it.

**Analogy** 🏥: like a surgeon who studies scans before operating. You don't cut without knowing what's around!

#### Objectives of impact analysis

1. 🔍 Evaluate the **technical feasibility** of the change
2. ⏱️ Estimate the **effort and cost** of the specific modification
3. 📋 Identify all **impacted elements** (code, documentation, tests)
4. ⚠️ Detect **conflicts** with other changes in progress
5. 🎲 Evaluate **risks** (regression, performance, security)
6. ✅ Make an informed **Go/No-Go** decision

#### Techniques

|Technique|How|Example|
|---|---|---|
|🔗 **Dependency Analysis**|Call graphs, inheritance|"Modifying this class impacts these 7 other classes"|
|🔄 **Traceability**|Links requirements ↔ code ↔ tests|"This requirement is covered by these 3 tests"|
|🔬 **Static Analysis**|Code analysis tools|SonarQube detects dependencies|
|🧪 **Usage Scenarios**|Which use cases are affected?|"The billing and reporting modules use this function"|
|👨‍💼 **Expert Consultation**|Developers who know the system|"The senior dev knows this module has undocumented behavior"|

#### Result of impact analysis

→ A report containing:

- List of impacted elements
- Refined effort estimate
- Risk assessment
- **Go/No-Go recommendation**

---

### 🔑 Factors Influencing Costs

```
🏗️ Technical          👥 Organizational       🌍 Environmental
────────────────────  ──────────────────────   ──────────────────
Complexity             Team competence          OS/DB stability
Code quality           Turnover                 Number of users
Documentation          Defined processes        Market pressure
Age (legacy)           Available tools          Multi-platform
Technology
```

---

## ⚙️ Chapter 5 — Evolution Process Models

### 📋 Key Activities according to IEEE 14764 _(know them in order!)_

```
1. 🏗️ Process Implementation
   └─ Maintenance plan, procedures, tools, training

2. 🔍 Problem Analysis
   └─ RFC reception → classification → priority → impact analysis → approval

3. 🛠️ Modification Implementation
   └─ Design → coding → unit tests → documentation update

4. ✅ Review / Acceptance
   └─ Integration tests → non-regression → UAT → final approval

5. 🚚 Migration
   └─ Move to new environment (if needed)

6. 🗑️ Retirement
   └─ End of life, archiving, user notification
```

> ⚠️ **Exam**: impact analysis is in step 2 (Problem Analysis)!

---

### 🏃 Comparison of Process Models

#### Waterfall

```
Analysis → Design → Implementation → Testing → Deployment
```

- ✅ Simple to manage for very well-defined corrections
- ❌ Rigid, poorly suited to the unpredictable nature of maintenance
- 🎯 **Ideal for**: small, isolated, well-understood corrections

#### Iterative/Incremental

- Short cycles with frequent deliveries
- ✅ More flexible, better adapted to continuous evolution
- 🎯 **Ideal for**: planned evolutionary maintenance

#### 🏃 Scrum (Agile)

```
Sprint Planning → Sprint (2-4 weeks) → Review → Retrospective → ...
```

- The Product Owner manages a **backlog** (prioritized list of bugs + improvements)
- ✅ Very flexible, reactive, continuous improvement through retrospectives
- ❌ Less predictable in the long term
- 🎯 **Ideal for**: managing a product with a mixed backlog (bugs + features)

**Concrete example** 🏃: each 2-week sprint, the team picks the 5 most urgent items from the backlog (2 critical bugs, 3 small improvements), completes them, delivers, and repeats.

#### 📋 Kanban (Agile)

```
[To Do] → [In Progress] → [Testing] → [Done]
   WIP limit: 5     WIP limit: 3    WIP limit: 2
```

- Flow visualization + Work In Progress (WIP) limitation
- ✅ Ideal for continuous and unpredictable task flow
- No fixed sprints → tasks progress as they go
- 🎯 **Ideal for**: continuous corrective maintenance (L2/L3 support)

**Concrete example** 📋: a bug is reported → goes into "To Do" → a dev picks it up ("In Progress") → tests it → "Done". No need to wait for the end of a sprint!

#### IEEE 14764

- Provides the **fundamental activities** integrable into any model
- Not a prescribed lifecycle — it's a **checklist** of essential activities
- 🎯 **Ideal for**: all types, serves as a universal reference

---

### 🚀 DevOps and Maintenance

> DevOps = Dev + Ops → streamline and automate collaboration between teams

**Impact on maintenance:**

- **CI** (Continuous Integration): every commit triggers tests automatically → quick regression detection
- **CD** (Continuous Deployment): fixes reach production quickly (hours/days vs weeks)
- Continuous **Monitoring**: if a deployment causes a problem → the team is immediately alerted
- **Infrastructure as Code**: the environment is versioned and reproducible

**Result**: the boundary between development and maintenance becomes blurred — it is a continuous flow of evolution.

---

## 🔁 Chapter 6 — Re-engineering of Existing Systems

### 🎯 Definition

> Re-engineering = analyzing an existing system (legacy), understanding it in depth, then **transforming and re-implementing** it in an improved form, while preserving its essential functionalities.

**Important distinction:**

- **Restructuring**: improves internal structure without changing the overall architecture
- **Re-engineering**: includes restructuring + possible architecture change + new technologies
- **Forward Engineering**: classic development from specifications

---

### 🧲 The Horseshoe Model _(must know for the exam!)_

```
┌─────────────────────────────────────────────────────┐
│  [Existing System]                                   │
│         │                                           │
│         ↓ ← Reverse Engineering (understand)        │
│  [Abstraction: design, architecture, data]          │
│         │                                           │
│         ↓ ← Transformation (decide the changes)    │
│  [New design / architecture]                        │
│         │                                           │
│         ↓ ← Forward Engineering (rebuild)          │
│  [New improved system]                              │
└─────────────────────────────────────────────────────┘
```

**Analogy** 🏚️→🏠: it's like renovating an old house. First you inspect everything (reverse engineering), decide what to keep/change (transformation), then rebuild (forward engineering). You don't demolish everything!

---

### 🤔 When to decide on re-engineering?

|Warning Signal|Decision Threshold|
|---|---|
|💸 Maintenance costs|Become prohibitive and keep increasing|
|🚧 Functional blockage|Impossible to add critical features|
|💀 Obsolete technology|Unsupported, skills unavailable on the market|
|☁️ Strategic migration|Need to move to cloud or microservices|
|📉 Degraded performance|SLA not met, impossible to optimize|

---

### 🛠️ Re-engineering Techniques

|Technique|Description|Risk|When to use|
|---|---|---|---|
|**Restructuring**|Improve code without changing behavior|Low|Readable but poorly structured code|
|**Wrapping** 🎁|Wrap the old system in a new API|Very low|Stable system but obsolete interface|
|**Data Migration**|ETL to new schema|Medium|DBMS change|
|**Refactoring**|Continuous internal improvement|Low|Reducing technical debt|
|**COTS Replacement**|Replace with a commercial component|Variable|Generic functionality available on the market|
|**Rewrite**|Rebuild from scratch|High|Completely unusable legacy|

> 🎁 **Wrapping**: concrete example — an old COBOL mainframe application that calculates pensions. Rather than rewriting everything, you put a REST API in front of it. New apps call the API, the COBOL still runs behind the scenes.

---

### 🧩 Software Reuse

**During maintenance**:

- Standard libraries/frameworks (avoid reinventing the wheel)
- Reuse existing internal modules

**Re-engineering objective**:

- Extract components into **reusable services** (e.g., microservices)
- Make modules independent → facilitates their reuse in other projects

**COTS replacement**: if an open-source library already does what a legacy module does → replace it!

---

## 🔍 Chapter 7 — Reverse Engineering and Comprehension

### 😰 The Comprehension Challenge

> **Key figure**: 40 to 60% of the total maintenance effort is dedicated to **understanding** the code before being able to modify it!

**Why is it so difficult?**

|Cause|Concrete Example|
|---|---|
|📚 Absent/outdated documentation|The code says `calculate()` but the doc says it does something else|
|👋 Turnover|The dev who coded this module left 3 years ago|
|🏗️ Degraded structure|5 years of "quick fixes" have made the code incomprehensible|
|💾 Legacy code|COBOL application from the 80s, nobody masters it anymore|
|🌐 Millions of lines|Impossible to have a global view|

---

### 🔎 Definition of Reverse Engineering

> Analyzing an existing software system to **identify its components and their relationships**, and create representations at **higher levels of abstraction** than the source code.

**Key point** ⚠️: reverse engineering **does not modify** the system! It produces **knowledge** about the system.

**Difference with re-engineering**:

- Reverse Engineering = **understand** (read only)
- Re-engineering = **understand + transform** (reverse engineering is the 1st step of re-engineering)

---

### 🛠️ Reverse Engineering Techniques

#### Static Analysis (without executing the code)

- Read the source code, identify dependencies
- Tools: code analyzers, call graph generators
- **Results**: who calls whom, which classes depend on which others

#### Dynamic Analysis (by executing the code)

- Profiling, execution traces, debugging
- **Results**: actual program behavior, which functions are called with which data

#### Model Reconstruction

- Generate UML diagrams from code (classes, sequences, states)
- Reconstruct data models (DB schemas)

---

### 🧠 Objectives of Reverse Engineering

1. 💡 **Facilitate comprehension** — provide abstract views to navigate the code
2. 📐 **Recover lost design** — reconstruct undocumented architecture
3. 🔍 **Support impact analysis** — identify dependencies before a modification

---

## 🗂️ Chapter 8 — Configuration Management Tools (SCM)

### 🔑 Fundamental Principles of SCM

**SCM = Software Configuration Management** = managing the evolution of all software artifacts

**3 key activities:**

|Activity|What it does|Example|
|---|---|---|
|**Identification**|Define what to manage and how to identify them|v1.2.3, branch-hotfix-login|
|**Control**|Change approval process|Mandatory code review before merge|
|**Audit**|Complete traceability of modifications|Who changed what, when, why|

---

### 🗃️ WinCVS — Version Management

> CVS = Concurrent Versions System — one of the first version control systems

**Key concepts:**

```
Repository (server)
    ↕
Checkout (local copy) → Modify → Commit (save)
    ↕
Branch (work in parallel) → Merge (reintegrate)
```

**Typical workflow**:

1. `checkout` → retrieve the latest version
2. Modify files locally
3. `commit` → send modifications to the repository with a message
4. If conflict → resolve manually + commit

**Usefulness for maintenance**: being able to go back if a modification breaks something!

---

### 🐛 Bugzilla — Bug Tracking

**Bug workflow**:

```
NEW → ASSIGNED → IN PROGRESS → RESOLVED → VERIFIED → CLOSED
                                    ↘ REOPENED (if not truly fixed)
```

**Important fields**:

- **Severity**: Blocker, Critical, Major, Normal, Minor, Trivial
- **Priority**: P1 (urgent) to P5 (someday maybe)
- **Assigned to**: which developer handles this bug
- **Version**: in which version the bug was found / fixed

**Value for maintenance**:

- Traceability: each fix is linked to a bug report
- History: you can see which modules generate the most bugs (→ targets for refactoring)
- Metrics: average resolution time, number of bugs per version (→ MTTR!)

---

## 🎯 Quick Recap — Everything for the Exam

### ⚡ Identify the type of maintenance (5 seconds)

```
The software crashes / produces wrong results?               → ❌ Corrective
The environment has changed (OS, law, partner API)?         → 🔄 Adaptive
Adding / improving a feature?                               → ✨ Perfective
Refactoring / updating a still-functional library?          → 🛡️ Preventive
```

### 📐 Formulas to know

```
V(G) = number of decisions (if, while, for, case, &&, ||) + 1
V(G) = E - N + 2P  (graph formula)

MI > 85  → ✅ highly maintainable
MI 65-85 → ⚠️ average
MI < 65  → 🚨 problem

Maintenance cost ≈ 15-25% of development cost / year (simple method)
```

### 🧲 Horseshoe Model

```
Reverse Engineering (understand) → Transformation (decide) → Forward Engineering (rebuild)
```

### 🏆 IEEE 14764 — Activities in order

```
1. Process implementation
2. Problem analysis + impact analysis ← key point
3. Modification implementation
4. Review / Acceptance + non-regression tests
5. Migration (if applicable)
6. Retirement (end of life)
```

### ⚖️ Lehman's Laws

```
Law I  → Continuing change inevitable (software must evolve or die)
Law II → Increasing complexity without active effort (justifies prevention + re-engineering)
```

### 🔍 Impact Analysis = MANDATORY before any modification

```
Input  : Change Request (RFC)
Process: Dependencies + traceability + static analysis + experts
Output : Go/No-Go report + estimated effort + identified risks
```

### 📊 Typical distribution of maintenance effort

```
✨ Perfective  ~50%   (new features, optimizations)
🔄 Adaptive    ~25%   (environment changes)
❌ Corrective  ~20%   (bugs)
🛡️ Preventive  ~5%    (often neglected!)
```

> 💡 These figures vary depending on the source, but the order remains the same!

---

_📝 Good luck on the exam! The essentials: master the 4 types, know how to calculate V(G), understand impact analysis, and know Lehman's first 2 laws._
