# 🎨 Chapter 4 — Design & Implementation of Interactive Systems

**Module:** Développement de Logiciels Interactifs (ISD) **Prof:** Dr. Dembri Amel · April 2026 **Tags:** #ISD #HCI #UCD #usability #Nielsen #heuristics #design-process #exam-prep

---

## 📌 The Goal: What Are We Designing For?

> **Technology must adapt to humans — not the other way around.**

A good interface must be:

```
┌─────────────────────────────────────────────────────────────┐
│              3 GOALS OF HCI INTERFACE DESIGN                │
│                                                             │
│  1. 🧠 EASY TO USE                                          │
│     Intuitive (بديهي) and natural                           │
│     Users just know what to do without thinking             │
│                                                             │
│  2. ⚡ EFFICIENT + EFFECTIVE                                │
│     Efficiency  (كفاءة)  → Users accomplish tasks QUICKLY   │
│     Effectiveness (فعالية) → Users accomplish tasks ACCURATELY│
│                                                             │
│  3. ♿ ACCESSIBLE TO ALL USERS                              │
│     Works for everyone, regardless of ability or background │
└─────────────────────────────────────────────────────────────┘
```

> ⚠️ **Efficiency ≠ Effectiveness** — a common exam trick!
> 
> - Efficiency = **how fast** (speed)
> - Effectiveness = **how accurately** (quality of outcome) 

---

## 🎯 Usability — The Core Concept

> **Usability (ISO 9241-11):** How well a defined group of users can use a product to accomplish specific goals **effectively, efficiently, and with satisfaction** within a particular context.

This approach is called **User-Centered Design (UCD)**.

**Product development must be guided by:**

- ✅ User needs and capabilities
- ❌ NOT just technological possibilities

---

## 📋 ISO Standards for Interactive Systems Design

> A system can function perfectly — and still **fail its users**. Technical performance alone is not enough.

**ISO standards ensure systems are:**

- Designed around real user needs
- Evaluated systematically
- Safe, usable, and effective
- Consistent across industries and countries

```
┌────────────────────────────────────────────────────────────┐
│               ISO TIMELINE FOR UCD                         │
│                                                            │
│  1999 → ISO 13407                                          │
│         Introduced User-Centered Design (UCD)              │
│                                                            │
│  2010 → ISO 9241-210                                       │
│         Modernized into Human-Centered Design (HCD)        │
│         (the current standard)                             │
│                                                            │
│  ISO = global organization that defines international      │
│        standards                                           │
└────────────────────────────────────────────────────────────┘
```

---

## 🔄 When Should Usability Be Checked?

```
┌─────────────────────────────────────────────────────────────────┐
│            THE USABILITY PROBLEM — 3 COMPANY TYPES             │
│                                                                 │
│  ❌ BAD COMPANIES                                               │
│     HCI experts called in AFTER the product is built.           │
│     Only when it proves unusable do they ask for help.          │
│     → Very expensive to fix at this stage!                      │
│                                                                 │
│  ⚠️ AVERAGE COMPANIES                                           │
│     Usability = testing only. Check if people can use it,       │
│     then patch problems found after the fact.                   │
│                                                                 │
│  ✅ BEST COMPANIES                                              │
│     Usability is DESIGNED IN from the very start.               │
│     Prevention is cheaper than cure!                            │
└─────────────────────────────────────────────────────────────────┘
```

> 💡 **Key principle:** Even if a good design process is used, you still need to assess and test the final system to ensure it actually meets user requirements.

---

## 🔁 The Interaction Design Process — 4 Phases + Loop

The design of interaction follows **4 main phases with an iteration loop**:

```
┌─────────────────────────────────────────────────────────────────────┐
│              INTERACTION DESIGN PROCESS                            │
│                                                                     │
│   ┌─────────────┐                                                   │
│   │ 📋 What is  │                                                   │
│   │   wanted    │◄────────────────────────────────┐                │
│   └──────┬──────┘                                 │                │
│          │                                        │                │
│          ▼                                        │                │
│   ┌─────────────┐        ┌────────────┐           │                │
│   │ 🔍  ANALYSIS│───────►│ 🎨 DESIGN  │___        │                │
│   │             │◄──┐    └─────┬──────┘   |        │                │
│   └─────────────┘   │          │          |        │                │
│          ▲           │          ▼         |         │                │
│          │    ┌──────┴──────────────────┐ |         │                │
│   Eval / │    │    🧪 PROTOTYPE         │ |        │                │
│ Heuristic│    └─────────────────────────┘ |         │                │
│          │                 │              |         │                │
│          └─────────────────┘              |         │                │
│                                           ▼         │                │
│   ┌──────────────────────────────────────────┐     │                │
│   │  🚀 IMPLEMENT & DEPLOY ──────────────────┼─────┘                │
│   └──────────────────────────────────────────┘                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Phase Details

| Phase                     | What happens                                                                      | Tools / Techniques                                      |
| ------------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------- |
| 📋 **Requirements**       | Find out what users need — watch and talk to them                                 | Interviews, observation, video recording                |
| 🔍 **Analysis**           | Organize results, identify key problems and needs                                 | Task models, scenarios, interaction stories             |
| 🎨 **Design**             | Move from _what_ is wanted to _how_ to achieve it, guided by rules and heuristics | Design notations, navigation structures, screen layouts |
| 🚀 **Implement & Deploy** | Build and release the final product                                               | Code, hardware, documentation                           |

### 🧪 The Prototype Loop

```
Design → Prototype → Evaluate → OK? → Done!
                  ↑                ↓ (not OK)
                  └──── Redesign ──┘
