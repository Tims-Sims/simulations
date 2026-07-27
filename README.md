# Green Computing: Energy Saver Challenge

An interactive, game-based simulation for ICT / Digital Literacy students (Forms 1–3). The student plays the last person leaving the school's ICT lab and must find and power down every energy-wasting device before the bell rings.

**File:** `POC/IT/green-computing-sim.html` — a single self-contained HTML file (HTML + CSS + JS + SVG). No installs, no server, no internet needed. Just open it in any modern browser (double-click the file).

## How to Play

1. Click **Enter the Lab** on the home screen.
2. A timer **counts up** to show how long you take — no time limit.
3. Find all **19 energy wasters** in the side-view lab scene. Wasteful equipment glows when you hover over it.
4. When you're done, click **Leave Room** to get your rating.

### Interactions

| Device | Action to turn OFF | Points |
|---|---|---|
| PC towers (×6) | **Press and hold** the power button until the ring fills (safe shutdown) | +10 each |
| Monitors (×6) | Click the screen | +5 each |
| Phone chargers (×3) | **Drag** the charger down out of the power strip | +8 each |
| Printer | Click | +10 |
| Projector | Click | +10 |
| Air conditioner | Click | +15 |
| Lights (bonus) | Click the wall switch — the whole room goes dark | +5 |

- **Turning things back on:** tap any switched-off device (including a PC's power button or an unplugged charger) to power it back up. The points come off your score until you switch it off again.
- **Decoy — the network router (on the wall shelf) must STAY ON.** Clicking it costs **−10 points** and explains why (it runs the school's network overnight).
- Every correct action shows a short **energy fact** in the feedback panel (phantom power drain, standby waste, etc.).

## Scoring & Ratings

Raw points are scaled to a score out of 100. The end screen shows the score, items fixed/missed, time used, and a rating:

| Score | Rating |
|---|---|
| 90–100 | 🏆 Energy Champion |
| 70–89 | ✅ Green Guardian |
| 50–69 | ⚠️ Room Still Wasting Power |
| Below 50 | ❌ Energy Offender |

The end screen also lists everything still wasting energy (with the energy fact) and everything done well, plus a **Play Again** button.

## Features

- **Timer:** counts up from 0:00 so students can see how long they took (shown on the end screen).
- **Live HUD:** score chip, fixed-items counter, and an "Energy Saved" progress bar.
- **Theme toggle:** dark / light mode. **Fullscreen** button. **Reset** with confirmation.
- **Help modal** with full instructions, shown from the topbar at any time.
- **Keyboard accessible:** Tab to any device, Enter/Space to toggle it.
- Works with mouse and touch (pointer events).

## Learning Objectives

- Identify energy-wasting behaviours in a digital/ICT environment.
- Understand the impact of small actions (shutdown, sleep, unplugging) on energy consumption — including phantom/vampire power drain.
- Recognise that some equipment (network infrastructure) must stay on — think before switching.

## Tweaking the Game

Constants at the top of the `<script>` in the HTML file:

- `HOLD_TIME` — ms to hold a PC power button (default `1000`)
- `DRAG_DIST` — how far a charger must be dragged to unplug (default `46`)
- `ITEM_INFO` — points and tooltip text per device type
- `DECOY_PENALTY` — points lost for touching the router (default `10`)
