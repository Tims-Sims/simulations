# Simulation Template — Developer Guide

> **One file. No server required.** Open `Sim_template_FixedV2.html` in a browser and it works.
> Everything a developer needs to change lives inside three clearly labelled sections of that file.

---

## Quick start — adding, editing, or removing a question

1. Open `Sim_template_FixedV2.html` in a code editor.
2. Press **Ctrl + F** and search for `DEVELOPER EDIT AREA 3`.
3. You will land on the `QUESTIONS` list. Each block between `{` and `}` is one question.
4. Edit the text inside a block to change that question, copy a block to add one, or delete a block to remove one.
5. Save the file and refresh the browser — changes appear instantly.

---

## The three developer areas

The file is a single HTML document. All editable content is grouped into three areas near the bottom of the file, inside `<script>` tags. Everything outside those areas is layout and styling — you do not need to touch it.

---

## Area 1 — Simulation configuration (`SIM_CONFIG`)

**Search for:** `DEVELOPER EDIT AREA 1`

This controls the name, branding, text, and on/off switches for the whole simulation.

```js
const SIM_CONFIG = {
    simId:       "simulation-template-shell",
    title:       "Editable Simulation Template",
    subtitle:    "Single-file shell for local student activities",
    badgeText:   "SIM",
    homeEyebrow: "Template Shell Ready",
    homeDescription: "Use this shell to build a student simulation.",
    footerText:  "Simulation Template Shell — swap the content, keep the structure.",
    ...
};
```

### Branding fields

| Field | Where it shows | What to put |
|---|---|---|
| `title` | Top bar, browser tab, home screen heading | The name of your simulation |
| `subtitle` | Top bar below the title | Short descriptor line |
| `badgeText` | Coloured square in the top-left corner | 2–4 letters, e.g. `"ELA"` or `"MTH"` |
| `homeEyebrow` | Small tag above the title on the home screen | Short category label |
| `homeDescription` | Paragraph on the home screen | Tell students what this sim is about |
| `footerText` | Tiny note at the very bottom of the page | Credit line or instructions reminder |

---

### Instructions modal

Shown when the student clicks **Help** or when the sim first loads (if `showIntroModalOnLoad` is `true`).

```js
showIntroModalOnLoad: true,
instructions: [
    "Read the question carefully before answering.",
    "Use the Hint button if you get stuck.",
    "Watch your score, streak, and progress bar as you go.",
    "Use Review Memory to revisit completed answers.",
    "Use the Reset button any time you want to restart."
],
```

- `showIntroModalOnLoad: true` — pops the instructions open the moment the page loads. Set to `false` to skip that.
- `instructions` — each string in the list becomes one bullet point. Add or remove lines freely.

---

### Rules modal

A separate pop-up the student can open from a button in the question area. Useful for classroom rules or marking reminders.

```js
showRulesModal: true,
rules: [
    "Read the full question before choosing an answer.",
    "Use the Hint if you are stuck — it will not cost points.",
    "After a wrong answer, read the feedback carefully before trying again.",
    "You can review any answered question using Review Memory."
],
```

- Set `showRulesModal: false` to hide the Rules button entirely.
- Each string in `rules` becomes one bullet point.

---

### Teach screen

An optional screen that plays **before the questions begin**. Use it to recap a concept or show key vocabulary. The student sees it after clicking Begin and before the first question.

```js
showTeachScreen: true,
teachContent: {
    eyebrow:  "📖 Quick Reminder",
    title:    "Key Concept Title",
    subtitle: "Skill focus: what students are about to practise.",
    columns: [
        {
            headingHTML:  "⭐ <strong>Concept A</strong> usually:",
            headingColor: "var(--accent)",
            items: [
                "First key point about Concept A",
                "Second key point",
                "Third key point"
            ]
        },
        {
            headingHTML:  "◇ <strong>Concept B</strong> usually:",
            headingColor: "var(--accent-2)",
            items: [
                "First key point about Concept B",
                "Second key point",
                "Third key point"
            ]
        }
    ],
    examples: [
        {
            text:       "Sample sentence illustrating Concept A.",
            labelHTML:  "⭐ Concept A example",
            labelClass: "ex-accent"
        },
        {
            text:       "Sample sentence illustrating Concept B.",
            labelHTML:  "◇ Concept B example",
            labelClass: "ex-accent2"
        }
    ]
},
```

