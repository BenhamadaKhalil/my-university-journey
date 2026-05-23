# 🧠 Chapter 2 — Descriptive & Predictive Models of the Human

**Module:** Développement de Logiciels Interactifs (ISD) **Prof:** Dr. Amel Dembri · March–April 2026 **Tags:** #ISD #HCI #descriptive-models #human-processor #Norman #exam-prep

---

## 📌 Introduction — Why Models?

HCI has evolved through three major interface eras:

```
1940s–1970s  →  💻 Command Line Interfaces (CLI)
                 Users type precise text commands
                 
1980s        →  🖱️ Graphical User Interfaces (GUI)
                 Mouse + keyboard, visual icons
                 
2000s–Now    →  👆 Natural User Interfaces (NUI)
                 Touch, voice, gestures
```

> 💡 **What is a model?** A model is a **simplification of reality**. It allows us to explore phenomena, think about them, and make changes. Models in HCI are tools for **thinking** and **predicting** human behavior.

**Two types of models in this chapter:**

| Type               | Purpose                                | Examples                                  |
| ------------------ | -------------------------------------- | ----------------------------------------- |
| 📝 **Descriptive** | Describe and categorize human behavior | Human Processor, Newell's Time Scale, KAM |
| 📊 **Predictive**  | Predict how users will perform tasks   | Norman's 7 Stages of Action               |

> ⚠️ **Why study humans?** The more we understand humans, the better our chances of designing interactive systems that work as intended.

---

## 🤖 Model 1 — The Human Processor Model (MHP)

### The Big Idea

The human is viewed **by analogy with a computer** — as an information-processing system with three interdependent subsystems, each with its own processor and memory.

```
┌─────────────────────────────────────────────────────────────────┐
│                    HUMAN PROCESSOR MODEL                        │
│                                                                 │
│   HUMAN                INTERFACE                COMPUTER        │
│   ┌──────┐            ╔═══════════╗            ┌──────────┐    │
│   │      │◄──────────╢  Displays  ╟────────────│          │    │
│   │ 🧠   │            ╚═══════════╝            │ Machine  │    │
│   │Brain │                 ║                   │  State   │    │
│   │      │            ╔═══════════╗            │          │    │
│   │      │───────────►║ Controls  ╟───────────►│          │    │
│   └──────┘            ╚═══════════╝            └──────────┘    │
│   Sensors &                                                     │
│   Responders          ← interaction happens here →              │
└─────────────────────────────────────────────────────────────────┘
```

> 🧪 **Example:** You see an error on screen (sensor) → brain processes it (cognitive) → your hands type a fix (motor/responder).

---

### 👁️ The Sensors — Entry Points for Information

Sensors convert physical phenomena (light, sound, pressure) into nerve signals sent to the brain.

| Sense          | How it works                           | Key fact for HCI                                                 |
| -------------- | -------------------------------------- | ---------------------------------------------------------------- |
| 👁️ **Vision** | Light → lens → retina → optic nerve    | 80% of our information comes through sight!                      |
| 👂 **Hearing** | Sound waves → eardrum → nerve impulses | Used for alerts, feedback sounds                                 |
| ✋ **Touch**    | Cutaneous sensors in skin              | Includes body position (proprioception) & movement (kinesthesis) |
| 👃 **Smell**   | ~10 main odor categories               | Closely linked to memory & emotions                              |
| 👅 **Taste**   | Gustatory system                       | Less relevant for digital HCI                                    |

> 💡 **Vision detail:** Eyes work through **fixations** (≥200ms — when we actually read/see) and **saccades** (30–120ms — rapid jumps between fixation points). Good UI design considers where the eye naturally lands!

---

### 🔄 The Three Subsystems

```
┌─────────────────────────────────────────────────────────────────┐
│              THREE INTERDEPENDENT SUBSYSTEMS                    │
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌────────────────┐  │
│  │  👁️ PERCEPTUAL  │  │  🧠 COGNITIVE   │  │  💪 MOTOR     │  │
│  │    SYSTEM       │  │    SYSTEM       │  │   SYSTEM      │  │
│  ├─────────────────┤  ├─────────────────┤  ├────────────────┤  │
│  │ Entry point for │  │ Processes &     │  │ Translates     │  │
│  │ all incoming    │→ │ interprets      │→ │ decisions into │  │
│  │ information     │  │ information,    │  │ physical       │  │
│  │                 │  │ makes decisions │  │ actions        │  │
│  ├─────────────────┤  ├─────────────────┤  ├────────────────┤  │
│  │ Uses:           │  │ Uses:           │  │ Uses:          │  │
│  │ • Sensory mem.  │  │ • STM           │  │ • Motor memory │  │
│  │ • Visual store  │  │ • LTM           │  │ (learned tasks)│  │
│  │ • Auditory store│  │                 │  │                │  │
│  └─────────────────┘  └─────────────────┘  └────────────────┘  │
│                                                                 │
│     Stimulus from ─────────────────────────────► Physical      │
│     environment                                   action        │
└─────────────────────────────────────────────────────────────────┘
```

