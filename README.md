# KiCad for Mere Mortals

Somewhere between the blinking LED on a
breadboard and a parcel from a fabrication
house sits a skill that looks harder than
it is: drawing the board properly.
**KiCad** is the open-source suite that
does the whole job — schematic, board
layout, the checkers that keep both
honest, and the manufacturing files a fab
needs — and it is what working engineers
reach for when the board is real. This
guide teaches that workflow the plain
way, on one small board you design end to
end: a 555 timer that blinks an LED, from
an empty project to a set of Gerber files
you could send away today.

The lab behind this guide ran the real
thing: **KiCad 8.0.9**, from the project's
own stable PPA on Ubuntu 24.04, with its
real symbol and footprint libraries. The
lab machine has no display, so the sample
board was authored the way KiCad stores
it — as files: a schematic built from the
genuine library symbols, and a board built
with KiCad's own `pcbnew` tooling from the
genuine footprints — and then judged by
the same tools a reader uses. The
finished schematic passes ERC with zero
errors and zero warnings; its exported
netlist was read net by net against the
intended circuit and matches, pin by pin;
the finished board passes DRC with zero
violations and zero unconnected pads; and
the full manufacturing set — Gerbers,
drill file, bill of materials, position
file — was generated and inspected. What
the lab could not do, it did not fake:
nobody clicked through the editors, the
ground zone's fill is a GUI act the
headless lab could not perform (the board
routes ground as tracks beneath the zone
instead, and says so), and no order was
placed with a real fab. `criteria.md`
keeps the full ledger of what was run and
what was only read.

## What this guide covers

- [**What KiCad is**](what-kicad-is.md) —
  the mental model: two drawings (a
  schematic that says what connects, a
  board that says where it sits) and the
  checkers that keep them agreeing; what
  it is not (a simulator first, an
  autorouter worth trusting)
- [**The moving parts**](the-moving-parts.md) —
  the project manager, the two editors,
  symbols, footprints, libraries, netlists
  and `kicad-cli` — which file holds what
- [**Installing KiCad**](installing-kicad.md) —
  Windows, Mac and Linux (the project's
  own PPA on Ubuntu), the libraries to
  take, and the one-minute verification
- [**Your first project**](your-first-project.md) —
  the Blinker board: a 555 LED flasher on
  a 9 V battery, its parts list, and what
  each part is doing there
- [**Drawing the schematic**](drawing-the-schematic.md) —
  placing symbols, wiring them, power
  symbols and labels, and annotation
- [**Checking the schematic**](checking-the-schematic.md) —
  ERC: what it catches, the power-flag
  lesson every beginner meets, and
  reading a report to zero
- [**Footprints and the board**](footprints-and-the-board.md) —
  assigning a physical footprint to every
  symbol and bringing the design onto the
  board, ratsnest and all
- [**Laying out the board**](laying-out-the-board.md) —
  placing parts, routing tracks, vias,
  copper zones and the board outline
- [**Design rules and DRC**](design-rules-and-drc.md) —
  clearances, widths and hole sizes as
  numbers; running DRC and fixing what it
  finds, crossings included
- [**Libraries, symbols and footprints**](libraries-symbols-and-footprints.md) —
  how the libraries are organised, and
  making a symbol or footprint of your own
- [**Ordering boards**](ordering-boards.md) —
  the manufacturing files, checking them
  before you send them, what a fab asks
  and what it costs
- [**Recipes**](recipes.md) — four small
  boards to build next: an optocoupler
  doorbell interface, a 7805 power supply
  board, an LDR night-light, and an SMD
  breakout adapter
- [**The neighbours**](the-neighbours.md) —
  Fritzing, EasyEDA, LibrePCB, Horizon EDA
  and the commercial tools, honestly
  placed
- [**Limits**](limits.md) — what KiCad
  will not do for you: simulation's place,
  autorouting, high-speed and flex work,
  and other edges
- [**Troubleshooting**](troubleshooting.md) —
  symptom → fix for the failures this
  guide's own lab met, and the ones every
  first board meets
- [**Glossary**](glossary.md) — the terms,
  in plain words

The sample board, its clean ERC and DRC
reports and its manufacturing files live
in `kicad-lab/blinker/`; the lab's
transcripts are in `kicad-lab/transcripts/`
and its notes in `examples/lab-notes.txt`.
