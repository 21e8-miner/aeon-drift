# AEON DRIFT — Volumetric Canyon Runner

AEON DRIFT is a high-performance, single-file WebGL2 canyon runner game featuring a volumetric rendering pipeline, procedural Web Audio synthesizers, roguelite upgrades, and full **[webcade.fun/arcade](https://webcade.fun/arcade)** cabinet integration.

Live Shareable URL: **[https://21e8-miner.github.io/aeon-drift/](https://21e8-miner.github.io/aeon-drift/)**

---

## Key Features

- **WebGL2 Volumetric Rendering**:
  - Volumetric clouds with raymarched atmospheric scattering and dynamic storm lightning.
  - GGX/Smith PBR shading with sedimentary canyon terrain, detail normals, wet rock sheen, and luminous mineral veins.
  - Screen-Space Reflections (SSR) and dynamic river surface wave physics with ship water wake.
  - Temporal Anti-Aliasing (TAA) with YCoCg variance clipping and Catmull-Rom history.
  - Motion Blur with ship masking, multi-mip GGX Bloom, Anamorphic Flares, God Rays, SSAO, ACES Filmic Tonemapping, and Contrast-Adaptive Sharpening (CAS).

- **Cockpit FPV & Visual Effects**:
  - 3D Holographic Cockpit HUD (pitch ladder, artificial horizon line, velocity vector circle, lock-on diamond, target range readout).
  - Dynamic Deflector Energy Shield hex mesh on impact/graze.
  - Mach Cone vapor condensation shockwave cone when boosting.
  - Exhaust plumes with mach diamonds and heat shimmer.

- **Deep Roguelite Gameplay**:
  - High-speed canyon flight physics with banking, pitch, roll, and ground effect hover cushion.
  - Multi-target Homing Missile System with target acquisition.
  - EMP Shock Pulse to purge minefields and hazards into flux.
  - 24 Roguelite Upgrades (*Chronos Core*, *Plasma Lance*, *Tether Magnet*, *Resonance Shield*, *Second Wind*, *Nova Prow*, etc.).
  - Overdrive Fever Mode at high combo multipliers.

- **Synthesized Web Audio**:
  - Procedural jet engine acoustic stack (Lighthill low-frequency roar, turbulent mixing, Mach-wave hiss, acoustic crackle spikes, fan whine).
  - Multi-track step sequencer synthwave music that dynamically layers and ramps as combo intensity climbs.

- **Webcade Arcade Cabinet Ready**:
  - Native `postMessage` protocol for parent iframe integration (`aeon:start`, `aeon:stageClear`, `aeon:gameOver`, `webcade_score`).
  - Deterministic run seeds via `?seed=...` or `?daily=1`.
  - PWA support with Web App Manifest and offline capability.

---

## Controls

### Keyboard & Mouse
- **Mouse** or **W/A/S/D** / **Arrows**: Steer
- **Shift** / **Space**: Burn (spend flux for speed)
- **Q / E** (or Double Tap A/D): Snap roll left/right
- **Ctrl** / **Z / X**: Air brake
- **F**: EMP Shock pulse (costs 22 flux)
- **G**: Fire homing missile (locks forward targets)
- **C**: Cycle camera modes (Chase, Far Chase, Cockpit FPV)
- **I**: Invert Y axis
- **T**: Toggle daily run mode
- **M**: Mute/Unmute audio
- **P**: Toggle performance stats
- **R**: Restart run
- **Esc**: Pause / Resume

### Touch & Mobile
- **Drag**: Virtual relative-drag joystick
- **Swipe / Flick**: Snap roll
- **▲ Burn Button**: Spend flux for speed
- **▼ Button**: Air brake
- **◎ Button**: Shock pulse
- **➤ Button**: Fire homing missile
- **II / ⌖**: Pause / Camera cycle

---

## Webcade Integration API

To embed AEON DRIFT inside webcade.fun or any arcade cabinet iframe:

```javascript
// Listen to game events
window.addEventListener("message", (e) => {
  if (e.data && e.data.aeon) {
    console.log("Arcade Event:", e.data.aeon, e.data);
  }
});

// Control commands
iframe.contentWindow.postMessage("pause", "*");
iframe.contentWindow.postMessage("resume", "*");
iframe.contentWindow.postMessage("restart", "*");
```

---

## License

MIT License. Open-source and free for Webcade arcade embedding.
