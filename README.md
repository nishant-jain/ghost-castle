# Ghost Castle

An animated Halloween scene built entirely with SVG, CSS animations, and the Web Audio API — no libraries, no canvas, just a single HTML file.

## Features

- **Haunted castle** silhouette with turrets and barred windows
- **Animated ghost** that drifts across the scene, fades in and out, and bobs gently
- **Storm clouds** rolling across a dark sky
- **Lightning bolts** that flash periodically (3 independent cycles)
- **Bats** that fly overhead occasionally — 3 bats, each with independent flight paths and wing-flap animation
- **Storm leaves** blowing leftward across the scene in the wind
- **Fog wisps** drifting at ground level
- **Trees** swaying in the storm
- **Graveyard** with tombstones and a wrought-iron fence

### Sound (click to enable)

All audio is synthesized in real-time via the Web Audio API — no audio files.

- **Wind** — layered bandpass-filtered noise for a howling wind bed
- **Thunder** — synchronized to the CSS lightning flashes using `performance.now()`:
  - Sharp crack (broadband noise, 45ms decay)
  - Sub-bass punch (55Hz sine, 85ms decay)
  - Two bandpass body resonances (118Hz + 310Hz)
  - Three staggered rumble echoes simulating near / mid / far terrain reflections
- **Wolf howl** — synthesized with two oscillators + vibrato LFO + breath noise; fires with 10% probability every 10 seconds

## Usage

Open `ghost-castle.html` in any modern browser. Click anywhere on the scene to enable sound.

No build step, no dependencies.
