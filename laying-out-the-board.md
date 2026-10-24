# Laying Out the Board

Layout is where the design becomes a
physical object with habits of its own.
The craft has whole books devoted to it;
this chapter covers the working method
that gets a small board right, in the
order experienced designers actually do
the steps.

## 1. Draw the outline first

The board's edge lives on the **Edge.Cuts**
layer. Draw it in the PCB editor with the
line and rectangle tools: for Blinker, a
plain rectangle of about 55 × 40 mm suits
the handful of parts and a 9 V battery
connector at one end. The outline is a
real constraint, not a suggestion — the
fab house cuts the board to this line,
and DRC (chapter 9) will hold everything
else inside it.

Mounting holes, if you want them, are
footprints too (the *MountingHole*
library) placed like any part — put them
in the outline step, not as an afterthought
in a corner the routing has already
claimed.

## 2. Place the parts

Drag each footprint (select, then **M**)
to roughly where it belongs, rotating
with **R**:

- **The connector goes at the edge.** J1
  at the board's end, where the battery
  leads reach it.
- **Fixed relationships next.** C1 sits
  near the 555, because in the circuit it
  *is* near the 555; parts that connect
  heavily belong near each other, and the
  ratsnest shortens visibly when you get
  it right.
- **Orientation is a decision.** The LED
  points the way you want the light to
  shine; polarised parts (C1, D1) go in
  the way the silkscreen will mark, which
  is also the way they must be soldered.
  The board will happily let you place a
  part backwards; the circuit will not.

Good placement is most of layout. When
the parts sit well, the ratsnest looks
like short local hops. When it looks like
a cat's cradle, move parts — routing
cannot rescue a bad arrangement, only
memorialise it.

## 3. Route the tracks

Routing (**Route → Route Tracks**, the
**X** key) draws copper between pads:
click a pad, and KiCad walks a track with
you, respecting clearances as you go, and
clicks it down at the pad the ratsnest
intended. Habits that keep small boards
easy:

- **Shortest, plainest path first.** Route
  the ground and power nets early while
  the board is empty; the fiddly ones get
  the room that's left.
- **45° bends, not right angles.** Tracks
  that turn at diagonals look tidier and
  behave better at every size this guide
  covers.
- **Use the other side.** Blinker is a
  two-layer board: when a track cannot
  get there on top copper, press **V**
  mid-route to drop a via (a plated hole)
  and continue on the bottom layer. Two
  layers forgive a great deal of beginner
  routing.
- **Width carries meaning.** The default
  track width suits signals. Power and
  ground traces can be drawn wider —
  chapter 9's net classes make that
  automatic rather than remembered.

Rip up and retry freely (**Backspace**
while routing deletes the last segment;
selecting a track and deleting removes
it). No fab house has ever charged for
the tracks you deleted.

## 4. Add a ground zone

Most small boards finish with a **copper
zone**: a region of one layer — usually
the bottom — filled with copper joined to
GND. It gives every ground connection a
short path home, makes the board easier
to route (the zone connects ground pads
for you), and is what real boards look
like. Draw it with **Place → Add Filled
Zone** over the whole outline, choose the
GND net, then **Edit → Fill All Zones**
(**B**). The fill keeps the clearances
chapter 9 sets, flowing around tracks and
pads like water around stones.

Check: after filling, the ratsnest's
ground lines are gone — the zone made
those connections — and what remains is
genuinely unrouted.

## The 3D viewer, briefly

**View → 3D Viewer** renders the board as
an object: parts standing on it, silk
screen printing visible, the LED on the
edge you chose. It is not vanity. It
catches the footprint that is mirrored,
the connector overhanging the edge, the
electrolytic lying where a tall part
cannot be — the class of mistake that
looks fine in plan view and ridiculous in
the world. One honest limitation, which
this guide's lab met head-on: a footprint
only appears in 3D if a model exists for
it in the 3D libraries, and a minimal
install may not carry those (chapter 3).
The board is no less real for rendering
some parts as bare pads.
