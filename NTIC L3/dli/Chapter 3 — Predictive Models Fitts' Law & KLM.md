# 📐 Chapter 3 — Predictive Models: Fitts' Law & KLM

**Module:** Développement de Logiciels Interactifs (ISD) **Prof:** Dr. Dembri Amel · April 2026 **Tags:** #ISD #HCI #predictive-models #Fitts-law #KLM #exam-prep

---

## 📌 What is a Predictive Model?

> A predictive model is an **equation** that estimates the outcome of a variable based on one or more input variables (predictors).

Unlike descriptive models (which _describe_ behavior), predictive models use **numbers** to _predict_ performance.

**What can they predict?**

- ⏱️ **Time / speed** to complete a task
- 🎯 **Accuracy** — error rate, spatial variability
- Any measure of human behavior expressed as **continuous or ratio-scale data**

**Two major predictive models in this chapter:**

```
┌──────────────────────────────────────────────────────────┐
│  Chapter 3 — Two Predictive Models                       │
│                                                          │
│  1. 🎯 FITTS' LAW        2. ⌨️ KLM                      │
│     Predicts movement       Predicts task completion     │
│     time to a target        time step-by-step            │
│     (pointing speed)        (expert users, no errors)    │
└──────────────────────────────────────────────────────────┘
```

---

## 🎯 Model 1 — Fitts' Law

### Background

> In **1954**, psychologist **Paul Fitts** discovered that the time needed to reach a target **increases with distance** and **decreases as the target gets larger**.

The core trade-off: **moving quickly toward a small target → more errors** (speed-accuracy trade-off).

> 💡 Originally NOT created for UI design — but it strongly influences how we design websites, apps, and interactive systems today.

---

### 3 Uses of Fitts' Law in HCI

```
┌─────────────────────────────────────────────────────────────────┐  
│               3 USES OF FITTS' LAW IN HCI                      │
│                                                                 │
│  1. 🔬 GOODNESS OF FIT                                         │
│     Test if a device/interaction technique follows the law.     │
│     → Build a prediction equation, measure how well data fits   │
│                                                                 │
│  2. ⚖️ COMPARE DESIGN ALTERNATIVES                             │
│     Use the equation to predict which design option lets        │
│     users perform faster or more accurately.                    │
│                                                                 │
│  3. 📊 MEASURE PERFORMANCE                                      │
│     Use Fitts' Index of Performance (= Throughput) as a        │
│     dependent variable to compare devices or techniques.        │
└─────────────────────────────────────────────────────────────────┘
```

---

### 📐 The Formula

**Movement Time (MT):**

```
MT = a + b × ID
 
Where:
  MT  = Movement Time (seconds)
  a   = constant (reaction/startup time, depends on device)
  b   = constant (movement speed, depends on device)
  ID  = Index of Difficulty (bits)
```

**Simplified version:**

```
MT = 1 × ID     (where 1 is a constant ≈ 100 ms)
```

**Index of Difficulty (ID):**

```
        ┌    2D  ┐
ID = log│  ────  │
      2 └    W   ┘

Where:
  D = Distance to the target  (also written as A = Amplitude)
  W = Width of the target
  log₂ = base-2 logarithm
```

> 🔑 **Core insight:** Closer targets + bigger targets = **lower ID** = **less time needed**

---

### 📊 Fitts' Law — Visual Intuition

```
    TIME TO REACH TARGET
         ▲
         │                              ● small + far  (hardest)
         │                    ●
         │            ●  small + close
         │    ●
         │  large + far
         │●
         │  large + close  (easiest)
         └─────────────────────────────►
                    DIFFICULTY (ID)

    ↑ distance  →  ↑ MT        (farther = slower)
    ↓ width     →  ↑ MT        (smaller = slower)
    ↑ width     →  ↓ MT        (bigger = faster)
    ↓ distance  →  ↓ MT        (closer = faster)
```

---

### 🧮 Exercise 1 — Solved (a = 0.4, b = 0.2)

Formula step by step:

```
ID  = log₂(2D / W)
MT  = a + b × ID
```

