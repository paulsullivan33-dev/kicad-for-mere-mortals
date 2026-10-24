# Footprints and the Board

The schematic says what connects. The
board needs to know what everything *is* —
how big, with what pads — before it can be
drawn. That translation, symbol to
footprint, is this chapter.

## Assigning footprints

Back in the schematic editor, open
**Tools → Assign Footprints**. The window
lists every part down the middle, the
footprint libraries on the left and the
footprints in the chosen library on the
right. For each part, pick the footprint
that matches the physical component you
will actually buy and solder:

| Ref | Part | Footprint for Blinker |
|---|---|---|
| U1 | NE555 | `Package_DIP:DIP-8_W7.62mm` |
| R1–R3 | Resistors | `Resistor_THT:R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal` |
| C1 | 47 µF electrolytic | `Capacitor_THT:CP_Radial_D5.0mm_P2.00mm` |
| C2 | 10 nF ceramic | `Capacitor_THT:C_Disc_D4.7mm_W2.5mm_P5.00mm` |
| D1 | 5 mm LED | `LED_THT:LED_D5.0mm` |
| J1 | Screw terminal | `TerminalBlock:TerminalBlock_bornier-2_P5.08mm` |

The names encode the truth that matters:
body size and pad spacing, in millimetres.
`P10.16mm` on the resistor is the distance
between its two pads; the resistor's leads
must bend to span it. A footprint that is
wrong in these numbers is wrong in the
world — the part will not fit, or will not
solder — and no checker will save you,
because KiCad cannot know which resistor
is in your parts drawer. Read footprint
names slowly. It is the cheapest care you
will ever take.

Filters at the top of the window narrow
the list by pin count and by the symbol's
own suggestions; most standard parts carry
a sensible default footprint already.

Check: the list shows a footprint against
every reference, with no blanks. A blank
here becomes a missing part on the board.

## Over to the board

Open the PCB editor and run **Tools →
Update PCB from Schematic** (or press
**F8** in either editor). KiCad reads the
schematic, and every footprint appears in
a pile at the cursor, trailing hair-thin
lines — the **ratsnest** — showing every
connection still to be made in copper.

Those footprints are now the board's
parts, and from here the schematic and
board stay in step two ways:

- **F8 again** after any schematic change
  brings the board up to date: new parts
  arrive, changed footprints swap,
  renamed references follow.
- **Update Schematic from PCB** (under the
  same Tools menu, going the other way)
  pushes back changes made board-side —
  the standard use is after swapping two
  gates or pins on the board for an easier
  route.

The ratsnest is not clutter; it is the
work list. Chapter 8 is about making it
go away one line at a time.

## The netlist, for the curious

What F8 carries across is the project's
**netlist** — the plain list of which pads
join which nets — and you can look at it
directly:

```bash
kicad-cli sch export netlist \
  --output blinker.net blinker.kicad_sch
```

The file is text (an S-expression, for the
KiCad-native format). Scripts and other
CAD tools read netlists; humans mostly
read them to answer "is pin 6 really on
the same net as pin 2?" without opening an
editor. It is also the sharpest proof that
the schematic and board agree about what
the circuit *is*: they are both built
from this list.
