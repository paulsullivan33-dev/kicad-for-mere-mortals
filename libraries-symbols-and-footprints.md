# Libraries, Symbols and Footprints

Sooner or later you meet a part KiCad's
libraries don't have, or have in a shape
you don't want. This chapter explains how
libraries are organised, where your own
parts belong, and how to make the two
things a new part actually needs: a symbol
for the schematic and a footprint for the
board.

## How libraries are found

Two small files in the project folder —
`sym-lib-table` and `fp-lib-table` — list
the libraries that project may use, by
nickname and path. KiCad also has global
tables of the same name, holding the
installed libraries. When a schematic
names a symbol `Device:R`, it means: the
symbol called `R` in the library
nicknamed `Device`, wherever the table
says that library lives.

Three consequences worth knowing:

- **A project is portable only with its
  tables.** Moving the folder moves the
  tables with it; a friend opening your
  project gets your library choices,
  which is the point.
- **The shipped libraries are read-only
  in spirit.** You *can* edit them, and an
  upgrade will silently replace your
  edits. Your own work goes in your own
  libraries, next to the project or in a
  folder of yours, added to the table
  under **Preferences → Manage Symbol
  Libraries** (and its footprint twin).
- **The schematic keeps its own copies.**
  Symbols placed on a sheet are embedded
  in the `.kicad_sch` file, so a project
  still opens and exports years later
  even if a library has moved on.
  Footprints on the board are likewise
  embedded in the `.kicad_pcb`. Libraries
  are where parts come *from*, not a
  live dependency of a finished design.

## Making a symbol

**Tools → Symbol Editor** in the project
manager. A symbol is a drawing plus pins,
and the pins are the part that matters:

1. Draw the body — a rectangle is a
   perfectly respectable integrated
   circuit.
2. Place pins around it. Each pin needs a
   **number** (the physical pin on the
   real part — this is what connects the
   symbol to footprint pads), a **name**
   (what it does), and an **electrical
   type** (input, output, power in, and
   so on — the types ERC judges by,
   chapter 6).
3. Set the symbol's default reference
   prefix (`U`, `Q`, `J`…) and, if it's a
   part you will reuse, the footprint it
   usually takes.

Pin *numbers* are the classic trap: a
symbol whose pins are numbered to look
tidy instead of matching the datasheet
produces a board that is tidy and wrong.
The datasheet's pinout diagram is the
only source; copy it pin by pin.

## Making a footprint

**Tools → Footprint Editor**. A footprint
is pads plus drawings:

1. Place pads at the datasheet's spacings
   — pad **numbers must match the
   symbol's pin numbers**, because number
   to number is the entire mapping.
2. Draw the part's outline on the
   silkscreen layer (**F.SilkS**) as the
   soldering human will see it, including
   the pin 1 mark.
3. Draw a courtyard on **F.CrtYd** around
   the whole part: the space it claims,
   which DRC uses to warn when two parts
   would collide.

Measure from the datasheet's mechanical
drawing, and add the small clearances
that make hand soldering possible —
pads a fraction longer than the
datasheet's minimum cost nothing and
forgive unsteady irons.

## The honest scope of this chapter

Whole afternoons live inside library
craft: multi-unit symbols (one chip drawn
as several boxes), symbols with hundreds
of pins, footprints for connectors that
mate with the physical world. This
chapter's claim is smaller and true:
the organisation is two tables and plain
files, a symbol is a drawing with honest
pins, a footprint is honest pads, and
both are checked by the same ERC and DRC
you already know. KiCad's own library
conventions (the "KLC" documents on the
project site) are the reference when a
part matters enough to make beautifully.