| Button W | Distance D | ID = log₂(2D/W)                  | MT = 0.4 + 0.2 × ID |
| -------- | ---------- | -------------------------------- | ------------------- |
| 60 px    | 100 px     | log₂(200/60) = log₂(3.33) ≈ 1.74 | **0.75 s**          |
| 10 px    | 100 px     | log₂(200/10) = log₂(20) ≈ 4.32   | **1.26 s**          |
| 60 px    | 50 px      | log₂(100/60) = log₂(1.67) ≈ 0.74 | **0.55 s**          |
| 10 px    | 50 px      | log₂(100/10) = log₂(10) ≈ 3.32   | **1.06 s**          |

> ✅ **Conclusion:** Movement time increases when the target is **smaller** or **farther away**.

---

### 🍕 Exercise 2 — Menu Types Evaluated by Fitts' Law

```
┌────────────────────────────────────────────────────────────────────┐
│                    THREE MENU TYPES                                │
│                                                                    │
│  LINEAR MENU          RECTANGULAR MENU        PIE MENU            │
│                                                                    │
│  ┌──────────┐         ┌────────┬────────┐     ╭────────╮          │
│  │ Option 1 │ ←close  │ Opt 1  │ Opt 4  │      Option 1           │
│  │ Option 2 │         │ Opt 2  │ Opt 5  │   ╭─╮   ╭─╮             │
│  │ Option 3 │         │ Opt 3  │ Opt 6  │  Opt8 ● Opt2            │
│  │ Option 4 │         └────────┴────────┘   ╰─╯   ╰─╯             │
│  │ Option 5 │                               Opt7 MENU Opt3        │
│  │ Option 6 │ ←far                           ╭─╯   ╰─╮            │
│  │ Option 7 │                               Opt6   Opt4            │
│  └──────────┘                                  Option 5            │
│                                                                    │
│  Distance varies      Avg distance smaller    All options at       │
│  top→bottom           than linear             equal distance       │
└────────────────────────────────────────────────────────────────────┘
```

| Menu               | Description                              | Fitts' Law Evaluation                                                                                                  |
| ------------------ | ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 📋 **Linear**      | Items arranged in a vertical line        | Distance increases from first to last item. Place **frequently used items at the top** to reduce selection time.       |
| 🔲 **Rectangular** | Items in rows and columns (2D)           | Average distance to items is **smaller** than linear → can improve speed.                                              |
| 🥧 **Pie**         | Items arranged in a circle around center | **All items at equal distance** → equal selection time for all. But less familiar to users, which adds cognitive cost. |

---

### ✅ Design Rules from Fitts' Law

```
┌────────────────────────────────────────────────────────────┐
│              FITTS' LAW DESIGN RULES                       │
│                                                            │
│  🔴 MAKE BUTTONS LARGE                                     │
│     Especially on touch devices (fingers are imprecise)    │
│                                                            │
│  🔵 KEEP BUTTONS CLOSE to where the user's attention is    │
│     Minimize distance between related elements             │
│                                                            │
│  🟢 PREFER SHORT DROPDOWN LISTS over long ones             │
│     Less distance to scroll = faster selection             │
│                                                            │
│  🟡 SCREEN EDGES & CORNERS are "infinite size" targets     │
│     The cursor can't go past them → easy to hit!           │
│     (Used by macOS menu bar at top of screen)              │
└────────────────────────────────────────────────────────────┘
```

> ⚠️ **Applies to:** pointing actions (mouse, finger, stylus). NOT for continuous movements like drawing.

---

## ⌨️ Model 2 — Keystroke-Level Model (KLM)

### What is KLM?

> KLM is a predictive model created by **Card, Moran & Newell**. Its goal: **predict how long an expert user takes to complete a task without errors**.

A **keystroke** = pressing one key on the keyboard once.

---

### 5 Key Elements of KLM

