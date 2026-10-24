# The Moving Parts

A KiCad design looks like one thing — "my
project" — but it is several files and
several programs cooperating. Knowing
which part holds what turns most beginner
confusion into a named problem.

## The project

A project is a folder. Inside it, one file
matters most:

| File | What it holds |
|---|---|
| `name.kicad_pro` | The project itself — settings, and pointers to the two drawings |
| `name.kicad_sch` | The schematic — symbols, wires, labels |
| `name.kicad_pcb` | The board — footprints, tracks, zones, outline |
| `sym-lib-table` | Which symbol libraries this project uses |
| `fp-lib-table` | Which footprint libraries this project uses |
| `*.kicad_sym`, `*.kicad_mod` | Your own symbols and footprints, when you make them (chapter 10) |

All of these are text files. You can open
them in a text editor and read them, put
the folder in version control, and email
it to a friend who can open exactly what
you sent. There is no database and no
account. If the folder exists, the project
exists — which makes backing up a design
as simple as copying the folder, and makes
chapter 11's exports a one-way trip: the
fab house gets copies, never your project.

## The programs

KiCad is a suite. You will spend your time
in two of its windows and visit the rest:

- **The project manager** — the home
  window. Opens the project, lists its
  files, launches the editors.
- **The schematic editor** — where the
  circuit is drawn and electrically
  checked (chapters 5 and 6).
- **The PCB editor** — where the board is
  laid out and checked against
  manufacturing rules (chapters 7 to 9).
- **The symbol and footprint editors** —
  where you make or adjust the drawings of
  parts (chapter 10).
- **`kicad-cli`** — the command-line tool.
  It runs the checkers and produces the
  manufacturing files without opening any
  window at all. This guide's lab drove
  KiCad through `kicad-cli` for
  everything except the drawing itself,
  and chapter 11 shows it earning its
  keep: scripts can ask "does this board
  still pass?" and "export the files
  again" without a human clicking.

## Symbols, footprints, and the wire between them

The idea that confuses every beginner,
stated once, plainly:

- A **symbol** is a part as the schematic
  sees it: a box or zigzag with pins. It
  lives in a *symbol library*.
- A **footprint** is the same part as the
  board sees it: the copper pads it will
  be soldered to, in their true size and
  spacing. It lives in a *footprint
  library*.
- A schematic symbol **names** the
  footprint it wants. That name is the
  only link between the two drawings.

One part, three descriptions. A common
resistor might be drawn with one symbol
but soldered down in half a dozen sizes,
each a different footprint. KiCad keeps
the descriptions separate so you decide
the physical size when you design the
board, not when you draw the idea.

The libraries KiCad ships with are large —
thousands of symbols and footprints,
maintained by the project — and they are
read-only for good reason: your edits go
in libraries of your own (chapter 10),
which no upgrade will overwrite.

## What checks what

Two checkers guard the two drawings, and
much of this guide is about pleasing them:

- **ERC** (electrical rules check) reads
  the schematic and complains about pins
  that go nowhere, outputs wired to
  outputs, and power nobody is supplying.
  Chapter 6.
- **DRC** (design rules check) reads the
  board and complains about tracks too
  close together, pads left unconnected,
  and anything else the chosen
  manufacturing rules forbid. Chapter 9.

Neither checker knows whether your circuit
is a *good idea*. They know whether it is
the idea you drew, drawn legally. That
distinction runs through the whole guide.
