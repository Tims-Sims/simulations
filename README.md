# Simulation Template — Developer Guide

> **One file. No server required.** Choose a template and open it in a browser—it works instantly.

## Repository Layout

- **blank-template.html** — An empty chrome shell with dark/light theme switching, start screen, help modal, fullscreen, and reset confirmation. Build your own simulation logic inside.
- **premade-template.html** — A complete question engine with built-in support for 7 question types, grading, scoring, progress tracking, hints, reviews, and input safety features.
- **OLD TEMPLATE/** — Legacy reference folder. `Challenge_Level_Sim_template.html` has been archived here for reference only.

---

## blank-template.html — Quick Start

**blank-template.html** is a stripped-down, minimal starting point for building simulations from scratch. Unlike premade-template.html (which includes a full question engine with built-in scaffolding, grading, and scoring), blank-template.html provides only the essential chrome: dark/light theme switching with persistence, a start screen, a help/instructions modal, fullscreen capability, and a styled reset confirmation modal. The simulation area itself is empty—you add all content here.

Use blank-template.html when you want complete control over what your simulation does. There are no built-in questions, grading systems, audio, history tracking, or student profiles. You decide the behavior and structure.

### How to use blank-template.html

1. Copy `blank-template.html` and rename it to match your simulation name.
2. Open the file in your code editor.
3. Search for the text `DEV-EDIT` — you will find exactly six marked zones. These are the only places you should change:

| Zone | What to change |
|---|---|
| **1. DEV-EDIT: PAGE TITLE** | Browser tab title |
| **2. DEV-EDIT: SIM CONFIG** | `simId` (must be unique, prefixes localStorage keys), `title`, `subtitle`, `instructions` |
| **3. DEV-EDIT: SIM STYLES** | Empty CSS section at the end of `<style>` for your simulation styling |
| **4. DEV-EDIT: SIM AREA** | Empty `#simContainer`—build your simulation markup here |
| **5. DEV-EDIT: FOOTER** | Footer text shown at the very bottom |
| **6. DEV-EDIT: SIM LOGIC** | `devInit()` runs on Start click; `devReset()` runs on confirmed Reset (clear sim state here); add your simulation functions below the banner |

Sections marked `CHROME — DO NOT EDIT` (chrome CSS and chrome JavaScript) must not be modified. Everything else is the chrome UI that supports your simulation.

### What's already built in

- **Theme switching** — dark/light mode toggle persisted to localStorage.
- **Start screen** — a welcome screen before the simulation begins.
- **Help modal** — instructions shown when the student clicks Help; the help button's pulse animation stops permanently after the first click.
- **Reset modal** — styled confirmation dialog when clearing the simulation.
- **Fullscreen button** — one-click fullscreen mode.
- **Safe storage** — `storageGet()` and `storageSet()` wrapper functions for browser localStorage (safe in sandboxed iframes).
- **Auto-scroll** — screen changes automatically scroll to the top.
- **Safe HTML rendering** — `escapeHtml()` helper function available for rendering user input without XSS risk.

### What you build

You write all simulation content inside `devInit()` (runs when Start is clicked) and `devReset()` (clears state when Reset is confirmed), and inside the `#simContainer` HTML. This might be a game, an interactive diagram, a data exploration tool, a physics simulation, or anything else. The template imposes no structure—it is yours to define.

---

## premade-template.html — Quick Start

**premade-template.html** is a complete, ready-to-use simulation engine. It provides the same dark/light theme switching and chrome features as blank-template.html, but adds a full question and grading system out of the box. Use this when you want to build a multi-question activity with automatic scoring, progress tracking, hints, and reviews—without writing the engine yourself.

### Question Types

The premade template supports 7 question types via the `QUESTIONS` array:

| Type | What the student sees |
|---|---|
| **multipleChoice** | Multiple choice with radio cards or buttons |
| **exactText** | Short text answer with case-insensitive matching |
| **exactNumber** | Number answer with optional tolerance range |
| **keywords** | Long text response scored by keyword count |
| **shortAnswer** | Textarea for multi-line written responses |
| **dragSort** | Drag-and-drop sorting into bins, with drag-back to tray and per-question Reset button |
| **matching** | Click left item then right item to pair them |

### How to use premade-template.html

1. Copy `premade-template.html` and rename it to match your simulation name.
2. Open the file in a code editor.
3. Search for the text `DEV-EDIT` — you will find exactly six marked zones:

| Zone | What to change |
|---|---|
| **1. DEV-EDIT: PAGE TITLE** | Browser tab title |
| **2. DEV-EDIT: SIM CONFIG** | `simId` (must be unique, prefixes localStorage keys), `title`, `subtitle`, `instructions` |
| **3. DEV-EDIT: QUESTIONS** | Full question schema with demo for each of the 7 types; documented in banner |
| **4. DEV-EDIT: INPUT LIMITS & FILTER** | Character limits per question and globally; profanity filter configuration |
| **5. DEV-EDIT: SIM STYLES** | CSS for question styling and layout customization |
| **6. DEV-EDIT: FOOTER** | Footer text shown at the very bottom |

Sections marked `CHROME — DO NOT EDIT` (chrome CSS and chrome JavaScript) must not be modified.

### Built-in Behavior

**Start & Navigation**
- Fresh open always shows the help screen.
- After the student closes Help, the questions begin.
- Submit swaps to the Next Question button after an answer is accepted.
- No Previous button; use step dots to revisit already-answered questions.
- Spam-click safe—only one submission allowed per question.

**State Management**
- Progress is saved automatically to localStorage (keyed by `simId`).
- Close mid-sim and reopen the same file → restores position.
- Finish all questions, then reopen → shows a fresh start and wipes the old session.
- Theme choice persists across sessions.

**Hints & Feedback**
- Hints are shown once clicked and remain visible, marked as "used".
- Hints are persisted—reopening shows used hints already revealed.
- Reviews/feedback render as vertical bullet lists.

### Input Safety

- **Per-question and global character limits** — live counter shown to user.
- **Profanity filter** — embedded word list, leetspeak normalized, substring matching for long words and word-boundary matching for short words. Extendable `PROFANITY_ALLOWLIST` for legit words that should not be blocked.
- **Input validation** — wrong or blocked input shows a red border and brief shake animation.
- **No native dialogs** — all messages use styled modals.
- **No type=password** — password masking is available via documented `.masked-input` CSS class.
- **XSS-safe** — all user text is escaped before rendering.