- Set `showTeachScreen: false` to skip the teach screen completely.
- `eyebrow` — small tag at the top of the teach card.
- `title` — large heading.
- `subtitle` — sentence below the heading.
- `columns` — two side-by-side bullet lists. Each column has a `headingHTML` and an `items` array.
- `examples` — labelled example sentences shown at the bottom of the teach card.
- `headingColor` — use `"var(--accent)"` (blue) or `"var(--accent-2)"` (purple) to colour-code.
- `labelClass` — use `"ex-accent"` or `"ex-accent2"` to match the column colour.

---

### Score labels

The words shown on the feedback badge after the student answers.

```js
scoreLabels: {
    correct: "Correct",
    partial: "Partially Correct",
    wrong:   "Not Quite"
},
```

Change these to match your school's language. For example: `"Well done"`, `"Almost"`, `"Try again"`.

---

### Other switches

| Field | What it does |
|---|---|
| `allowSummaryPage: true` | Shows a results screen after the last question. Set to `false` to disable. |
| `storageKey` | The name used to save progress in the browser. Change this if you copy the file so different sims don't share saved data. Use a unique name with no spaces. |

---

## Area 2 — Language filter (`BLOCKED_LANGUAGE`)

**Search for:** `DEVELOPER EDIT AREA 2`

A list of words that are blocked from text and textarea answers. If a student types one of these words, they get a warning and cannot submit.

```js
const BLOCKED_LANGUAGE = [
    "placeholderbadword1",
    "placeholderbadword2"
];
```

Replace the placeholder strings with real words your organisation wants to block. The check ignores capital letters and accents. Leave the list empty (`[]`) to turn the filter off.

---

## Area 3 — Questions (`QUESTIONS`)

**Search for:** `DEVELOPER EDIT AREA 3`

This is the main content area. It is a list of question objects. Each object is one question. The order they appear in the list is the order the student sees them.

---

### Every field a question can have

```js
{
    id:          "q1",
    title:       "Question 1",
    prompt:      "The question text the student reads.",
    directions:  "Tell the student what to do.",
    type:        "mcq",
    choiceStyle: "buttons",
    difficulty:  "easy",
    screenLabel: "Try It (Easy)",
    placeholder: "Type here",
    hint:        "A clue shown when they click Hint.",
    points:      10,
    passage: { ... },
    choices: [ ... ],
    grading: { ... }
}
```

---

### Field-by-field reference

#### `id`
A unique internal label for this question. The sim uses it to save and load the student's answer.
- Must be different for every question.
- No spaces. Use `"q1"`, `"q2"`, `"partA"`, etc.
- Students never see this.

#### `title`
Shown as a small heading above the question on screen.
- Example: `"Question 1"`, `"Part A"`, `"Reading Check"`

#### `prompt`
The actual question or instruction the student reads. This is the main text.
- Can include basic HTML for bold text or line breaks:
  ```js
  prompt: "Read this sentence: <br><strong>The cat sat on the mat.</strong><br>What is the noun?"
  ```
- If it has no HTML, just write plain text.

#### `directions`
A smaller line below the prompt giving extra instruction.
- Example: `"Choose one answer."`, `"Enter a number only."`, `"A full sentence is best."`
- Optional — leave it out and the line is hidden.

#### `type`
Controls what kind of input the student sees. Must be one of four values:

| Value | What the student sees |
|---|---|
| `"mcq"` | A list of options they click to select (radio cards or buttons) |
| `"text"` | A single-line text box |
| `"number"` | A number-only input box |
| `"textarea"` | A large multi-line writing area |

#### `choiceStyle` *(mcq only, optional)*
Changes how the MCQ choices look.
- Leave it out (default) → choices appear as clickable card rows with radio buttons.
- Set to `"buttons"` → choices appear as compact clickable buttons side by side. Good for short answers like `["Yes", "No"]` or `["Even", "Odd"]`.