```
┌────────────────────────────────────────────────────────────────┐
│                 5 KEY ELEMENTS OF KLM                         │
│                                                                │
│  1. 📋 THE TASK                                                │
│     What the user is trying to accomplish.                     │
│     Can be broken into sub-tasks.                              │
│     e.g. "Print a document" = open file + select print +      │
│           choose printer + confirm                             │
│                                                                │
│  2. 🔀 THE METHOD                                              │
│     The specific way chosen to do the task.                    │
│     Same task, multiple methods exist.                         │
│     e.g. Save = Ctrl+S  OR  File → Save  OR  toolbar button   │
│                                                                │
│  3. 💬 COMMAND LANGUAGE OF THE SYSTEM                          │
│     How the system accepts input: typed commands, menus,       │
│     button clicks, voice. Complexity affects total time.       │
│                                                                │
│  4. 💪 MOTOR SKILL PARAMETERS                                  │
│     User's physical actions: typing speed, mouse precision,    │
│     reaction time. KLM uses standard values for expert users.  │
│                                                                │
│  5. ⚡ SYSTEM RESPONSE TIME                                    │
│     How fast the system reacts. A slow system increases        │
│     total time even if the user is perfect.                    │
└────────────────────────────────────────────────────────────────┘
```

---

### 🔑 The KLM Operators Table

Each primitive action has a standard time cost:
 

