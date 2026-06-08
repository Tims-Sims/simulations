# Simulation Template — Question Guide

This file explains how to add, edit, or replace questions in the simulation. You only need to touch **one section** of the HTML file.

---

## Where to edit

Open `Sim_template_FixedV2.html` and find this comment:

```
DEVELOPER EDIT AREA 3: QUESTION DATA
```

Below it is a list called `QUESTIONS`. Each item in the list is one question. Add, remove, or edit items here.

---

## Question skeleton — every question needs these fields

```js
{
    id: "q1",
    title: "Question 1",
    prompt: "Your question text goes here.",
    directions: "Tell the student what to do.",
    type: "mcq",
    hint: "A clue to help if they are stuck.",
    explanation: "The explanation shown after they answer.",
    points: 10,
    grading: { ... }
}
```

| Field | What it does |
|---|---|
| `id` | A unique label for this question. No spaces. (`"q1"`, `"q2"`, etc.) |
| `title` | Short heading shown above the question. (`"Question 1"`, `"Part A"`) |
| `prompt` | The actual question or instruction the student reads. |
| `directions` | Extra instruction line below the prompt. (`"Choose one answer."`) |
| `type` | What kind of input the student sees. See types below. |
| `hint` | Shown when the student clicks the Hint button. |
| `explanation` | Shown after the student submits their answer. |
| `points` | How many points a correct answer is worth. |
| `grading` | Rules for how the answer is marked. See grading modes below. |

---

## Question types

Set `type` to one of these values:

### `"mcq"` — Multiple choice (radio buttons)

Student picks one option from a list.

```js
{
    id: "q1",
    title: "Question 1",
    prompt: "Which sentence uses a noun correctly?",
    directions: "Choose one answer.",
    type: "mcq",
    hint: "A noun is a person, place, or thing.",
    explanation: "Option B is correct because 'dog' is a noun.",
    points: 10,
    choices: [
        "The dog runned fast.",
        "The dog ran fast.",
        "Fast ran the dog did."
    ],
    grading: {
        mode: "mcq",
        correctAnswer: 1,
        explanations: [
            "Incorrect. 'Runned' is not a real word.",
            "Correct. 'Dog' is a noun and the sentence is properly formed.",
            "Incorrect. The word order does not make sense."
        ]
    }
}
```

**Extra fields for MCQ:**

| Field | What it does |
|---|---|
| `choices` | Array of answer options. Each one is a string. |
| `grading.correctAnswer` | The index of the correct choice. Counting starts at 0. So first option = `0`, second = `1`, third = `2`. |
| `grading.explanations` | One explanation per choice. Shown after the student picks that option. Must have the same number of items as `choices`. |

---

### `"text"` — Short text answer

Student types a single word or short phrase.

```js
{
    id: "q2",
    title: "Question 2",
    prompt: "What is a word that names a person, place, or thing?",
    directions: "Type one word.",
    type: "text",
    placeholder: "Type your answer here",
    hint: "It starts with the letter N.",
    explanation: "The answer is 'noun'.",
    points: 10,
    grading: {
        mode: "exactText",
        acceptableAnswers: ["noun"]
    }
}
```

**Extra fields:**

| Field | What it does |
|---|---|
| `placeholder` | Grey hint text shown inside the empty input box. |
| `grading.acceptableAnswers` | List of answers that count as correct. Case does not matter. Add multiple if there are valid alternatives: `["noun", "a noun"]` |

---

### `"number"` — Number answer

Student types a number only.

```js
{
    id: "q3",
    title: "Question 3",
    prompt: "What is 24 ÷ 6?",
    directions: "Enter a number only.",
    type: "number",
    placeholder: "0",
    hint: "How many groups of 6 fit into 24?",
    explanation: "24 divided by 6 equals 4.",
    points: 10,
    grading: {
        mode: "exactNumber",
        correctAnswer: 4,
        tolerance: 0
    }
}
```

**Extra fields:**

| Field | What it does |
|---|---|
| `grading.correctAnswer` | The correct number. |
| `grading.tolerance` | How far off the student can be and still be marked correct. Set to `0` for exact answers. Set to `0.5` to accept answers within half a unit. |

---

### `"textarea"` — Long written response

Student types a full sentence or paragraph.

```js
{
    id: "q4",
    title: "Question 4",
    prompt: "Write one sentence explaining why kindness matters in a classroom.",
    directions: "A full sentence is best.",
    type: "textarea",
    placeholder: "Write your sentence here",
    hint: "Think about respect, teamwork, or safety.",
    explanation: "Kindness helps classrooms feel safe and ready for learning.",
    points: 15,
    grading: {
        mode: "containsKeywords",
        keywords: ["respect", "help", "safe", "kind", "teamwork", "learn"],
        minimumForCorrect: 2,
        minimumForPartial: 1
    }
}
```

**Extra fields:**

| Field | What it does |
|---|---|
| `grading.keywords` | Words to look for in the student's answer. |
| `grading.minimumForCorrect` | How many keywords must appear for a full correct mark. |
| `grading.minimumForPartial` | How many keywords must appear for a partial mark. Anything below this is marked wrong. |

---

## Grading modes summary

| Mode | Use with | How it works |
|---|---|---|
| `"mcq"` | `type: "mcq"` | Checks if the selected index matches `correctAnswer` |
| `"exactText"` | `type: "text"` | Checks if the typed answer matches any item in `acceptableAnswers` (ignores capital letters) |
| `"exactNumber"` | `type: "number"` | Checks if the number matches `correctAnswer` within `tolerance` |
| `"containsKeywords"` | `type: "textarea"` | Counts how many `keywords` appear in the answer |
| `"custom"` | Any | You write your own grading function (for advanced use) |

---

## How to add a new question

1. Open `Sim_template_FixedV2.html`
2. Find `DEVELOPER EDIT AREA 3`
3. Copy one of the existing question objects
4. Paste it at the end of the list, before the closing `]`
5. Add a comma after the previous question's closing `}`
6. Change the `id` to something new (`"q6"`, `"q7"`, etc.)
7. Fill in your content
8. Save and refresh the browser

---

## How to remove a question

Delete the entire object for that question (everything from `{` to the matching `}`), including the comma before or after it. Make sure you do not leave a trailing comma on the last item in the list.

---

## How to change the points value

Each question has a `points` field. Change the number. Full correct answers award all the points. Partial answers award roughly half. Wrong answers award zero.

---

## Tips

- `id` values must be unique. If two questions share the same `id`, one will overwrite the other in the save system.
- You can use basic HTML in `prompt` and `choices` text (bold, line breaks). Example: `"Read this: <br><strong>The cat sat.</strong>"`
- The order questions appear in the list is the order students see them.
- You can have as many or as few questions as you want.