```js
type: "mcq",
choiceStyle: "buttons",
choices: ["Even", "Odd"],
```

#### `difficulty` *(optional)*
Adds a coloured badge to the question card.
- `"easy"` → green badge
- `"medium"` → yellow badge
- `"challenge"` → red badge
- Leave out to show no badge.

#### `screenLabel` *(optional)*
A small chip shown beside the difficulty badge.
- Use it to label what skill or part of the activity this is.
- Example: `"Try It (Easy)"`, `"Challenge"`, `"Part B"`
- Leave out to show nothing.

#### `placeholder` *(text, number, textarea only)*
The grey hint text shown inside an empty input box before the student types anything.
- Example: `"Type your answer here"`, `"0"`

#### `hint`
Shown when the student clicks the **Hint** button. Clicking Hint does not cost points.
- Write a clue, not the answer.
- Example: `"It starts with the letter N."`

#### `points`
How many points a fully correct answer is worth.
- Partial answers get roughly half.
- Wrong answers get zero.
- Example: `10`, `15`, `5`

---

### The passage panel *(optional)*

If a question has a `passage` field, a reading panel appears on the left side of the screen beside the question. Questions without `passage` show in full-width with no panel.

```js
passage: {
    panelTitle: "📖 Passage",
    text:       "The full text of the reading passage goes here.",
    footerText: "Read carefully before answering.",
    audioSrc:   ""
}
```

| Field | What it does |
|---|---|
| `panelTitle` | Heading at the top of the passage panel |
| `text` | The reading text shown in the panel |
| `footerText` | Small note shown below the passage text |
| `audioSrc` | Path to an audio file. If filled in, a Listen button appears. Leave as `""` to hide it. |

To add a passage to a question, paste the block above inside that question object. To remove it, delete the whole `passage: { ... }` block.

---

### The `choices` array *(mcq only)*

A list of options the student can pick from. Each item is a string.

```js
choices: [
    "Option A — the first choice",
    "Option B — the second choice",
    "Option C — the third choice"
]
```

- You can have as many choices as needed, but 3–4 is standard.
- You can include bold text using `<strong>word</strong>`.
- The index (position) of each choice is used in grading. The first item is index `0`, the second is `1`, the third is `2`, and so on.

---

### The `grading` object

This tells the sim how to mark the student's answer. The `mode` field decides which rules apply.

---

#### Mode: `"mcq"`

For multiple choice questions. Marks correct if the student picks the right option by its index number.

```js
grading: {
    mode: "mcq",
    correctAnswer: 1,
    perFeedback: [
        {
            status: "wrong",
            icon: "❌", label: "Incorrect",
            text: "This is wrong because...",
            fix: "To fix it, look for...",
            model: "Correct version: option B"
        },
        {
            status: "correct",
            icon: "✅", label: "Correct",
            text: "You got it because...",
            fix: null, model: null
        },
        {
            status: "wrong",
            icon: "❌", label: "Incorrect",
            text: "This is wrong because...",
            fix: "To fix it, look for...",
            model: "Correct version: option B"
        }
    ]
}
```

| Field | What it does |
|---|---|
| `correctAnswer` | The index of the correct choice. `0` = first option, `1` = second, `2` = third. |
| `perFeedback` | One feedback block per choice. Shown when the student picks that choice. |
| `perFeedback[].status` | `"correct"` or `"wrong"` — controls the colour of the feedback box. |
| `perFeedback[].icon` | Emoji shown in the feedback label. |
| `perFeedback[].label` | Short word in the feedback label. |
| `perFeedback[].text` | The explanation shown to the student. |
| `perFeedback[].fix` | Optional sentence telling them how to correct their thinking. Set to `null` to hide. |
| `perFeedback[].model` | Optional model answer line. Set to `null` to hide. |

**Simpler alternative** — if you do not need per-choice feedback, use `explanations` instead:

```js
grading: {
    mode: "mcq",
    correctAnswer: 1,
    explanations: [
        "Wrong because option A...",
        "Correct because option B...",
        "Wrong because option C..."
    ]
}
```

One explanation per choice, shown after the student submits.

---

#### Mode: `"exactText"`

For short text answers. Marks correct if the student's answer matches one of the acceptable answers. Case and accents are ignored.

```js
grading: {
    mode: "exactText",
    acceptableAnswers: ["noun", "a noun"],
    explanation: "A noun names a person, place, animal, thing, or idea."
}
```

| Field | What it does |
|---|---|
| `acceptableAnswers` | List of answers that count as correct. Add multiple if there are valid alternatives. |
| `explanation` | Shown after the student submits, whatever they answered. |

---

#### Mode: `"exactNumber"`

For number answers. Marks correct if the number is within the allowed range.

```js
grading: {
    mode: "exactNumber",
    correctAnswer: 4,
    tolerance: 0,
    explanation: "24 divided by 6 equals 4."
}
```

| Field | What it does |
|---|---|
| `correctAnswer` | The correct number. |
| `tolerance` | How far off the student can be and still be marked correct. `0` means exact match only. `0.5` would accept `3.5` to `4.5`. |
| `explanation` | Shown after the student submits. |

---

#### Mode: `"containsKeywords"`

For long written responses. Counts how many key words appear in the student's answer and grades based on that.

```js
grading: {
    mode: "containsKeywords",
    keywords: ["respect", "help", "safe", "kind", "teamwork", "learn"],
    minimumForCorrect: 2,
    minimumForPartial: 1,
    explanation: "Kindness helps classrooms feel safe, respectful, and ready for learning."
}
```

| Field | What it does |
|---|---|
| `keywords` | Words to look for in the answer. |
| `minimumForCorrect` | How many keywords must appear for a full correct mark. |
| `minimumForPartial` | How many keywords must appear for a partial mark. Anything below this = wrong. |
| `explanation` | Shown after the student submits. |

---

#### Mode: `"custom"`

For any grading logic that the other modes cannot handle. You write a function that receives the student's answer and the question, and returns a result object.

```js
grading: {
    mode: "custom",
    grader(answer, question) {
        if (answer.toLowerCase() === "odd") {
            return { status: "correct", scoreAwarded: question.points, explanation: "9 is odd." };
        }
        return { status: "wrong", scoreAwarded: 0, explanation: "9 is not even." };
    }
}
```

The function must return an object with three fields:
- `status` — `"correct"`, `"partial"`, or `"wrong"`
- `scoreAwarded` — number of points to give
- `explanation` — text shown to the student

---

## How to add a question

1. Find `DEVELOPER EDIT AREA 3` in the file.
2. Go to the end of the last question object — just before the closing `]`.
3. Add a comma after the last `}`, then paste a new question block.
4. Fill in your content. Make sure `id` is unique.

```js
    },        ← end of previous question (add comma here)
    {
        id: "q6",
        title: "Question 6",
        prompt: "Your question here.",
        directions: "Your instruction here.",
        type: "text",
        hint: "Your hint here.",
        points: 10,
        grading: {
            mode: "exactText",
            acceptableAnswers: ["answer"],
            explanation: "Your explanation here."
        }
    }
];            ← end of the list
```

---

## How to remove a question

Delete everything from the opening `{` to the matching `}` for that question, including the comma before or after it. Make sure the last question in the list does not have a trailing comma.

---

## How to reorder questions

Cut the full question block (from `{` to `}` plus its comma) and paste it in the new position. The order in the list is the order the student sees.

---

## Tips

- `id` must be unique. Two questions with the same `id` will overwrite each other in the save system.
- You can use `<br>` for a line break and `<strong>word</strong>` for bold in `prompt` and `choices` text.
- Leaving out optional fields (`passage`, `difficulty`, `screenLabel`, `directions`) hides those elements — you do not need to delete anything extra.
- The sim saves progress in the browser automatically. If you want students to start fresh, they can use the **Reset** button, or you can change `storageKey` in Area 1 to a new unique name.
- This file runs completely offline. No internet connection is needed.
