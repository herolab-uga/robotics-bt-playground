# BT Playground Pro 🤖

An interactive, web-based **Behavior Tree playground** for programming and simulating mobile robots — no installation required. Built as a single self-contained HTML file, deployed in GitHub Pages.

![BT Playground Pro](https://img.shields.io/badge/status-live-4ade80?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-a78bfa?style=flat-square) ![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-ready-22d3ee?style=flat-square)

## Live Demo

> Check here: `https://herolab-uga.github.io/bt-playground/`

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

## Deploying to GitHub Pages

### Option A — GitHub Web UI (no git required)

1. Create a new repository at [github.com/new](https://github.com/new)  
   - Name it `bt-playground` (or anything you like)  
   - Set visibility to **Public**  
   - Check **Add a README file**  
   - Click **Create repository**

2. In your new repo, click **Add file → Upload files**

3. Drag `index.html` into the upload area, then click **Commit changes**

4. Go to **Settings → Pages**  
   - Under *Source*, select **Deploy from a branch**  
   - Branch: `main`, folder: `/ (root)`  
   - Click **Save**

5. Wait ~60 seconds, then visit:  
   `https://<your-username>.github.io/bt-playground/`

---

### Option B — Git CLI

```bash
# 1. Clone your empty repo (create it on GitHub first)
git clone https://github.com/<your-username>/bt-playground.git
cd bt-playground

# 2. Copy index.html into the folder
cp /path/to/index.html .

# 3. Commit and push
git add index.html README.md
git commit -m "Initial deploy: BT Playground Pro"
git push origin main

# 4. Enable GitHub Pages in Settings → Pages → main branch / root
```

---

### Option C — GitHub CLI (`gh`)

```bash
gh repo create bt-playground --public --source=. --remote=origin --push
# Then enable Pages in Settings → Pages
```

---

## Customising

The playground is a **single self-contained HTML file** (`index.html`). All CSS and JS are inlined — no build step, no dependencies, no CDN calls beyond Google Fonts.

To add a new node type:
1. Add an entry to the `NDEF` object in the `<script>` block  
2. Add a `.pnode` entry in the palette `<div id="palette">`  
3. Add a `case` in `tickCondition()` or `tickAction()` as appropriate

To change the default environment, edit the `ENV` object near the top of the script.

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