```

> ⚠️ **Key challenge of prototyping:** The hard part isn't _finding_ usability problems — it's deciding **which ones are worth fixing** given time and budget constraints.

---

## 📏 Design Rules & Evaluation Frameworks

Three widely recognized sets of heuristics for evaluating usable systems:

```
┌──────────────────────────────────────────────────────────────┐
│           3 MAJOR DESIGN RULE FRAMEWORKS                     │
│                                                              │
│  🔟 Nielsen's 10 Heuristics    ← Most commonly used          │
│  8️⃣  Shneiderman's 8 Golden Rules                            │
│  7️⃣  Norman's 7 Principles     ← See Chapter 2 (Theory of    │
│                                   Action)                    │
└──────────────────────────────────────────────────────────────┘
```

---

## 🔍 Heuristic Evaluation — What & How

> A **heuristic** is a simple rule or guideline used to help design or evaluate a system.

> **Heuristic evaluation** is a method where a few experts check a system using these rules to find usability problems.

**Properties:** Quick ✅ · Flexible ✅ · Low-cost ✅ · Any stage ✅ (early designs, prototypes, or finished systems)

### How It Works:

```
┌──────────────────────────────────────────────────────────────┐
│              HEURISTIC EVALUATION PROCESS                    │
│                                                              │
│  Step 1: 4–5 evaluators review the system INDEPENDENTLY      │
│  Step 2: Each checks against the 10 heuristics               │
│  Step 3: Each problem gets a SEVERITY RATING                 │
│  Step 4: Team fixes the most critical problems FIRST         │
│                                                              │
│  → Key insight: Finding problems is easy.                    │
│    The challenge is deciding which ones to fix first!        │
└──────────────────────────────────────────────────────────────┘
```

### Severity Rating Scale:

| Score | Meaning          | Action                              |
| ----- | ---------------- | ----------------------------------- |
| **0** | Not a problem    | Ignore                              |
| **1** | Small issue      | Fix only if extra time available    |
| **2** | Minor problem    | Low priority                        |
| **3** | Major problem    | Should be fixed                     |
| **4** | Critical problem | 🔴 **MUST be fixed before release** |

---

## 📋 Nielsen's 10 Heuristics — Complete Reference

### H1 · 👁️ Visibility of System Status

> Always tell users what's happening.

```
❌ File uploads with no indicator — user can't tell if it's working or frozen
✅ Fix: Progress bar showing "47% complete" during upload
```

---

### H2 · 🌍 Match Between System and the Real World

> Use familiar language, not technical terms. Follow real-world conventions.

```
❌ Using an unusual, unfamiliar icon for "delete"
✅ Fix: Trash / Recycle Bin icon — users already know what it means
```

---

### H3 · 🕹️ User Control and Freedom

> Let users undo mistakes easily. Support undo and redo.

```
❌ Deleting files with no way to confirm or recover
✅ Fix: Undo / Redo functions, Cancel buttons on dialogs, "Are you sure?" prompts
```

---

### H4 · 🔁 Consistency and Standards

> Keep everything uniform. Follow platform conventions users already know.

```
❌ Inventing a new shortcut for "Copy" that no one expects
✅ Fix: Ctrl+C always means Copy. "Save" button always in the same place across all pages.
```

---

### H5 · 🛡️ Error Prevention

> Better to prevent errors than to fix them after they happen.

```
❌ Allowing form submission with missing required fields
✅ Fix: Confirmation dialogs, form validation before submission, disabled invalid options
```

---

### H6 · 👀 Recognition Rather Than Recall

> Make objects, actions, and options visible. Users shouldn't have to memorize.

```
❌ Requiring users to type commands from memory (like old CLI systems)
✅ Fix: Dropdown menus showing all options · Browser autocomplete · Icons with labels
```

> 💡 Connected to STM (7±2 chunks) from Chapter 2 — reduce memory load!

---

### H7 · ⚡ Flexibility and Efficiency of Use

> Support both beginners and experts. Allow users to tailor frequent actions.

```
❌ Only one slow way to do everything
✅ Fix: Multiple methods for same action:
        Beginner → Edit menu → Copy
        Expert   → Ctrl+C (shortcut, hidden from novice view)
