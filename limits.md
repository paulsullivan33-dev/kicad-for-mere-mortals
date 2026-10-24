# Limits

What KiCad doesn't do, stated plainly
enough to plan around.

## It checks drawings, not ideas

ERC and DRC between them can prove your
board is the circuit you drew, drawn
legally. Neither knows the circuit is
wrong: a timing network calculated for
the wrong flash rate, a regulator without
its stability capacitors, an LED fed
three times its rated current all pass
both checkers on their way to not
working. Simulation helps some designs
and is, in KiCad, a guest (chapter 1);
the rest is datasheets and arithmetic.
This is not a KiCad flaw so much as the
shape of the craft, but beginners meet
it here first, so here is where it's
written down.

## The checkers trust your libraries

Every ERC verdict rests on pin types
declared in symbols; every DRC verdict
on footprints being honest. A downloaded
symbol with a wrong pin type, or a
footprint whose pads are numbered
creatively, produces a board that passes
and fails. Chapter 10's rule — datasheet
first, always — is the limit's other
half.

## Big boards are a different sport

This guide's scale is deliberate: a
handful of parts, two layers, hand
soldering. KiCad itself goes far beyond
that — multilayer boards, length-matched
high-speed routing, designs with
thousands of parts exist and ship — but
the *working methods* change with scale:
impedance control, stackup negotiation
with the fab house, team libraries, design
reviews. Nothing here pretends to teach
those, and the neighbours chapter
includes tools whose professional depth
is aimed at exactly that world.

## No autorouter worth the name

KiCad routes what you route. External
autorouters exist and can be bolted on,
and on a dense board they have their
place; on boards at this guide's scale
they mostly produce routes you cannot
read and would not have chosen. If your
project's joy is the circuit and not the
board, a neighbour with stronger
automation may suit you better — said
without shame in either direction.

## The 3D view is only as real as its models

The 3D viewer renders footprints that
have models. A minimal install — this
guide's own lab included — may carry no
3D library at all, in which case every
part renders as bare pads and the
mechanical checks of chapter 8 (tall
parts, overhangs, collisions) are ones
you do with calipers and imagination.
The electrical design is unaffected; the
illusion of completeness is the risk,
so it's stated here.

## Your fab house is part of the design

Minimum clearances, hole sizes, board
thicknesses and finishes vary by
manufacturer. The defaults in chapter 9
suit the mainstream low-cost houses; a
board designed tighter than your chosen
house can build is a board that comes
back wrong or doesn't come back. Match
the rules to the maker before the final
DRC, not after the parcel.
