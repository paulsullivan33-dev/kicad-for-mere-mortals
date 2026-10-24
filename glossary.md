# Glossary

**Annotation** — numbering every part on
the schematic uniquely (R1, R2, U1…). The
references are how the schematic, board
and BOM refer to the same part. Chapter 5.

**BOM** — bill of materials: the parts
list, one row per distinct part, exported
from the schematic. Chapter 11.

**Board** — the physical printed circuit
board; also, in KiCad, the `.kicad_pcb`
file and the editor that draws it.

**Courtyard** — the outline on a
footprint's `F.CrtYd` layer marking the
space the part claims. DRC uses it to
spot collisions. Chapter 10.

**DRC** — design rules check: the PCB
editor's checker, testing the board
against manufacturing rules — clearances,
widths, unconnected pads. Chapter 9.

**Drill file** — the manufacturing file
listing every hole's position and size
(`.drl`). Sent with the Gerbers.
Chapter 11.

**Edge.Cuts** — the board layer holding
the outline the fab house cuts to.
Chapter 8.

**ERC** — electrical rules check: the
schematic editor's checker, testing pin
connections against pin types — unconnected
pins, outputs tied to outputs, unpowered
power pins. Chapter 6.

**Fab house** — the fabrication house:
the company that turns Gerber and drill
files into bare boards.

**Footprint** — a part as the board sees
it: the copper pads it solders to, at
true size and spacing. Lives in a
footprint library; named from its
schematic symbol. Chapters 2 and 7.

**Gerber** — the per-layer drawing files
(`.gbr`) describing copper, mask,
silkscreen and outline; the manufacturing
lingua franca since long before KiCad.
Chapter 11.

**Net** — one electrical connection: every
pin and pad the schematic joins, by wire
or by sharing a label, is one net, named
(`GND`, `+9V`, …) and carried into the
board. Chapters 5 and 7.

**Net class** — a named bundle of board
rules (clearance, track width, via size)
applied to a group of nets. Chapter 9.

**Netlist** — the plain list of nets and
the pads on each: what "update PCB from
schematic" carries between the two
drawings. Chapter 7.

**Pad** — one copper landing on a
footprint, where one pin of a real part
solders down. Pads are numbered to match
symbol pins.

**Pick and place** — the file of
component positions and rotations an
assembly service uses to populate a
board. Chapter 11.

**Pin type** — a symbol pin's declared
electrical character (input, output,
power in, passive…). ERC judges
connections by these. Chapter 6.

**PWR_FLAG** — a schematic symbol that
promises ERC a net is powered from
off-sheet. One per externally supplied
net. Chapter 6.

**Ratsnest** — the hair-thin straight
lines the PCB editor draws for every
connection not yet made in copper; the
layout's work list. Chapters 7 and 8.

**Schematic** — the circuit as meaning:
symbols joined by wires, in the
`.kicad_sch` file. Chapters 5 and 6.

**Silkscreen** — the printed layer
(usually white) carrying part outlines,
references and labels onto the board's
surface.

**Symbol** — a part as the schematic
sees it: the drawing and its pins. Lives
in a symbol library. Chapters 2 and 5.

**Via** — a plated hole whose only job is
carrying a track from one copper layer to
another. Chapter 8.

**Zone** — a region of copper belonging
to one net, filled around other features;
the usual home of a ground plane.
Chapters 8 and 9.
