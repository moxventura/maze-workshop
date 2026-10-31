# Maze Workshop

**[Open the generator →](https://moxventura.github.io/maze-workshop/)**

A single-file, client-side generator for printable maze sheets. Runs entirely
in the browser — no build step, no server, nothing uploaded. Clone the repo and
open `index.html` locally if you prefer.

![themes: mineshaft, explorer, unicorn, space, dino](https://img.shields.io/badge/themes-5-blue) ![styles](https://img.shields.io/badge/maze%20styles-5-green)

## What it does

- **5 themes** — Mineshaft, Explorer, Unicorn, Space, Dino. Each has its own
  pixel-art character at the entrance, a goal sprite at the exit, and ink colour.
- **5 maze styles**, multi-select and dealt out across the page one per maze:
  Classic, Loopy, Against the grain, Spiral trap, The lot.
- **4 difficulties** plus Ladder, which ramps Easy → Expert down the page.
- **1–8 mazes per page**, laid out to fit exactly one A4 or US Letter sheet.
- **Seeded** — the same seed always produces the same sheet.
- Optional solution overlay, and a difficulty read-out that is not printed.

## Printing

Press the Print button, or Ctrl/⌘+P. The sheet is sized against the real
printable area (page minus 12mm margins) and then measured and trimmed after
layout, so it comes out as exactly one page at every maze count.

## How the mazes are made

The generator follows the maze-design literature rather than the usual
textbook depth-first carve, which produces long corridors with few real choices:

- **Growing tree with mixed cell selection** — tunes Pullen's "river" factor:
  fewer but longer decoys instead of many one-cell stubs that are trivial to reject.
- **Passage bias** — gives the maze a grain running across the line of travel,
  since a maze is harder navigated "against the grain".
- **Braiding** — opens dead ends into loops, which defeats both wall-following
  and dead-end filling.
- **Spiral trap** — a unicursal spiral wired into the maze at two points; you
  cannot tell by eye which side a spiral passage comes out of.
- **Off-corner entrance and exit** — removes the "just head for the far corner"
  shortcut, while staying far enough apart to keep the journey long.

Each maze is the best of 22 candidates, scored on *forks along the route* ×
*how far a wrong turn carries you before it is provably wrong*, with candidates
whose route is too short rejected outright.

Sources: Walter Pullen's [Think Labyrinth](https://www.astrolog.org/labyrnth/algrithm.htm)
and Jamis Buck's *Mazes for Programmers*.

## Licence

[MIT](LICENSE)
