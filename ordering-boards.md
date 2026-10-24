# Ordering Boards

This chapter turns a checked design into
files, and files into boards in a parcel.
The export half ran for real in this
guide's lab; the ordering half is a
walkthrough of what fab houses ask for
and how not to be surprised by it.

## What a fab house wants

A fabrication house does not want your
KiCad project. It wants the manufacturing
description of the board, in the
industry's long-standing formats:

| File set | Contents |
|---|---|
| **Gerbers** (`.gbr`, one per layer) | The copper, solder mask, silkscreen and outline drawings, layer by layer |
| **Drill file** (`.drl`) | Every hole: where, how big, plated or not |
| **Your choices on their form** | Thickness, colour, finish, quantity |

Together these are "the Gerbers", and
producing them correctly is a solved
problem — which is exactly why you let
KiCad solve it rather than improvising.

## Exporting, two ways

**In the PCB editor:** **File → Fabrication
Outputs → Gerbers**, choose a folder, tick
the layers your board uses, **Generate**,
then **Generate Drill Files** in the same
dialogue. The defaults suit two-layer
boards at mainstream houses.

**From the command line** — the way the
lab did it, and the way worth scripting
once a design changes often:

```bash
mkdir -p fab
kicad-cli pcb export gerbers \
  --output fab/ blinker.kicad_pcb
kicad-cli pcb export drill \
  --output fab/ blinker.kicad_pcb
```

Check: the `fab/` folder holds a Gerber
per layer — top and bottom copper
(`.gtl`, `.gbl` in the classic naming, or
`-F_Cu.gbr` and `-B_Cu.gbr` in KiCad's own
naming, depending on the exporter's
options), mask, silkscreen, the edge
cuts, and one drill file. Count them
against your layer list; a missing layer
in the zip is a missing layer on the
board.

## The parts list

The board is only half the parcel habit.
The **bill of materials** (BOM) lists
what to buy and solder:

```bash
kicad-cli sch export bom \
  --output blinker.csv blinker.kicad_sch
```

One row per distinct part: references,
value, footprint. The BOM is only as true
as the values you typed in chapter 5 —
another reason to write values the way
people write them.

If a house is also *assembling* boards
for you (placing and soldering the parts,
"PCBA"), it will additionally ask for a
**pick and place** file — component
positions and rotations — exported from
**File → Fabrication Outputs → Component
Placement** or:

```bash
kicad-cli pcb export pos \
  --output blinker-pos.csv blinker.kicad_pcb
```

Assembly multiplies both the cost and
the ways to be misunderstood; for a
first board, bare boards and your own
soldering iron teach more per penny.

## Look at the Gerbers before you send them

Every fab house's viewer, and KiCad's own
**GerbView**, renders the export as the
factory will read it. Spend two minutes:
the outline is the shape you meant, the
silkscreen text is the right way round,
the holes are where the parts are. This
is the last moment a mistake costs
nothing.

## Ordering, honestly

Upload the zipped Gerbers, choose
thickness (1.6 mm is the unremarkable
standard), a colour you like, the usual
lead-free finish if offered at no
premium, and the smallest quantity while
you are learning — boards are commonly
priced in fives, and five is plenty to
populate two and frame your mistakes.
Prices at the well-known low-cost houses
start at a few dollars for five small
boards, plus postage that often exceeds
the boards; treat any exact figure,
including that one, as a snapshot that
will have moved by the time you order.

Then wait, and when the parcel comes,
hold the board against chapter 8's 3D
view and chapter 9's clean DRC report.
The first board you designed, in your
hand, is the moment the two drawings stop
being an abstraction.