```

---

### H8 · 🎨 Aesthetic and Minimalist Design

> Show only relevant information. Every extra element competes for attention.

```
❌ Dialogs cluttered with rarely-needed technical information
✅ Fix: Show only what's needed for the task. Remove anything unnecessary.
```

---

### H9 · 🔧 Help Users Recognize, Diagnose & Recover From Errors

> Error messages should be in plain language, identify the problem, and suggest a solution.

```
❌ Showing just "Error 404" — user has no idea what went wrong or what to do
✅ Fix: "Page not found. Try going back to the homepage or searching for what you need."
```

---

### H10 · 📖 Help and Documentation

> Few systems can be used with zero instructions. Help should be easy to find.

```
Good help documentation:
  ✅ Focused on the user's task
  ✅ Lists concrete steps to follow
  ✅ Not too large or overwhelming
  ✅ Easy to find (search, tooltips, contextual help)
```

---

## 🧠 All 10 Heuristics — Quick Reference Table

| #   | Heuristic                   | One-word memory hook | Bad example               | Fix                           |
| --- | --------------------------- | -------------------- | ------------------------- | ----------------------------- |
| 1   | Visibility of system status | **FEEDBACK**         | No upload indicator       | Progress bar                  |
| 2   | Match with real world       | **FAMILIAR**         | Weird delete icon         | Trash can 🗑️                 |
| 3   | User control & freedom      | **ESCAPE**           | No undo/redo              | Ctrl+Z support                |
| 4   | Consistency & standards     | **UNIFORM**          | Random shortcuts          | Ctrl+C = always Copy          |
| 5   | Error prevention            | **PREVENT**          | No form validation        | Disabled invalid options      |
| 6   | Recognition not recall      | **VISIBLE**          | Type commands from memory | Dropdown menus                |
| 7   | Flexibility & efficiency    | **SHORTCUT**         | One slow method for all   | Menu + keyboard shortcut      |
| 8   | Aesthetic & minimalist      | **MINIMAL**          | Cluttered dialogs         | Only relevant info shown      |
| 9   | Error recovery              | **DIAGNOSE**         | "Error 404" only          | Plain-language error + fix    |
| 10  | Help & documentation        | **SUPPORT**          | No help available         | Searchable, task-focused help |

---

## 🧠 Chapter Summary — Big Picture

```

┌─────────────────────────────────────────────────────────────────────┐
│                    CHAPTER 4 BIG PICTURE                            │
│                                                                     │
│   GOAL: Maximum Usability                                           │
│      → Effective + Efficient + Satisfying (ISO 9241-11)             │
│                                                                     │
│   APPROACH: User-Centered Design (UCD)                              │
│      → Technology adapts to humans, not the other way               │
│                                                                     │
│   PROCESS: 4 Phases with iteration loop                             │
│      Requirements → Analysis → Design → Prototype → Evaluate → ...  │
│                                                                     │
│   EVALUATION TOOL: Heuristic Evaluation                             │
│      → 4–5 experts · 10 rules · Severity ratings 0–4               │
│      → Quick, flexible, low-cost                                    │
│                                                                     │
│   THE 10 RULES: Nielsen's Heuristics                                │
│      Status · Real world · Freedom · Consistency · Prevention ·     │
│      Recognition · Flexibility · Minimalism · Recovery · Help       │
└─────────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Quick Recall — Exam Cheat Sheet

- **Usability (ISO 9241-11):** effectively + efficiently + with satisfaction
- **Efficiency vs Effectiveness:** speed vs accuracy (don't mix them up!)
- **UCD:** design guided by user needs, NOT just technology
- **ISO 13407 (1999):** introduced UCD · **ISO 9241-210 (2010):** modern HCD standard
- **4 design phases:** Requirements → Analysis → Design → Implement & Deploy
- **Prototype loop:** Design → Prototype → Evaluate → Redesign (until OK)
- **Heuristic evaluation:** 4–5 independent experts · rate 0–4 · fix worst first
- **Severity 4:** critical, must fix before release
- **3 heuristic frameworks:** Nielsen (10) · Shneiderman (8) · Norman (7)
- **Most important heuristics for exam:** H1 (feedback), H3 (undo), H5 (prevent errors), H6 (recognition not recall), H9 (error recovery)

---

_📁 ISD · Chapter 4 (Final Chapter) · Links: [[Chapter 3 — Predictive Models Fitts' Law & KLM]] | [[Chapter 2 — Descriptive & Predictive Models of the Human]] | [[Chapter 1 — Interactive Software & Human-Computer Interaction]]_

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DLI/DLI|◀ DLI]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
