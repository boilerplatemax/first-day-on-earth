# First Day on Earth

A tiny browser game: you're an alien disguised as the new kid. Each class period
the teacher announces something to build out of shapes — but you can't read
English. Your translator only *describes* the word. Build something passable,
sneak looks at your neighbours without getting caught, and survive Show & Tell
until the last bell.

## Run it

Just open `index.html` in a modern browser (Chrome, Firefox, Safari, Edge).
No build step, no backend, no install. It loads [three.js](https://threejs.org/)
`0.160.0` from a CDN via an import map, and (optionally) the *Press Start 2P*
pixel font from Google Fonts. An internet connection is needed on first load
so the CDN modules can be fetched.

```
# or serve locally if your browser blocks module imports over file://
python3 -m http.server 8000   # then visit http://localhost:8000
```

## How to play

- **Build:** pick a shape (keys `1`–`5`) and a colour (swatches), then click your
  desk to place a piece. `[` `]` or scroll to resize, `R` to rotate, `F` to flip,
  `Z` to undo. Max 12 pieces.
- **Peek:** hold `A` / `D` to lean toward a neighbour's desk. If their head turns
  toward you while you're peeking — or Ms. Huxley spots you — suspicion rises.
  Watch for the `❗` cue and the red screen-edge glow.
- **Sabotage** (from Art onward): press `E` while peeking to mess with a
  neighbour's build. Risky if seen.
- Bad grades, getting caught, and copying a neighbour too closely raise
  **Suspicion**. At 100 you're caught. Survive all five periods to win.
- `Esc` pauses · `` ` `` toggles a debug overlay.

The whole game is a single self-contained `index.html`, organised into clearly
labelled sections (config/data, rendering + dither, classroom scene, build
system, kid AI, teacher AI, grading, suspicion, onboarding/tutorial, UI, game
state). The grader (`gradeBuild`) is isolated so it can be swapped for an AI
grader later; `renderCleanSnapshot(build)` is included (unused) for that purpose.
