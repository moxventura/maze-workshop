# Maze Workshop

**[Open the generator →](https://moxventura.github.io/maze-workshop/)**

A single-file, client-side generator for printable maze sheets. Runs entirely
in the browser — no build step, no server, nothing uploaded. Clone the repo and
open `index.html` locally if you prefer.

![themes](https://img.shields.io/badge/themes-7-blue) ![styles](https://img.shields.io/badge/maze%20styles-5-green)

## What it does

- **4 grid shapes** — Square, Circle, Hex and Picture:
  - **Circle** is a theta maze: concentric rings that subdivide as they widen,
    entered at the top with the goal in the hub.
  - **Hex** is a sigma maze — six ways out of every cell, so there is no
    straight line to follow.
  - **Picture** cuts the maze to the silhouette of the theme's character, so
    the unicorn maze is unicorn-shaped and the alien maze is a big-headed alien.
    Enter at the top of the shape, leave at the bottom.
- **7 themes** — Mineshaft, Explorer, Unicorn, Space, Dino, Alien, Monsters.
  Each has its own pixel-art character at the entrance, a goal sprite at the
  exit, and ink colour: the alien crosses the crop circles to reach his flying
  saucer, the unicorn hunts rainbows, the little monster finds its way back to
  its ball.

  All sprites are original pixel art drawn for this project, so the repo can
  stay MIT-licensed. The monster theme is a monster-catching motif, not any
  particular franchise's characters.
- **5 maze styles**, multi-select and dealt out across the page one per maze:
  Classic, Loopy, Against the grain, Spiral trap, The lot.
- **4 difficulties** plus Ladder, which ramps Easy → Expert down the page.
- **1–8 mazes per page**, laid out to fit exactly one A4 or US Letter sheet.
- **Seeded** — the same seed always produces the same sheet.
- Optional solution overlay, and a difficulty read-out that is not printed.

## Playing

Switch the **Mode** control to **Play**, or just click any maze on the sheet.

- **Drag** a line with the mouse or a finger, **or** steer with the arrow keys
  or `WASD`. Retrace your line to rub it out, exactly like a pencil.
- Hex mazes have six ways out of every cell and no straight up or down, so they
  also get six exact keys: `Q`/`E` and `Z`/`C` for the diagonals, `A`/`D` for
  left and right. The arrows still work — they take the only open way when
  there is one, and otherwise carry on the way you were going.
- **Timer, move count and your personal best** per maze, saved in the browser.
  Stars are awarded against the shortest possible route.
- **Torchlight** hides the walls beyond a small radius and reveals them as you
  explore. The goal stays visible so you always know where you are heading.
- **Stuck?** dots in the next few steps. **Show the way** draws the rest of the
  route, and the run stops being scored.
- **Copy link** gives you a URL carrying the exact maze — shape, theme,
  difficulty, styles, sheet layout and seed — so two people can race the same
  one.

Movement is "walk the graph": a legal move is an open edge to a neighbouring
cell, which is why all four shapes are playable with no per-shape movement code.

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

Each maze is the best of 16 candidates, scored on *forks along the route* ×
*how far a wrong turn carries you before it is provably wrong*, with candidates
whose route is too short rejected outright. The score is also weighted towards
mazes that keep branching **near the exit**, because working backwards from the
goal is the usual shortcut — maze designers counter it by branching in both
directions.

All four shapes share one carving core: a grid is just cells, neighbours and
wall geometry, so braiding, bias, scoring and solving are shape-agnostic.

Sources: Walter Pullen's [Think Labyrinth](https://www.astrolog.org/labyrnth/algrithm.htm)
and Jamis Buck's *Mazes for Programmers*.

## Licence

[MIT](LICENSE)
