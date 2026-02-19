# Murmuration

> *Each bird knows only three rules — yet together they paint the sky.*

An interactive real-time 3D starling murmuration simulation built with Three.js and MediaPipe. 800 autonomous agents follow emergent flocking behavior, and you can disturb the flock using your cursor or webcam hand tracking.

![Murmuration Preview](https://img.shields.io/badge/Three.js-r160-black?style=flat-square&logo=threedotjs) ![MediaPipe](https://img.shields.io/badge/MediaPipe-0.10.3-blue?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

---

## ✨ Features

- **800 Boids** running Craig Reynolds' classic flocking algorithm in real-time 3D
- **Cursor / Trackpad interaction** — move your cursor to act as a predator and repel the flock
- **Webcam Hand Tracking** via MediaPipe — raise your hand to scatter the birds
- **Generative Audio** — ambient drone and wing flutter noise that evolve with flock density and speed
- **Live Telemetry Panel** — cohesion, average speed, neighbor count updated in real-time
- **Cinematic rendering** — ACES Filmic tone mapping, exponential fog, 4000-star background
- **Custom animated cursor** with lagging ring follow effect
- **Single HTML file** — zero build step, zero dependencies to install

---

## 🧠 How It Works

The simulation is built on **three simple rules** per bird, applied every frame:

| Rule | Description |
|------|-------------|
| **Separation** | Steer away from nearby neighbors to avoid crowding |
| **Alignment** | Match velocity with nearby neighbors |
| **Cohesion** | Steer toward the average position of nearby neighbors |

From just these three local rules, complex global murmuration behavior **emerges naturally** — no central controller, no leader bird. This is a classic example of emergent behavior in complex systems, first described by Craig Reynolds in his 1987 paper *"Flocks, Herds, and Schools: A Distributed Behavioral Model."*

**Your hand/cursor acts as a predator** — birds within a ~28-unit radius detect the threat and flee, cascading a ripple-scatter through the flock just like a hawk diving into a real murmuration.

---

## 🚀 Getting Started

### Option 1 — Open directly in browser
Just double-click `murmuration_final.html`. No server needed for basic usage.

### Option 2 — Live Server (recommended for webcam)
Webcam access requires a secure context (`localhost` or `https`). Use VS Code Live Server or any local HTTP server:

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .
```

Then open `http://localhost:8080/murmuration_final.html`

### Option 3 — Deploy to Netlify (instant public URL)
Drag and drop the HTML file at [netlify.com/drop](https://netlify.com/drop) — live in 30 seconds.

---

## 🎮 Controls

| Input | Action |
|-------|--------|
| **Move cursor / trackpad** | Repel the flock (predator mode) |
| **Webcam hand** | Raise palm to scatter nearby birds |
| **Allow camera permission** | Enables MediaPipe hand tracking |
| **Turn up volume** | Hear the evolving ambient soundscape |

---

## 🛠 Tech Stack

| Technology | Purpose |
|------------|---------|
| [Three.js r160](https://threejs.org) | 3D rendering, instanced mesh, fog, lighting |
| [MediaPipe Tasks Vision](https://developers.google.com/mediapipe) | Real-time hand landmark detection |
| [Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) | Display typography |
| [Space Mono](https://fonts.google.com/specimen/Space+Mono) | UI / monospace elements |
| Web Audio API | Generative ambient audio |

---

## 📁 Project Structure

```
murmuration/
├── murmuration_final.html   # Entire simulation — single self-contained file
└── README.md
```

---

## ⚙️ Configuration

All tuneable parameters are at the top of the `<script>` block:

```js
const NUM_BOIDS = 800;          // Number of birds (lower for slower devices)
const PERCEPTION_RADIUS = 4.0;  // How far each bird can "see"
const MAX_SPEED = 0.3;          // Maximum bird velocity
```

Repulsion tuning (inside the boid loop):
```js
if (hDistSq < 800) {            // Predator influence radius (~28 units)
    const f = 1.5 / (hDist + 0.1); // Inverse falloff strength
```

---

## 🌐 Browser Compatibility

| Browser | Status |
|---------|--------|
| Chrome 90+ | ✅ Full support |
| Edge 90+ | ✅ Full support |
| Firefox | ⚠️ Works, MediaPipe GPU delegate may fall back to CPU |
| Safari | ⚠️ Works, webcam requires explicit permission prompt |

> **Note:** MediaPipe hand tracking requires a secure context (`https://` or `localhost`). Cursor/trackpad interaction works without webcam.

---

## 📖 Background Reading

- [Craig Reynolds — Boids (1987)](https://www.red3d.com/cwr/boids/)
- [Three.js InstancedMesh docs](https://threejs.org/docs/#api/en/objects/InstancedMesh)
- [MediaPipe Hand Landmarker](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker)
- [The Science of Murmurations — Royal Society](https://royalsocietypublishing.org/doi/10.1098/rsif.2020.0794)

---

## 📄 License

MIT — free to use, modify, and share.

---

*Built with Three.js · MediaPipe · Web Audio API*
