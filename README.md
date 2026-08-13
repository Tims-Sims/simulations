# MATH-F1-T1-PREWORK-SIM2 — Maxi-Taxi Change Master

An interactive maths simulation for Form 1 students (Trinidad and Tobago). It is the second of four "Getting Back Into Maths" warm-up sims used before Topic 1.1.1 (Whole Numbers) begins.

**Skill practised:** subtraction of large whole numbers in columns, with exchanging (borrowing) between place-value columns — including chained exchanges across zeros.

## The file

| | |
|---|---|
| Simulation | [`MATH/Form1/Term1/PreWork/MATH-F1-T1-PREWORK-SIM2.html`](MATH/Form1/Term1/PreWork/MATH-F1-T1-PREWORK-SIM2.html) |
| Built from | Simulation template v2.2.1 (blank template) |
| Runs | Fully offline, single HTML file, no other assets |
| Curriculum link | Form 1, Strand 1, Topic 1.1.1 — outcomes 1.1.1.3 (place value) and 1.1.1.8 (problem solving) |
| Audience | Form 1 students, 11–12 years old |
| Session length | About 5–10 minutes |

## How to run it

Download the HTML file and double-click it. It opens in any modern browser (Chrome, Edge, Firefox) with no server and no internet connection.

## How the game works

The player is a maxi-taxi conductor on the Priority Bus Route working out change and balancing the cash float at the end of each run.

1. **Read the route story** — each run is a subtraction written in a place-value frame, already lined up.
2. **Work each column from the Ones.** If the top digit is too small, **tap the column that can give a ten** — the digit is struck out and drops by one, and the column to its right gains ten, written exactly as it would be in a copybook. When a column holds a zero, the exchange must be walked column by column: the student taps every hop themselves; a zero column refuses with a hint to go one more column left.
3. **Type the answer digit** for each ready column on the keyboard or the on-screen keypad.
4. On the last run, **check by adding back**: the answer plus the amount subtracted must rebuild the original number before it is accepted.

There are 5 fixed runs across 4 levels (3-digit change up to a 5-digit float with chained exchanges across several zeros). Correct answers bank the amount left in the float; a clean run (no hints or wrong tries) earns a $50 tip. Escalating hints help after wrong tries — the answer digit is only revealed on the third miss, with a reason. Confetti falls behind the game card on every correct answer, and the finished frame stays on screen so the student sees the completed subtraction before the round summary appears. Finishing all five runs earns the end-of-day banner and an animated review of every run with mistakes made.

Features: Mr Roger the conductor coach with speech bubbles, offline synthesised sound (mutable, volume slider in Help), dark/light theme, fullscreen, calculator-style keypad, keyboard and touch input, idle nudge highlighting the next action, a route progress bar that fills one stop per completed run, progress restored on reload, all learner data cleared when the tab closes.

## The marking key

The 5 questions and answers are fixed (from the SIM plan, Section 6) and must not be changed:

| Level | Subtraction | Answer |
|---|---|---|
| 1 | $452 − $218 | $234 |
| 1 | 806 − 259 | 547 |
| 2 | $4 223 − $1 878 | $2 345 |
| 3 | $5 003 − $1 675 | $3 328 |
| 4 | $50 000 − $27 645 | $22 355 |

## Testing

This branch is in the **testing** phase — see `TESTER_INSTRUCTIONS.md` for the tester brief and the QA checklist to follow. Report bugs as issues with steps to reproduce, expected result, and actual output. Do not modify the simulation while testing.