---

### 🧩 Chunks — The Unit of Information

> A **chunk** is a piece of information the brain treats as a **single unified unit**, regardless of its internal complexity.

**Examples of chunks:**

| Chunk          | What it is      | Who sees it as one chunk |
| -------------- | --------------- | ------------------------ |
| `A`            | A single letter | Everyone                 |
| `coffee`       | A whole word    | Literate adults          |
| `0555 123 456` | A phone number  | Familiar format users    |
| 😊             | WhatsApp logo   | Regular WhatsApp users   |
| 👤             | A friend's face | Anyone who knows them    |

> 🎓 **Key insight:** The more experience in a domain, the larger the chunks. A beginner sees individual letters; an expert sees whole words and sentences at once.

---

### 🧠 Memory — Short-Term vs Long-Term

```
┌────────────────────────────────────────────────────────────────┐
│                      MEMORY TYPES                              │
│                                                                │
│  ┌──────────────────────────┐  ┌──────────────────────────┐   │
│  │   📋 SHORT-TERM (STM)    │  │   📚 LONG-TERM (LTM)     │   │
│  ├──────────────────────────┤  ├──────────────────────────┤   │
│  │ Capacity: 7 ± 2 chunks   │  │ Capacity: virtually ∞    │   │
│  │ Duration: 10–30 seconds  │  │ Duration: permanent       │   │
│  │ Volatile: easily erased  │  │ Built by repetition       │   │
│  │ by distraction           │  │ & practice over time      │   │
│  └──────────────────────────┘  └──────────────────────────┘   │
│                                                                │
│  Repetition transfers STM → LTM                               │
└────────────────────────────────────────────────────────────────┘
```

### ✅ Design Recommendations from MHP

**For STM (short-term memory):**

- Limit menu/screen items to **4–7 items max**
- Link related elements with **colors, formats, positioning**
- Use **brief and concise** messages
- Avoid presenting **unnecessary information**

**For LTM (long-term memory):**

- Encourage learning through **repetition**
- Use **metaphors** that build on what users already know
    - 🗑️ Trash can = delete · 📁 Folder = file container · 🖨️ Print icon = print

---

## ⏱️ Model 2 — Newell's Time Scale of Human Action

Proposed by Allen Newell (1990). Human actions happen at **very different time scales** — from microseconds to months. Newell organizes them into **4 bands**.

> 🎯 Think of it like a zoom lens on human behavior — some things happen in a blink, others take months.

```
┌────────────────────────────────────────────────────────────────────┐
│              NEWELL'S 4 BANDS — TIME SCALE OF ACTION               │
│                                                                    │
│  Scale        Time      System          Band                       │
│  ──────────────────────────────────────────────────────────────    │
│  10⁷  ──────  Months                  ┌──────────────────────┐    │
│  10⁶  ──────  Weeks       –           │  🌐 SOCIAL BAND      │    │
│  10⁵  ──────  Days        –           │  Habits, culture,    │    │
│                                        │  long-term behavior  │    │
│                                        └──────────────────────┘    │
│  10⁴  ──────  Hours      Task         ┌──────────────────────┐    │
│  10³  ──────  10 min     Task         │  🤔 RATIONAL BAND    │    │
│  10²  ──────  Minutes    Task         │  Planning, problem   │    │
│                                        │  solving, working    │    │
│                                        └──────────────────────┘    │
│  10¹  ──────  10 s       Unit Task    ┌──────────────────────┐    │
│  10⁰  ──────  1 s        Operations  │  💡 COGNITIVE BAND   │    │
│  10⁻¹ ──────  100 ms     Deliberate  │  Conscious thinking, │    │
│                            act        │  quick interactions   │    │
│                                        └──────────────────────┘    │
│  10⁻² ──────  10 ms      Neural        ┌──────────────────────┐    │
│  10⁻³ ──────  1 ms       Neuron        │  ⚡ BIOLOGICAL BAND  │    │
│  10⁻⁴ ──────  100 µs     Organelle     │  Automatic body      │    │
│                                        │  processes           │    │
│                                        └──────────────────────┘    │
└────────────────────────────────────────────────────────────────────┘
```