| Operator | Action                                 | Time                                       |
| -------- | -------------------------------------- | ------------------------------------------ |
| **K**    | Press a key or button                  | Varies by typist (see below)               |
| **P**    | Point with a mouse (Fitts' Law based)  | **1.10 s**                                 |
| **H**    | Home hands to keyboard or device       | **0.40 s**                                 |
| **D**    | Draw n straight-line segments          | 0.9n + 0.16/D s                            |
| **M**    | Mentally prepare (think before acting) | **1.35 s**                                 |
| **R(t)** | Wait for system Response               | t seconds (counted only if user must wait) |

**K operator — typing speed breakdown:**

```
┌──────────────────────────────────────────────────────┐
│         TYPING SPEED → TIME PER KEYSTROKE            │
│                                                      │
│  🥇 Best typist          135 wpm  →  0.08 s/key     │
│  ✅ Good typist           90 wpm  →  0.12 s/key     │
│  📊 Average skilled       55 wpm  →  0.20 s/key     │
│  📝 Average non-sec.      40 wpm  →  0.28 s/key     │
│  🔡 Random letters          —     →  0.50 s/key     │
│  💻 Complex codes           —     →  0.75 s/key     │
│  🐢 Worst (unfamiliar)      —     →  1.20 s/key     │
│                                                      │
│  How? 135 wpm × 5 chars = 675 chars/min              │
│       675 / 60 = 11.25 chars/sec                     │
│       1 / 11.25 ≈ 0.08 s/keystroke ✓                │
└──────────────────────────────────────────────────────┘
```

---

### 🧮 Total Execution Time Formula

```
t_EXECUTE = t_K + t_P + t_H + t_D + t_M + t_R

→ Sum the time of every individual operator in the task sequence.

Example: typing "abc"
  t_K = t_a + t_b + t_c = 3 × t_ki
```

---

### 🧮 Exercise 1 — Type "Ali" + Enter (solved)

User: average skilled typist → 0.20 s/keystroke

```
Task: Think → Home hands → Type A, l, i → Press Enter

Operators:  M   +  H  +  4K
Time:      1.35 + 0.40 + 4 × 0.20
         = 1.35 + 0.40 + 0.80
         = 2.55 seconds ✓
```

---

### 🧮 Exercise 2 — Print a Document: Two Methods Compared

**Method 1: Keyboard Shortcut (Ctrl + P)**

```
Think → Home → Press Ctrl → Press P → Think → Press Enter

Operators:  M  +  H  +  2K  +  M  +  K
Time:      1.35 + 0.40 + 2×0.20 + 1.35 + 0.20
         = 1.35 + 0.40 + 0.40 + 1.35 + 0.20
         = 3.70 seconds

→ Best for EXPERT users who know shortcuts 🧑‍💻
```

**Method 2: Menu Navigation (File → Print)**

```
Think → Home → Point File → Click → Think → Point Print →
Click → Think → Point Enter → Click

Operators:  M  +  H  +  P  +  K  +  M  +  P  +  K  +  M  +  P  +  K
Time:      1.35+0.40+1.10+0.20+1.35+1.10+0.20+1.35+1.10+0.20
         = 8.35 seconds
         

→ Typical of NOVICE users unfamiliar with shortcuts 🧑‍🎓
```

**Comparison:**

```
┌──────────────────────────────────────────────────────────────┐
│              SHORTCUT vs MENU — PRINT ACTION                 │
│                                                              │
│  ⌨️ Ctrl + P   →  3.70 s   ████░░░░░░░░░░░░░░░  FAST         │
│  🖱️ File>Print →  8.35 s   ████████████████████  SLOW        │
│                                                              │
│  Difference: 8.35 - 3.70 = 4.65 seconds per print!           │
│  Over 100 prints = 7.75 minutes lost using menus             │
└──────────────────────────────────────────────────────────────┘
```

---

### 📚 KLM Applied — Common Task Examples

| Task                 | Method A (faster)           | Method B (slower)            |
| -------------------- | --------------------------- | ---------------------------- |
| 💾 Save a document   | `Ctrl+S`                    | File → Save                  |
| 📨 Send a message    | Select from suggestion list | Type recipient name manually |
| 📋 Copy & paste      | `Ctrl+C` / `Ctrl+V`         | Right-click → context menu   |
| 🔍 Search for a file | Type in search bar          | Navigate folders manually    |
| 🔍 Zoom into image   | Keyboard shortcut           | Click zoom button repeatedly |

---

### ✅ When to Use KLM — and When NOT To

```
┌──────────────────────────────┐  ┌──────────────────────────────┐
│    ✅ USE KLM WHEN...        │  │    ❌ DON'T USE KLM WHEN...  │
├──────────────────────────────┤  ├──────────────────────────────┤
│ • You know the exact         │  │ • Interactions are NOT       │
│   sequence of actions        │  │   clearly defined in advance │
│   needed for the task        │  │                              │
│                              │  │ • Tasks involve exploration, │
│ • You want to compare        │  │   creativity, or open-ended  │
│   two interface designs      │  │   behaviors                  │
│                              │  │                              │
│ • You're evaluating          │  │ • Users may make errors      │
│   expert performance         │  │   (KLM assumes error-free)   │
└──────────────────────────────┘  └──────────────────────────────┘
```

---

## 🧠 Chapter Summary — Both Models at a Glance
|Model|Fitts' Law|KLM|
|---|---|---|
|**Created by**|Paul Fitts (1954)|Stuart Card, Thomas P. Moran & Allen Newell|
|**Predicts**|Time to point/select a target|Total expert task completion time|
|**Key formula**|( MT = a + b \times \log_2(2D/W) )|( t = \Sigma(t_K + t_P + t_H + t_M + t_R) )|
|**Main variables**|Distance (D) and Width (W)|Keystroke, Pointing, Homing, Mental, Response|
|**Best for**|UI layout and target/button sizing|Comparing interface interaction efficiency|
|**User type**|General users|Expert users only|
|**Errors**|Includes speed–accuracy trade-off|Assumes error-free performance|
|**Focus**|Single pointing action|Entire interaction sequence|

---

## ⚡ Quick Recall — Exam Cheat Sheet

- **Fitts' Law:** MT = a + b × ID · ID = log₂(2D/W) · **bigger + closer = faster**
- **Fitts' 3 uses:** goodness of fit · compare alternatives · measure throughput
- **KLM operators:** K (key) · P (point, 1.10s) · H (home, 0.40s) · M (mental, 1.35s) · R (response)
- **KLM formula:** t_EXECUTE = tK + tP + tH + tD + tM + tR
- **KLM assumes:** expert users · no errors · predefined sequence
- **Shortcut vs Menu** print example: **3.70s vs 8.35s**
- **Pie menu advantage:** all items at equal distance from center
- **Linear menu tip:** put most-used items at the top

---

_📁 ISD · Chapter 3 of N · Links: [[Chapter 2 — Descriptive & Predictive Models of the Human]]] | Next: [[Chapter 4 — Design & Implementation of Interactive Systems]]]_

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DLI/DLI|◀ DLI]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
