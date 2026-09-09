# Simulation Template — Developer Guide

**Template version: 2.2.1**

> **One file. No server required.** Choose a template and open it in a browser—it works instantly.

## Repository Layout

- **blank-template.html** — An empty chrome shell with dark/light theme switching, start screen, help modal, fullscreen, and reset confirmation. Build your own simulation logic inside.
- **premade-template.html** — A complete question engine with built-in support for 11 question types, grading, scoring, progress tracking, hints, reviews, images, an offline sound engine, a config validator, and input safety features.
- **OLD TEMPLATE/** — Legacy reference folder. `Challenge_Level_Sim_template.html` has been archived here for reference only.

---

## blank-template.html — Quick Start

**blank-template.html** is a stripped-down, minimal starting point for building simulations from scratch. Unlike premade-template.html (which includes a full question engine with built-in scaffolding, grading, and scoring), blank-template.html provides only the essential chrome: dark/light theme switching with persistence, a start screen, a help/instructions modal, fullscreen capability, and a styled reset confirmation modal. The simulation area itself is empty—you add all content here.

Use blank-template.html when you want complete control over what your simulation does. There are no built-in questions, grading systems, history tracking, or student profiles (an optional, removable sound engine is included — see the Sound engine section below). You decide the behavior and structure.

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

The premade template supports 11 question types via the `QUESTIONS` array. See the "Question types" section below for the full list and config fields.

### How to use premade-template.html

1. Copy `premade-template.html` and rename it to match your simulation name.
2. Open the file in a code editor.
3. Search for the text `DEV-EDIT` — you will find exactly six marked zones:

| Zone | What to change |
|---|---|
| **1. DEV-EDIT: PAGE TITLE** | Browser tab title |
| **2. DEV-EDIT: SIM CONFIG** | `simId` (must be unique, prefixes localStorage keys), `title`, `subtitle`, `instructions` |
| **3. DEV-EDIT: QUESTIONS** | Full question schema with demo for each of the 11 types; documented in banner |
| **4. DEV-EDIT: INPUT LIMITS & FILTER** | Character limits per question and globally; profanity filter configuration |
| **5. DEV-EDIT: SIM STYLES** | CSS for question styling and layout customization |
| **6. DEV-EDIT: FOOTER** | Footer text shown at the very bottom |

Sections marked `CHROME — DO NOT EDIT` (chrome CSS and chrome JavaScript) must not be modified.

### Built-in Behavior

**Start & Navigation**
- Fresh open always shows the help screen.
- After the student closes Help, the questions begin.
- Submit swaps to the Next Question button after an answer is accepted.
- No Previous button; use step dots to revisit already-answered questions (TEST_MODE allows free navigation to any question — see "Config validator & test mode" below).
- Spam-click safe—only one submission allowed per question, unless `attemptsPerQuestion` allows a retry (see "Premade template settings").

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

---

## Premade template settings

These live in `SIM_CONFIG` inside the `DEV-EDIT: SIM CONFIG` zone.

- **templateVersion** — identifies which template base a sim was built from. Don't change it.
- **TEST_MODE** — builder testing mode: shows answers, allows free navigation between questions, and doesn't save progress. **Always set this back to `false` before giving the file to students.** Note that this is a convenience flag, not real security — any HTML file can always be opened and read by a tech-savvy student, so nothing client-side (including question answers) is ever truly secret.
- **shuffleQuestions** — `true` puts the questions in a random order each run.
- **shuffleChoices** — `true` shuffles multiple-choice answer choices each run. This only affects the `multipleChoice` type; `trueFalse` always shows True then False, and `ordering` shuffles its items on its own regardless of this setting.
- **attemptsPerQuestion** — `1`, `2`, `3`, or `"unlimited"`. When a wrong or partial answer is submitted and attempts remain, a Try Again button appears that re-enables the inputs so the student can retry the same question.
- **useQuestionBank** / **bankDrawCount** — two ways to build a question set. Leave `useQuestionBank: false` to use the `QUESTIONS` array in order as written. Set it `true` to instead ignore `QUESTIONS` and randomly draw `bankDrawCount` questions from a larger `QUESTION_BANK` pool each run.

## Question types

Every question also supports an optional `hint` and an optional `image` (see "Images in questions" below).

| Type | What the student does | Key config fields |
|---|---|---|
| **multipleChoice** | Picks one of several choices | `choices`, `correctIndex`, optional `perChoiceFeedback` |
| **exactText** | Types a short text answer | `answer`, optional `caseSensitive` |
| **exactNumber** | Types a number | `answer`, optional `tolerance` |
| **keywords** | Writes a longer response scored by keyword hits | `keywords`, `minMatches` |
| **shortAnswer** | Writes a free-form multi-line response in a textarea | optional `keywords` + `minMatches`, or `ungraded: true` for manual/reflection answers |
| **dragSort** (a.k.a. sorting) | Drags items into bins (or clicks item then bin, or uses the keyboard) | `items` (`id`, `label`, `icon`, `correctBin`), `bins` (`id`, `label`, `icon`, `description`) |
| **matching** | Clicks a left card, then its matching right card | `pairs` (array of `{ left, right }`) |
| **trueFalse** | Picks True or False | `correctAnswer`, optional `feedbackCorrect`/`feedbackWrong` |
| **fillBlank** | Fills inline blanks within a sentence — typed, typed with a word bank shown, or drag-the-word-into-the-blank | `text` (with `{tokens}`), `blanks` (per-token `accept` list, optional `caseSensitive`), optional `wordBank` (`"none"`/`"list"`/`"drag"`), optional `extraWords` decoys |
| **ordering** | Reorders a shuffled list into the correct sequence by grabbing and dragging blocks (keyboard: arrow keys on a focused block) | `items` (`id`, `label`), `correctOrder` (array of item ids) |
| **imageHotspot** | Clicks the correct region(s) of a picture | `image`, `imageAlt`, `hotspots` (`id`, `label`, `x`, `y`, `w`, `h`, `correct`), optional `multiSelect` |

## Images in questions

Any question can carry a picture: add `image` and `imageAlt` (required — this is what screen readers read out).

There are three ways to fill `image`:

1. **Embedded base64 (recommended)** — keeps the picture baked into the single offline HTML file with nothing else to ship.

   PowerShell:
   ```powershell
   [Convert]::ToBase64String([IO.File]::ReadAllBytes("picture.png")) | Set-Clipboard
   ```
   Then paste the result into the question:
   ```js
   image: "data:image/png;base64,PASTE"
   ```
   macOS/Linux:
   ```bash
   base64 -w0 picture.png
   ```

2. **Inline SVG** — a string starting with `<svg`. Great for diagrams and keeps file size tiny. Only paste SVG you trust (your own drawings or ones you generated), since it's injected as-is.

3. **Relative file path** — e.g. `pictures/diagram.png`, if you're shipping image files alongside the HTML instead of a single-file sim.

Base64 encoding makes a file roughly 1.37x its original size, so keep images small — this is best for diagrams and icons, not large photos.

## Config validator & test mode

On load, the template checks every question's configuration. If something is missing or malformed, students never see a broken sim — instead a friendly error screen lists exactly what needs fixing, with which question and which field.

Recommended workflow when building a sim:

1. Set `TEST_MODE: true`.
2. Open the file and step through every question — answers and free navigation are visible so you can check each one quickly.
3. Set `TEST_MODE: false`.
4. Share the file with students.

## Accessibility

- Fully keyboard-playable: Tab and Enter/Space work throughout, including drag-and-drop questions (Enter to pick up, arrow keys to target a bin or the tray, Enter to drop) and ordering questions (ArrowUp/ArrowDown on a focused block moves it); drag-mode fill-in-the-blank also works by clicking or pressing Enter on a word chip, then on a blank.
- Feedback and status changes are announced to screen readers via a live region.
- `imageAlt` is required on any question with an image, so screen reader users get a description of the picture.

## Sound engine (audio in the templates)

### What it is

Both templates ship with a built-in, fully offline audio engine: a speaker icon in the header toggles all sound on/off (persisted to localStorage), a set of default sounds are synthesized in-browser with no audio files required, and the Help modal shows a per-category volume slider for whatever sound categories your simulation uses.

### Using it

Call `playSound("name")` from your simulation logic (inside `devInit()`, `devReset()`, or any function you add in the DEV-EDIT: SIM LOGIC zone). The built-in sound names are:

- `click` — general button/option clicks
- `correct` — learner answers correctly
- `wrong` — learner answers incorrectly
- `typing` — per-keystroke or per-character reveal
- `complete` — simulation/activity finishes

You can add your own sound names to `SOUND_FILES` (e.g. `levelUp: ""`) and call `playSound("levelUp")` anywhere.

Every sound belongs to a category in `SOUND_CATEGORIES`. All built-in sounds are in the `effects` category, which always gets a volume slider in the Help window. Give a sound you add a different category name (for example `voice` for narration) and it automatically gets its own labelled slider — if nothing uses a category, no slider appears for it. Optional friendlier slider labels live in `CATEGORY_LABELS`.

### Adding your own MP3/WAV fully inside the HTML

Encode the audio file to base64 text, then paste it into `SOUND_FILES` as a data URI—this keeps the sound baked into the single HTML file with nothing else to ship.

PowerShell:
```powershell
[Convert]::ToBase64String([IO.File]::ReadAllBytes("mysound.mp3")) | Set-Clipboard
```

macOS/Linux:
```bash
base64 -w0 mysound.mp3
```

Then in `SOUND_FILES`:
```js
mysound: "data:audio/mp3;base64,PASTE_HERE"
```

And add it to its own category in `SOUND_CATEGORIES` so it gets a dedicated slider:
```js
mysound: "voice"
```
A "Voice / narration" slider then appears automatically in Help.

Base64 encoding makes the file roughly 1.37x its original size, so this is best for short sound effects, not music or long narration. If you have several files or longer clips, ship them next to the HTML instead and reference a relative path, e.g. `"sounds/mysound.mp3"`—but then remember to ship that file alongside the HTML.

### Removing audio

Delete the `#audioBtn` button in the header (search "OPTIONAL: AUDIO TOGGLE BUTTON") and the entire `DEV-EDIT: AUDIO (OPTIONAL)` script section (the file's audio comment banner notes exactly where this section starts and ends). Everything else in the chrome checks for the audio elements being absent and stays safe if you remove them.

---

## Changelog

- **2.2.1** — Offline sound engine with mute and per-category volume sliders; config validator with a friendly error screen; TEST_MODE; question shuffling and choice shuffling; attempts-per-question with Try Again; optional question bank with random draw; 4 new question types (true/false, fill-in-the-blank, ordering, image hotspot); images on any question (base64, inline SVG, or file); keyboard-only accessibility and screen-reader announcements.
- **2.x (previous)** — Rebuilt blank and premade templates.
- **1.x** — Original template set.

