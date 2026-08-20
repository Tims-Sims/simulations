# AGENTS.md

## Project Overview
This is the **Tims-Sims** organisation repository containing educational simulations (sims) for UK secondary school students. All sims are single-file HTML with no external dependencies, no server required.

## Repository
- **GitHub Org:** Tims-Sims
- **Repo:** Tims-Sims/simulations
- **Clone location:** `C:\Users\Moe\Tims-Sims-simulations`
- **GitHub account:** EliAlpha799 (authenticated via `gh` CLI)

## Branch Workflow
- **NEVER commit or push to `main`.**
- Each issue has its own branch named after the issue content (e.g., `SCI-BIO-F2-T1-U1-SEC3-SIM3.1B1`).
- Before starting work: check `git branch --show-current` and confirm it matches the issue branch.
- Commit messages MUST start with `#<issue-number>` (e.g., `#166 Add walkthrough and assessment`).
- After pushing, change the issue label to "review needed".

## Development Workflow (MANDATORY ORDER)
1. Read the README dev guide at the repo root for template usage and sim requirements.
2. Read the GitHub issue description for specific requirements and the QA checklist.
3. Use `blank-template.html` for custom mechanic sims or `premade-template.html` for standard question types.
4. Template version: **2.2.1**. There are 6 `DEV-EDIT` zones in the template.
5. After initial build, ask user what can be improved, then implement all enhancements.
6. Run QA checklist before committing.
7. Commit and push to the issue branch.

## Enhancement Pattern
After building the base sim, the user expects these enhancements to be added before commit:
- **Guided walkthrough** — 6-step banner with progress dots, Skip/Next buttons, sessionStorage persistence.
- **Multiple assessment questions** — 3 sequential questions with progress dots, hints, retry, feedback, Next Question/See Results.
- **Auto-animate button** — Play/pause to cycle the simulation automatically.
- **Side-by-side comparison** — Where applicable, static reference states flanking the live interactive state.
- **Context caption** — Explains WHY changes happen (biological/physical context).
- **Completion stats** — Mastery %, time on task, attempts, first-attempt tracking, stored in sessionStorage.

## Universal Sim Requirements
- No audio, no typing interactions, no timers, no lives.
- British spelling throughout.
- 44x44px minimum touch targets.
- Keyboard accessible.
- Non-colour status cues (icons, patterns, labels alongside colour).
- Correct feedback: state what went wrong, why, how to fix, and show model answer.
- First-attempt accuracy tracking.
- Retry allowed on incorrect answers.
- Single-file, no external dependencies.

## Reporting (Section 9 of template)
Save to sessionStorage: completion, first-attempt accuracy, final mastery, attempts, hints used, time on task, missed focus skill.

## Technical Notes
- PowerShell does NOT support `&&`. Use `; if ($?) { ... }` for chained commands.
- Example: `git add . ; if ($?) { git commit -m "#123 message" }`
- Example: `git commit -m "#123 msg" ; if ($?) { git push origin branch-name }`

## Available Issues
- #161 — SCI-BIO-F2-T1-U1-SEC3-SIM3.1B1 "The Pressure Pump" (COMPLETE, pushed)
- #166 — SCI-BIO-F2-T1-U1-SEC3-SIM3.2B2 "Gas Composition Comparison Slider" (COMPLETE, pushed)
- #168 — SCI-BIO-F2-T1-U1-SEC3-SIM3.3A2 "Oxygen Demand Animation" (COMPLETE, pushed)
- #91 — ELA-F2-T1-U7-SEC1-SIM1 "Backdrop Breakout" (COMPLETE, pushed)
- #99 — ELA-F2-T1-U15-SEC1-SIM1 "Topic Target" (COMPLETE, pushed)
- #175 — SS-HIST vocabulary sorter (not started)
