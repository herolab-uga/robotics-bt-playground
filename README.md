# BT Playground Pro 🤖

An interactive, web-based **Behavior Tree playground** for programming and simulating mobile robots — no installation required. Built as a single self-contained HTML file, deployable to GitHub Pages in minutes.

![BT Playground Pro](https://img.shields.io/badge/status-live-4ade80?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-a78bfa?style=flat-square) ![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-ready-22d3ee?style=flat-square)

## Live Demo

> [https://herolab-uga.github.io/robotics-bt-playground/](https://herolab-uga.github.io/robotics-bt-playground/)

---

## Features

### Visual BT Editor
- Drag-and-drop node palette onto a snap-to-grid canvas
- Click-drag port connectors to wire parent → child relationships
- Select any node to edit label, parameters, and robot assignment

### Node Library (35+ nodes)

| Category | Nodes |
|---|---|
| **Composite** | Sequence, Selector, Parallel, Random Selector |
| **Decorator** | Inverter, Repeat N, Retry, Timeout, Cooldown, Memory Sequence, Memory Selector, Force Success |
| **Condition** | Battery OK?, Obstacle Ahead?, At Goal?, Package Found?, Area Clear?, Ally Near?, Msg Received?, Zone Occupied? |
| **Action** | Move To, Charge, Avoid, Pick Up, Drop Off, Scan, Broadcast, Send Msg, Request Help, Guard Zone, Wait, Set Blackboard |

### Simulation
- Real-time animated robot in a 2D environment
- Per-robot blackboard, battery drain, and status display
- Execution log with tick-by-tick node results
- Adjustable tick speed + single-step mode

### Interactive Environment Editor
- 🧱 **Wall** — click-drag to place rectangular obstacles
- 📍 **Waypoint** — click to add named navigation targets
- 📦 **Package** — click to place pickup objects
- ✕ **Erase** — remove any placed element
- ↺ **Reset** — restore default environment

### Multi-Robot & Communications
- Add up to 6 robots, each with independent blackboard and BT execution
- Assign nodes to specific robots via the Properties panel
- `Broadcast` (all), `Send Msg` (point-to-point), `Request Help` (nearest ally)
- Live Comms log tab

### Import / Export
- ⬇ Export full tree + environment as JSON
- ⬆ Import from clipboard or `.json` file

### Challenge Scenarios
1. **Patrol & Recharge** — waypoint patrol with cooldown-gated charging
2. **Package Delivery** — scan → retry pick-up → timeout-capped navigation
3. **Swarm Coordination** — R1 scans & broadcasts; R2 responds and delivers
4. **Search & Rescue** — Memory Sequence with inter-robot help requests

---



## Project Structure

```
bt-playground/
├── index.html   ← entire application (self-contained)
└── README.md    ← this file
```

---

## License

MIT — free to use, modify, and redistribute.