### The 4 Bands Explained

| Band             | Timeframe       | What happens                          | Examples                                                                   |
| ---------------- | --------------- | ------------------------------------- | -------------------------------------------------------------------------- |
| ⚡ **Biological** | µs → 10ms       | Automatic body processes, unconscious | Eye reacting to light, neuron firing, brain signal to finger when clicking |
| 💡 **Cognitive** | 100ms → 30s     | Conscious thinking, quick actions     | Clicking a button, reading a word, typing a password, choosing from a menu |
| 🤔 **Rational**  | Minutes → Hours | Working, planning, problem-solving    | Writing a report, searching for info, booking a trip online                |
| 🌐 **Social**    | Days → Months   | Long-term habits and social behavior  | How employees use email or collaboration tools over months                 |

> ⭐ **Most HCI research lives in the Cognitive Band** — studying how fast and accurately people interact with interfaces. But remember: **the goal of HCI is to adapt technology to humans, not the inverse!**

---

## ⌨️ Model 3 — Key-Action Model (KAM)

KAM is a descriptive model that categorizes all keyboard keys into **3 types** based on their function.

```
┌─────────────────────────────────────────────────────────────────┐
│                    KEY-ACTION MODEL (KAM)                       │
│                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌───────────────┐    │
│  │  ⌨️ SYMBOL KEYS │  │ ▶️ EXECUTIVE KEY│  │ 🔀 MODIFIER  │    │
│  ├─────────────────┤  ├─────────────────┤  ├───────────────┤    │
│  │ Type characters │  │ Perform actions │  │ Change what   │    │
│  │                 │  │                 │  │ another key   │    │
│  │ Letters: A–Z    │  │ Enter, Esc,     │  │ does          │    │
│  │ Numbers: 0–9    │  │ F1–F12,         │  │               │    │
│  │ Punctuation:    │  │ Tab, Caps Lock, │  │ Shift, Alt,   │    │  
│  │ . , ! ? …       │  │ Delete, Windows │  │ Ctrl, Fn      │    │
│  └─────────────────┘  └─────────────────┘  └───────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

### 🤔 Is KAM a good model? — Critical Analysis

**Key imbalance (left vs right hand):**

- Left side: **4 executive keys** (Tab, Caps Lock, Esc, Windows)
- Right side: **19 executive keys** (Enter, Delete, arrows, numpad...)
- → The keyboard **favors the right hand** — and with the mouse also on the right (since 1980s), the right hand may be **overloaded!**

**Key ambiguity problem:**

- Some keys produce **1 symbol** (no ambiguity) → `A` always types `A`
- Some keys produce **multiple symbols** (ambiguity) → `5` alone = `5`, but `Shift+5` = `%`
- → A **"key-ambiguity" descriptive model** might be more accurate

> 💡 **The most important question about any model:** _Is it useful?_ A good model helps us understand the **strengths, limits, and possibilities** of how users interact with a system.

> 📝 **Other descriptive models (mentioned):** Bimanual control & scrolling · Circumplex model of affect · Three-state model of graphical input

---

## 🎯 Model 4 — Norman's 7 Stages of Action (Theory of Action)

From the book **"The Design of Everyday Things"** by Donald Norman. This model describes how humans interact with the world to achieve a goal — consciously or unconsciously.

### The 7 Stages

```
┌─────────────────────────────────────────────────────────────────────┐
│              NORMAN'S 7 STAGES OF ACTION                            │
│                                                                     │
│                        ┌──────────┐                                 │
│                        │  🎯 GOAL │  ← "What I want to achieve"    │
│                        └────┬─────┘                                 │
│            ▲               │              ▲                         │
│   BRIDGE   │               │              │   BRIDGE                │
│     OF     │               │              │     OF                  │
│ EVALUATION │               │              │  EXECUTION              │
│            │               ▼              │                         │
│   ┌────────┴──────────────────────────┐   │                         │
│   │           EXECUTION               │   │                         │
│   │  ┌──────────────────────────────┐ │   │                         │
│   │  │  2. PLAN   → What to do?     │─┤   │                         │
│   │  │  3. SPECIFY → Which actions? │─┼───┘                         │
│   │  │  4. PERFORM → Do it!         │ │                             │
│   │  └──────────────────────────────┘ │                             │
│   │           ↓↓↓  WORLD  ↓↓↓         │                             │
│   │  ┌──────────────────────────────┐ │                             │
│   │  │  5. PERCEIVE → What happened?│ │                             │
│   │  │  6. INTERPRET → What does it │ │                             │
│   │  │     mean?                    │ │                             │
│   │  │  7. COMPARE → Did I succeed? │ │                             │
│   │  └──────────────────────────────┘ │                             │
│   │           EVALUATION              │                             │
│   └───────────────────────────────────┘                             │
└─────────────────────────────────────────────────────────────────────┘
```

### The 7 Stages as Questions

| #   | Stage            | Question to ask                                | Category   |
| --- | ---------------- | ---------------------------------------------- | ---------- |
| 1   | 🎯 **Goal**      | What do I want to do and why?                  | Goals      |
| 2   | 📋 **Plan**      | How can I do it? What actions are possible?    | Execution  |
| 3   | 🔍 **Specify**   | What exact actions should I take?              | Execution  |
| 4   | 👆 **Perform**   | Do the action!                                 | Execution  |
| 5   | 👁️ **Perceive** | What happened? What is the state of the world? | Evaluation |
| 6   | 🧩 **Interpret** | What does what I perceived mean?               | Evaluation |
| 7   | ✅ **Compare**    | Did the outcome match my goal?                 | Evaluation |

---

### 💻 Concrete Example — Bad UX Login

```
🎯 GOAL    → Log in to my dashboard
    ↓
