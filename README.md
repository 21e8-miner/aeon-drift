# AEON DRIFT — Volumetric Canyon Runner

AEON DRIFT is a high-performance, single-file WebGL2 canyon runner game featuring a volumetric rendering pipeline, custom procedural audio synthesizers, and multi-platform input support.

Live Demo: [https://21e8-miner.github.io/aeon-drift/](https://21e8-miner.github.io/aeon-drift/)

## Features

- **WebGL2 HDR Renderer**: Volumetric clouds, GGX/Smith PBR shading, screen-space reflections, god rays, bloom, motion blur, SSAO, and TAA with Contrast-Adaptive Sharpening.
- **Adaptive Resolution**: Automatically scales internal rendering scale to keep framerates locked on mobile and desktop.
- **Procedural Sound**: Step sequencer soundtrack and sound effects synthesized entirely in the browser using the Web Audio API.
- **Responsive Controls**: Fully supports Keyboard, Mouse, Touch (virtual joystick & swipe rolls), Tilt steering, and standard Gamepads.
- **Arcade/Cabinet Wrapper Ready**:
  - Out-of-the-box support for iframe communication via `postMessage`.
  - Deterministic run seeds via query parameter (`?seed=...`) or `window.AEON_SEED`.

## Controls

### Keyboard & Mouse
- **Mouse** or **W/A/S/D** / **Arrows**: Steer
- **Shift** / **Space**: Burn (spend flux for speed)
- **Q / E**: Snap roll left/right
- **Ctrl** / **Z / X**: Air brake
- **F**: Shock pulse (clears mines, costs 22 flux)
- **C**: Cycle camera modes (Chase, Far Chase, Cockpit)
- **I**: Invert Y axis
- **T**: Toggle daily run mode
- **M**: Mute/Unmute audio
- **P**: Toggle performance metrics
- **R**: Restart run
- **Esc**: Pause / Resume

### Touch Devices
- **Drag**: Steer (virtual relative-drag stick recenters dynamically)
- **Tap Left/Right Thirds** (or flick sideways): Snap roll
- **▲ Burn Button**: Spend flux for speed
- **▼ Button**: Air brake
- **◎ Button**: Shock pulse
- **II Button**: Pause / Resume
- **⌖ Button**: Cycle camera

### Gamepads
- **Left Stick**: Steer
- **Right Trigger**: Burn
- **Left Trigger**: Air brake
- **Left/Right Shoulders (L1/R1)**: Snap roll left/right
- **X / A**: Pause / Resume
- **Y**: Cycle camera
- **B (Button 2)**: Shock pulse

## Host/Wrapper Integration API

You can embed AEON DRIFT in any arcade layout or iframe. The game exposes the following integration hooks:

### Event Listeners (Parent Window)
The game communicates lifecycle events using `window.parent.postMessage`. Listen to these events in your parent page:
```javascript
window.addEventListener("message", (e) => {
  if (e.data && e.data.aeon) {
    const { aeon, seed, ...details } = e.data;
    if (aeon === "start") {
      console.log("Game started with seed:", seed);
    } else if (aeon === "stageClear") {
      console.log("Zone cleared:", details.stage, "Score:", details.score);
    } else if (aeon === "gameOver") {
      console.log("Run finished. Final Score:", details.score, "Zone:", details.stage, "Distance:", details.km);
    }
  }
});
```

### Control Commands (Iframe Control)
You can send postMessage controls into the iframe to control game state:
```javascript
// Pause the game
iframe.contentWindow.postMessage("pause", "*");

// Resume the game
iframe.contentWindow.postMessage("resume", "*");

// Restart the game
iframe.contentWindow.postMessage("restart", "*");

// Mute / Unmute
iframe.contentWindow.postMessage("mute", "*");
iframe.contentWindow.postMessage("unmute", "*");
```

### Deterministic Seed Injection
To force a specific level layout for competitive tournaments or duels:
- Define `window.AEON_SEED = "YOUR_HEX_OR_NUMBER"` in the iframe before load, or
- Append `?seed=YOUR_HEX_OR_NUMBER` to the URL.
