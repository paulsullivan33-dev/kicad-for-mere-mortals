# What KiCad Is

KiCad is a suite of programs for designing
printed circuit boards — the green (or
black, or purple) boards inside nearly
every electronic product, with their copper
tracks, pads and white printed labels. You
draw what the circuit *means* in one
editor, and where the copper *goes* in
another, and at the end KiCad produces the
files a fabrication house turns into real
boards, ready for you to solder parts onto.

It is free and open-source software, and
it runs on Windows, Mac and Linux. It is
also genuinely professional software —
companies design shipping products in it —
that happens not to cost anything and not
to lock your files in somebody else's
cloud. That combination is why it is the
default recommendation for a first board.

## The two drawings

Everything in KiCad rests on two pictures
of the same circuit, kept in step by the
software:

| Drawing | Says | You edit it in |
|---|---|---|
| **Schematic** | What connects to what, and why | The schematic editor |
| **Board** | Where every part and track physically sits | The PCB editor |

The schematic is abstract: a resistor is a
zigzag, a chip is a box with numbered
pins, and lines mean "these pins are
electrically connected." The board is
concrete: that same resistor is a
rectangle of exact size with two copper
pads, and the connections are copper tracks
you draw on a board of a chosen size and
shape.

Neither drawing is optional decoration.
The schematic is what you think with; the
board is what gets manufactured. Chapter 2
explains the parts; chapters 5 to 9 walk
the path from one drawing to the other.

## Who it is for

KiCad suits anyone whose circuit has
outgrown a breadboard or a strip of
veroboard: the hobbyist whose project
deserves a tidy board of its own, the
student who needs a board for a course
project, the small team making a run of
fifty sensor boards, the repairer who
wants to reproduce a part nobody sells any
more. The common thread is that the board
itself is the goal — one design, made
real, possibly made again later.

## What it is not

- **Not a circuit simulator.** KiCad
  contains hooks for the ngspice simulator,
  and for some jobs that is useful, but
  simulation is a guest, not the host.
  KiCad's job is the board.
- **Not a breadboard with better graphics.**
  It will not stop you designing a circuit
  that cannot work. Its checkers (chapters
  6 and 9) catch wiring mistakes and
  manufacturing problems, not wrong ideas.
- **Not push-button.** There is an
  auto-router available as a separate tool,
  but KiCad expects you to place parts and
  draw tracks yourself. For the small
  boards this guide covers, that is a
  feature: you learn where things are.
- **Not a parts shop.** It designs the
  board. Ordering the board, and ordering
  the components to solder onto it, are
  separate steps with separate suppliers
  (chapter 11).

## The one-sentence version

If your circuit currently lives on a
breadboard and deserves to survive being
knocked off the bench, KiCad turns it into
a pair of checked drawings that a
fabrication house can build for a few
pounds, dollars or euros a board — at the
price of learning to think in two pictures
at once.
