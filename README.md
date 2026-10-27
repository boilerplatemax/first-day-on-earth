# First Day on Earth

A tiny browser game: you're an alien disguised as the new kid. Each class period
the teacher announces something to **draw** — but you can't read English. Your
translator only *describes* the word. Draw something passable, sneak looks at your
neighbours' papers without getting caught, and survive Show & Tell until the last
bell. The word is picked at random from a big pool, so no two days are the same.

## Run it

Open `index.html` in a modern browser. No build step, no backend. It loads
[three.js](https://threejs.org/) `0.160.0` from a CDN via an import map, and
(optionally) the *Press Start 2P* pixel font from Google Fonts. You need internet
on first load so the CDN module can be fetched.

```
# or serve locally if your browser blocks module imports over file://
python3 -m http.server 8000   # then visit http://localhost:8000
```

## How to play

- **Draw:** pick a crayon (left edge, or keys `1`–`8`) and draw on your paper with
  the mouse. `S` `M` `L` (or `[` `]` / scroll) set brush size, `ERASE`/`X` the
  eraser, `Z` undo, `C` clear.
- **Read the translator** (bottom-centre): it can't read the word, only describe
  it. That description is your only clue.
- **Peek:** hold `A` / `D` to lean toward a neighbour. A zoomed view of their paper
  pops up top-left. Stop before their head turns toward you (watch for the `!` and
  the warning beep) or Ms. Huxley's **vision cone** sweeps red over you.
- **Scribble** (from Art onward): hold `E` while peeking to mess up a neighbour's
  drawing. Risky if seen. Note: neighbours sometimes draw badly on purpose, so
  copying them can backfire.
- Bad grades, getting caught, and copying a neighbour too closely raise
  **Suspicion** (top-right). At 100 you're caught. Survive all five periods to win.
- `Esc` pauses · `` ` `` toggles a debug overlay.

## Structure

The whole game is one self-contained `index.html`, organised into labelled
sections: config/data, render+dither, scene, draw system, kid AI, teacher AI,
grading, suspicion, onboarding, UI, game state / show & tell, debug, boot.

The grader (`gradeDrawing`) is isolated so it can be swapped for an AI grader
later; it samples the paper into per-band colour coverage and scores it strictly
against each word's recipe. `renderCleanSnapshot(entity)` returns an undithered
PNG of a drawing, reserved for that future AI grader.
