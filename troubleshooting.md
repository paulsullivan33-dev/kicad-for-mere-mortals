# Troubleshooting

Symptom first, cause second, fix last.
Most of these were met for real while
building this guide's sample board; the
rest are the ones every first board
meets.

## ERC says a pin is "not connected" that is visibly wired

The wire ends *on* another wire instead
of *at* its end. KiCad connects wires
that share an endpoint, and wires that
meet at a junction dot — but a wire that
touches the middle of another wire with
no junction is just crossing it, however
connected it looks. Fix: end the wire on
the other wire's endpoint, or place a
junction (the dot) exactly where they
meet. This guide's lab board lost the
555's discharge pin to exactly this; the
lab notes tell the story.

## ERC says "power pin not driven" / "input pin not driven" on the supply

Nothing on the schematic *outputs* power
— the battery connector's pins are
passive, so as far as ERC knows the +9V
net appears from nowhere. That is what
`PWR_FLAG` is for: place one on the power
net and one on ground (chapter 6). The
flag is you, the designer, telling the
checker "a supply enters here on
purpose." Do not silence it by changing
pin types in the library symbol instead.

## Dozens of "off grid" warnings after moving things

Schematic parts and wire ends belong on
the 1.27 mm (50 mil) connection grid —
symbol pins are drawn on it, and anything
placed off it can *look* connected while
missing the pin by a fraction. Turn the
grid on, set it to 1.27 mm for schematic
work, and nudge the offenders onto it.
A layout built off-grid produces these
warnings by the dozen; they are worth
fixing properly rather than excluding,
because the same sloppiness causes the
"not connected" error above.

## `kicad-cli` answers "Maximum number of positional arguments" to `sch erc` or `pcb drc`

Your KiCad is version 7 or older: its
`kicad-cli` can export but has no `erc`
or `drc` subcommands (they arrived in
KiCad 8). Either run the checks in the
GUI under **Inspect**, or install the
current release the way chapter 3
recommends. `kicad-cli --version` tells
you which situation you are in.

## A part is missing from the board

Its symbol has no footprint assigned, or
the footprint field names a library your
fp-lib-table doesn't include (watch for
library renames between versions — the
lab met a terminal block whose library
is `TerminalBlock`, not the longer name
older tutorials use). Fix in the
schematic: assign the footprint (chapter
7), check the library is in the table,
then update the board again. The BOM
export (`kicad-cli sch export bom`)
lists every part's footprint and shows
the blank ones plainly.

## DRC reports ground pads unconnected, but the zone covers them

The zone is drawn but not *filled*, or
the pads' connection style leaves them
isolated. Fill it — press **B** in the
board editor — and re-run DRC. If a pad
still complains, zoom in: the zone keeps
its clearance from tracks of other nets,
and a pad can end up on an island the
fill cannot reach without breaking that
clearance. The cure is a via or a short
track stitching the island to the rest
of the net, not shrinking clearances
until the error gives up.

## DRC: "tracks crossing"

Two tracks of different nets occupy the
same copper. On one layer that is a
short circuit, whatever the screen made
it look like. Re-route one of them:
around, or — on a two-layer board —
through a via to the other layer for the
crossing stretch and back (chapter 9).
Do not "fix" it by narrowing tracks until
they fit past each other; crossing means
touching, not merely close.

## DRC: "hole too close to hole" after placing a via

Vias have a minimum distance from other
drilled holes — the lab's first CV via
sat 0.78 mm from a chip pin and failed
with 0.18 mm to spare against a
0.2495 mm minimum. Move the via further
along the track; a via wants roughly a
millimetre of elbow room from pads and
other vias on a beginner board.

## The Gerber viewer shows the board mirrored or the text backwards

You plotted, or are viewing, a bottom
layer as if it were the top. Bottom
copper and silkscreen are *supposed* to
look reversed when viewed from above —
the fab flips them when making the
board's underside. KiCad's own Gerber
viewer (chapter 11) has a "flip board"
view for looking at the bottom properly.
Only worry if the *top* layer reads
backwards.

## The fab's preview shows a different board size than you designed

The outline lives on the **Edge.Cuts**
layer, and the fab reads its size from
that layer's export — if the outline was
drawn on a drawing or silkscreen layer,
or the Edge.Cuts Gerber is missing from
the set, the fab guesses from the copper,
often wrong. Check that `Edge_Cuts` is
in the plotted set (chapter 11's list)
and that exactly one closed outline is
on it.

## Everything checks, but the LED lights backwards

ERC and DRC verify that the board matches
the schematic; they cannot verify that
the schematic matches physics. An LED
drawn anode-to-ground passes both
checkers and fails on the bench. The
defence is chapter 5's discipline: check
polarised parts (LEDs, electrolytic
capacitors, diodes, IC pin 1) against the
datasheet once, by eye, before the board
is ordered — the one review no tool in
this guide can do for you.