📋 PLAN    → Enter my credentials
    ↓
🔍 SPECIFY → Type username and password
    ↓
👆 PERFORM → Click the Login button
    ↓
👁️ PERCEIVE → Page reloads... nothing changes
    ↓
🧩 INTERPRET → Did it work? No feedback shown at all!
    ↓
✅ COMPARE → ❌ BAD UX — goal not clearly achieved

🛠️ FIX: Show "Welcome back!" on success
         Show "Wrong password, try again" on failure
```

---

### ⚠️ Two Design Failure Points (Norman)

```
┌─────────────────────────────────────────────────────────────────┐
│              WHERE UX DESIGN FAILS                              │
│                                                                 │
│  ❌ FAILURE 1 — Execution Phase                                 │
│     "User does not know what to do"                             │
│     → The system does NOT communicate its possibilities         │
│     → Bad interface design, unclear affordances                 │
│     Example: Hidden buttons, no visible actions                 │
│                                                                 │
│  ❌ FAILURE 2 — Evaluation Phase                                │
│     "User does not understand what happened"                    │
│     → No clear feedback, absent results                         │
│     Example: Button clicked → nothing visible happens           │
│                                                                 │
│  ✅ GOOD DESIGN addresses BOTH bridges:                         │
│     → Bridge of Execution: make possibilities visible           │
│     → Bridge of Evaluation: give clear, instant feedback        │
└─────────────────────────────────────────────────────────────────┘
```

> 💬 _"When we address the steps of Norman's model from Execution to Evaluation, our product is human-centered designed."_

---

## 🧠 Chapter Summary — All 4 Models at a Glance

|Model|Author|Type|What it tells us|
|---|---|---|---|
|🤖 **Human Processor**|Card, Moran & Newell|Descriptive|Human = info processing system with 3 subsystems + memory|
|⏱️ **Time Scale**|Allen Newell (1990)|Descriptive|Human actions span 4 time bands (biological → social)|
|⌨️ **KAM**|—|Descriptive|Keyboard keys = Symbol / Executive / Modifier|
|🎯 **7 Stages of Action**|Donald Norman|Descriptive + Predictive|Human interaction = Goal → Execution (3 steps) → Evaluation (3 steps)|

---

## ⚡ Quick Recall — Exam Cheat Sheet

- **Chunk** = brain's unit of information · STM holds **7 ± 2 chunks** · lasts **10–30 seconds**
- **Newell's most HCI-relevant band** = Cognitive (ms to ~30s)
- **KAM 3 types** = Symbol · Executive · Modifier
- **Norman's 7 stages** = Goal / Plan / Specify / Perform / Perceive / Interpret / Compare
- **Norman's 2 failure points** = "Doesn't know what to do" (execution) · "Doesn't understand what happened" (evaluation)
- **Key design principle** = Both bridges (execution + evaluation) must work for good UX

---

_📁 ISD · Chapter 2 of N · Links: [[Chapter 1 — Interactive Software & Human-Computer Interaction]] | Next: [[Chapter 3 — Predictive Models Fitts' Law & KLM]]_

---
## 🔗 Navigation
- **Module:** [[NTIC L3/DLI/DLI|◀ DLI]]
- **Semester:** [[NTIC L3/NTIC L3|◀ NTIC L3]]
- **Academic Home:** [[README|🏠 Home]]
