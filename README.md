# 🕯️ The Cursed Chamber

A browser-based WebXR escape room built with A-Frame and Cannon-ES physics. You wake up locked inside a cursed ritual chamber inside an Egyptian pyramid. Solve three puzzle-gated relic discoveries, complete the ritual, enter the passcode — then walk out into the desert night.

**Runs in any WebXR-capable browser. No installation. Works on desktop and Meta Quest.**

---

## 🎮 How to Play

**Desktop**
- `WASD` — move
- `Mouse` — look around (click to lock pointer)
- `Left Click` — grab / interact
- `Right Click + Drag` — rotate a held object
- `Esc` — release pointer lock

**Meta Quest (VR)**
- Thumbstick — move
- Trigger — grab / interact
- Grip — rotate held object
- Open the URL in the Quest browser and tap the **VR** button (bottom right)

---

## 🧩 The Puzzle

The relics are not just sitting out. Each one is locked behind a mini-puzzle:

| Relic | Where | How to unlock |
|-------|-------|----------------|
| 💀 Skull | Iron chest | Find the **rusty key** on the bookshelf |
| 🔮 Amulet | Behind the wardrobe | Solve the **rune-lock** — match wardrobe runes to the clue on the mirror |
| 📖 Tome | Desk drawer | Pull the **glowing book** on the bookshelf (hidden lever) |

Once you have all three, place them into the correct slots on the ritual table. The **socket glows green** when you're holding the right relic. Wrong placement flings it back at you.

After the ritual — enter the passcode, walk through the second door, and escape into the Egyptian desert.

---

## 🚀 Running Locally

You need a static file server. The simplest options:

**Option 1 — VS Code Live Server**
1. Install the [Live Server extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
2. Open the project folder in VS Code
3. Click **Go Live** in the bottom status bar
4. Navigate to `http://localhost:5500/index.html`

**Option 2 — npx**
```bash
npx serve .
```
Then open `http://localhost:3000/index.html`

**Option 3 — Python**
```bash
# Python 3
python -m http.server 8000
```
Then open `http://localhost:8000/index.html`

> ⚠️ Opening `index.html` directly as a `file://` URL will **not** work — A-Frame and ES modules require a server.

---

## 📁 What's in This Repo

```
cursed-chamber/
│
├── index.html              ← Entry point. Open this in your browser.
│
├── src/
│   ├── main.js             ← Scene init, A-Frame component registration
│   ├── puzzle.js           ← Ritual state machine (all game logic lives here)
│   ├── interactions.js     ← Grab, inspect, place, drawer pull, rune-lock
│   ├── horror.js           ← Lighting phases, mirror distortion, escalation
│   └── audio.js            ← Positional audio manager (Resonance Audio)
│
├── assets/
│   ├── models/             ← All GLTF models (Blender exports)
│   │   ├── ritual_table.glb
│   │   ├── demon_lock.glb
│   │   ├── mirror_frame.glb
│   │   ├── skull_relic.glb
│   │   ├── amulet_relic.glb
│   │   ├── tome_relic.glb
│   │   ├── iron_chest.glb
│   │   ├── wardrobe.glb
│   │   ├── bookshelf.glb
│   │   └── ...
│   │
│   ├── textures/           ← PBR texture maps (albedo, normal, roughness)
│   │
│   └── audio/              ← Ambient loops, impact sounds, horror cues
│
└── README.md
```

---

## 🔧 Tech Stack

| Library | Version | Role |
|---------|---------|------|
| [A-Frame](https://aframe.io) | 1.4 | WebXR scene graph, component system |
| [Cannon-ES](https://github.com/pmndrs/cannon-es) | 0.20 | Physics — rigid bodies, constraints, impulses |
| [Three.js](https://threejs.org) | r146 | Underlying WebGL renderer (via A-Frame) |
| [A-Frame Resonance Audio](https://github.com/resonance-audio/resonance-audio-web-sdk) | — | 3D positional audio in VR |
| Blender 3.6 | — | All custom 3D assets (GLTF 2.0 export) |

No build step. No bundler. Pure ES modules — it just runs.

---

## ✨ Features

- **Puzzle-gated relic discovery** — key lock, rune-lock puzzle, hidden book lever
- **6 VR interaction types** — grab+inspect, snap placement, constrained drawer pulls, gaze examine, event triggers, physics door
- **Ritual state machine** — 6 states, event-driven architecture, escalating horror system
- **Cannon-ES physics** — rigid body props, spring-return drawers, impulse-based jumpscare ejections
- **Horror escalation** — 5 phases: ambient → flickering → hostile → penalty → ritual complete
- **Socket glow feedback** — green for correct relic, red warning for wrong
- **Egyptian desert ending** — walk outside, see the pyramid reveal, 15-second outdoor sequence
- **Desktop + Meta Quest** — full feature parity on both platforms

---

## 🐛 Known Issues

- Physics runs at 30Hz on Meta Quest (browser CPU limitation) — fast interactions can feel slightly delayed vs desktop
- Mirror distortion shader is disabled on mobile WebXR (performance) — replaced with a static baked texture
- No session persistence — closing the tab resets all progress

---

## 🛠️ Debug / Dev Shortcuts

Open `src/puzzle.js` and set at the top:

```js
const DEBUG_MODE = true;
```

This enables:
- **`Ctrl+Shift+G`** — skip directly to ritual completion (passcode auto-fills, door opens)
- Console logging of all state transitions

> Remember to set `DEBUG_MODE = false` before submitting or recording.

---

## 👥 Team

| Name | NetID | Role |
|------|-------|------|
| Niyam Momaya | nkm66 | State machine, physics, horror system, Blender assets (ritual table, relics ×3) |
| Aryan Nagwekar | an1262 | VR interactions, A-Frame scene, WebXR input, Blender assets (demon lock, mirror frame, desert environment) |

**ECE 576 — Virtual Reality · Rutgers University · Spring 2025**

---

## 📄 License

Assets and code are original work created for ECE 576. Audio sourced from [Freesound.org](https://freesound.org) under CC0 license. A-Frame, Cannon-ES, and Three.js are open-source under MIT / Apache 2.0.
