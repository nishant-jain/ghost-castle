# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A standalone single-file HTML Halloween animation (`index.html`) using SVG, CSS animations, and Web Audio API. No build step, no dependencies, no package manager.

**To run:** Open `index.html` in any modern browser. Click the sound button to enable audio.

## Architecture

Everything lives in `index.html` (~1100 lines), organized into three sections:

### CSS (lines 7–296)
Defines all animations: ghost float/sway/glow, parallax mountains, fog drift, star twinkle, lightning flash (3 independent cycles), cloud drift (9 groups with staggered delays for parallax depth), tree sway (18 trees with individual timing/pivot origins), bat wing flap, bat flight paths, storm leaf patterns, and sound button styling.

### SVG (lines 301–670)
Defines gradients, sky/moon/stars, 3 sky flash overlays, 3 lightning bolt pairs (outer thick stroke + inner white for glow), 3 bat groups, 9 cloud groups at varying altitudes, parallax mountain layers (far/near), castle structure (towers, battlements, barred windows), graveyard, ghost outline, and fog layer.

### JavaScript (lines 700–1123)
Two subsystems:

**Ghost loop** — picks from 21 spawn positions, shows ghost 500–1900ms, hides 3–10s, uses CSS transitions + JS for position control.

**Audio system** (click-triggered, Web Audio API only — no audio files):
- Wind: layered bandpass-filtered noise buffers + LFOs for gusting, frequency sweep over 40s
- Leaf rustle: stochastic amplitude-modulated noise
- Owl calls: sine fundamental + 2nd harmonic + vibrato LFO, scheduled every 9–24s
- Thunder: broadband crack + sub-bass + dual bandpass resonances + 3 staggered rumble echoes, **synchronized to CSS lightning** via `performance.now()` — each of 3 lightning cycles (8s, 11s, 14s periods) has a calculated flash-point that the JS matches audio scheduling to
- Wolf howl: sine + harmonic + vibrato, triggered with 10% probability every 10s

## Key Patterns

- **Parallax depth:** slower animation duration = farther away (clouds, mountains)
- **Thunder sync:** JS calculates CSS animation elapsed time using `performance.now()` to schedule thunder at the exact frame matching each lightning flash keyframe
- **All audio synthesized:** no `.mp3`/`.wav` files — realistic sounds come from layered oscillators, filtered noise, and envelope shaping
- **Organic variation:** multiple independent timers, probabilistic scheduling, and LFO modulation prevent repetitive loops
