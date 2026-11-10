# 🤖 BT Playground Pro

> An interactive, browser-based Behavior Tree editor and multi-robot simulator for robotics education and research.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![HTML5](https://img.shields.io/badge/Built%20with-HTML5%2FJS-orange.svg)]()
[![No dependencies](https://img.shields.io/badge/Dependencies-none-brightgreen.svg)]()
[![HeRo Lab](https://img.shields.io/badge/HeRo%20Lab-UGA-990000.svg)](https://herolab.uga.edu)

---

## Overview

**BT Playground Pro** is a fully self-contained, single-file web application for designing, visualising, and simulating Behavior Trees (BTs) on mobile robots. It requires no installation, no build step, and no server — open `index.html` in any modern browser and start building.

Developed at the **[HeRo Lab](https://herolab.uga.edu)** at the University of Georgia in collaboration with Claude Assistant, BT Playground Pro makes BT concepts tangible through live simulation and is designed for use in graduate AI and robotics courses, research prototyping, and self-guided learning.

---

## ✨ Feature Highlights

| Area | Features |
|---|---|
| **BT Editor** | Drag-and-drop canvas · zoom/pan · 70+ node types · structural validation · copy/paste subtrees · left-to-right priority indicators |
| **Multi-Robot BTs** | Each robot can run its own independent BT tab simultaneously |
| **Simulation** | Up to 6 robots · animated with wheels, lights, FOV cone · interactive environment editor |
| **Environment** | Rect/circle walls · dynamic bouncing obstacles · waypoints · charging stations · packages (static/dynamic) · collection zones · light sources · victims · floor dirt |
| **Navigation** | VFH obstacle-avoidance nav · direct-line move · wander (random walk) · patrol · explore frontier · dock |
| **Coordination** | Per-robot blackboards · global params · ROS-style topics · 3-mode message passing · conflict-aware zone assignment |
| **Sensing** | Customisable range & FoV per sensor node · TOF (4-direction) · light sensor with noise · victim detection · dirt detection |
| **Blackboard** | Local (per-robot) and global variables · manual add/edit/delete in BB pane · Set/Get/Check BB with explicit scope param |
| **Utility BTs** | Per-node utility scores · cumulative score propagation · Utility Selector/Sequence · Utility Change action |
| **Analytics** | Replay scrubber · per-tick explainability · coverage metrics · custom expressions · battery analytics |
| **Search** | Global search across palette, BT nodes, BT tabs, sim objects, blackboard, sensors, log, comms |
| **Import/Export** | BT JSON · Sim config JSON · Execution log JSON (replay-capable) |
| **Test Harness** | Scripted test runner with `sim` and `bt` APIs and 9 built-in tests |

---

## Getting Started

Access the deployed pages at [BT-Playground-PRO](https://herolab-uga.github.io/robotics-bt-playground/)
No build step. No installation. No server. Directly Works in your browser: Chrome, Firefox, Edge, and Safari. 
Note - Make sure to export the data after your interaction. The site does not store/save any data between sessions/reloads.

### Quick Start

1. Open the Playground web link. (https://herolab-uga.github.io/robotics-bt-playground/)
2. Load a built-in challenge from the **Scenes** tab (try *Patrol & Recharge* first)
3. Press **▶ Run** — the robot executes the pre-built BT immediately
4. Watch the **BB** (Blackboard) and **Explain** panels for live state
5. Pause, edit a node's P1 value, resume — changes take effect on the next tick
6. Use **⏮ Replay** to scrub backwards through execution history

---

## Layout of the Playground

```
┌─ Topbar: Speed · Robots · Scene · 🔍 Search · Select · Export · Run ───────┐
│                                                                              │
│  ┌── Palette ──┬──── BT Editor (tabs) ──────┬──── Simulator ────┐          │
│  │  🔀 Logic   │  [Root]──[Selector]         │  🤖 🤖 🤖         │          │
│  │  🔎 Conds   │      ├──[Sequence]──...     │  Waypoints/Walls  │          │
│  │  ⚡ Actions  │      └──[Navigate To]       │  Packages/Victims │          │
│  │  🗄 BB       │                             │                   │          │
│  └─────────────┴────────────────────────────┴───────────────────┘          │
│                                                                              │
│  ┌─ Log ─┬─ Blackboard ─┬─ Comms ─┬─ Explain ─┬─ Sensor ─┬─ Metrics ─┐   │
└──┴───────┴──────────────┴─────────┴───────────┴──────────┴───────────┴───┘
```

---

## Node Categories

### 🔀 Logic — Flow Control
Composites (`Sequence`, `Selector`, `Parallel`, `Mem.Sequence`, `Mem.Selector`, `Utility Selector`, `Utility Sequence`), Decorators (`Inverter`, `Repeat N`, `Retry`, `Timeout`, `Cooldown`, `Force Success`, `Set Utility`), and the `Root` entry point.

### 🔎 Conditions — Sensors & State
Boolean literals (`TRUE`, `FALSE`, `Number Literal`), robot state (`Battery OK?`, `At Goal?`, `My ID is?`), environment sensing (`Obstacle?`, `Package Near?`, `Waypoint Near?`, `Path Clear?`, `TOF Sensor?`, `Light Level?`, `Dirt Nearby?`, `Victim Near?`), communication (`Ally Near?`, `Msg Received?`), and blackboard checks (`Check BB`, `BB Expression`).

### ⚡ Actions — Robot Behaviors
Navigation (`Navigate To`, `Move To (direct)`, `Patrol Route`, `Explore Frontier`, `Wander`, `Collision Avoid`, `Dock`), movement primitives (`Move Fwd/Bwd`, `Move By N`, `Turn Left/Right/Back`, `Rotate By°`), manipulation (`Scan`, `Pick Up`, `Drop Off`, `Rescue Victim`, `Vacuum`), system (`Wait`, `Charge`, `Light Up`), communication (`Send Message`, `Publish Topic`, `Read Topic`).

### 🗄 Blackboard — Variables & Goals
Read/write (`Set BB`, `Increment BB`), literals (`Set True/False/Number/String`), utility (`Utility Change`), custom (`Custom Process`, `Function`).

---

## Multi-Robot Behavior Trees

Each robot can be assigned its own BT tab. When challenges like **Swarm** or **Search & Rescue** are loaded, separate BT tabs are created automatically — one per robot. All robots tick simultaneously every tick cycle regardless of which tab is currently displayed.

```
BT Tab: "Scout (R1)"    →  Robot 1 runs this BT independently
BT Tab: "Mapper (R2)"   →  Robot 2 runs this BT independently  
BT Tab: "Guard (R3)"    →  Robot 3 runs this BT independently
```

Robots communicate via broadcast messages, shared global BB variables, and ROS-style topics.

---

## Built-in Challenges

| Challenge | Robots | Key Concepts |
|---|---|---|
| Patrol & Recharge | 1 | Selector priority, Memory Sequence, battery guard |
| Package Delivery | 1 | Pick-up/drop-off, obstacle avoidance, MemSequence |
| Swarm Coordination | 3 | Per-robot BTs, zone conflict resolution via messaging |
| Search & Rescue | 2 | Scout/Medic roles, victim detection, broadcast |
| Utility Demo | 1 | Utility Selector, dynamic score computation |
| Foraging | 3 | `pkg:nearest` targeting, collection zones |

---

## Check BB — Back-chaining Pattern

The `Check BB` node enables the standard BT back-chaining (goal-check-first) pattern:

```
Selector
├── Check BB: "victims_found >= 3"    ← goal already met? → SUCCESS, done
└── Sequence                           ← goal not met? → achieve it
    ├── Navigate To: pkg:nearest
    ├── Pick Up
    └── Drop Off
```

Compound expressions supported: `"victims_found >= 1 AND battery > 20 OR carrying == true"`

---

## Blackboard Scoping

All `Set BB`, `Get BB`, `Check BB` nodes accept a **P3 = Scope** parameter:
- `local` (default) — robot's own blackboard, not shared
- `global` — `GLOBAL_PARAMS` shared across all robots
- Prefix key with `/` to force global regardless of scope param

---

## Navigation

`Navigate To` uses **VFH (Vector Field Histogram)** obstacle avoidance:
- Scans N directions (default 36) with configurable look-ahead
- Scores each by clearance minus goal-deviation penalty
- Hysteresis bonus prevents oscillation between equal-score paths
- Wall-following escape when stuck > 5 ticks

Tune per-node via **Config Params**: `kH` (heading gain), `look` (px), `avoid` (weight), `N` (directions), `arrivalDist` (px).

`Move To (direct)` goes straight-line with no obstacle consideration — use when the path is known clear.

---

## Sensor Customisation

All sensor condition nodes accept:
- **P1 = range** (px, 0 = use robot's global sensor range)
- **P2 = FoV** (degrees, 0 = 360° omnidirectional)

Example: `Obstacle? P1=40 P2=90` detects obstacles only in a 90° front cone within 40px.

---

## Search (Ctrl+F)

The global search panel finds:
- **Palette nodes** — all 70+ available node types by name, type, or description; click to add to canvas
- **Canvas nodes** — placed nodes on the active BT
- **BT library nodes** — nodes in all other BT tabs
- **Simulation objects** — waypoints, packages, victims, walls, charging stations
- **Blackboard** — local and global variable values
- **Sensors** — live battery, light, obstacle readings per robot
- **Log** — text search through execution log
- **Comms** — inbox messages

---

## Import / Export

| Format | Contents |
|---|---|
| `bt_tree.json` | BT nodes, edges, library tabs, robot assignments |
| `bt_sim_config.json` | Environment (walls, waypoints, packages, victims, dirt, etc.) |
| `bt_log.json` | Full execution log + snapshots (enables replay on import) |

---

## Test Harness

Click **🧪 Test** in the topbar to open the scripted test runner:

```js
// Example script
bt.loadChallenge('patrol');
await sim.runTicks(20);
const r = sim.robot(0);
assert(r.battery > 0, 'battery drained correctly');
assert(Math.hypot(r.x-80, r.y-70) < 15, 'reached waypoint A');
log(r);
```

APIs: `sim.placeRobot(idx,x,y)`, `sim.robot(idx)`, `sim.addWaypoint(id,x,y)`, `sim.runTicks(n)`, `bt.loadChallenge(key)`, `bt.step()`, `bt.rootStatus()`, `assert(cond, msg)`.

---

## Citation

If you use BT Playground Pro in your research or teaching, please cite:

```bibtex
@software{btplaygroundpro2025,
  title   = {{BT Playground Pro}: An Interactive Behavior Tree Editor and Multi-Robot Simulator},
  author  = {{HeRoLab, University of Georgia}},
  year    = {2025},
  url     = {https://github.com/HeRoLab/bt-playground},
  note    = {Single-file HTML/JS application, no build step required}
}
```

___
## Heterogeneous Robotics (HeRoLab)

Heterogeneous Robotics Research Lab (HeRoLab) of the University of Georgia.

Please contact hero at uga . edu for any queries

https://hero.uga.edu/

<p align="center">
<img src="https://herolab.org/wp-content/uploads/2021/04/herolab_newlogo_whitebg.png" width="300">
</p>

---

## License

MIT © HeRoLab, University of Georgia. See [LICENSE](LICENSE) for details.
