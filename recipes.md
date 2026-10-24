# Recipes

Four small boards, each a step beyond
Blinker and each buildable with this
guide's chapters alone. The point of a
recipe here is the *idea* and the parts
that matter; the drawing is the practice.

## A doorbell that plays fair

**The problem:** a push-button, a long
cable run, and a microcontroller that
resets itself whenever the bell is
pressed, because the cable picks up every
electrical cough in the house.

**The board:** an optocoupler (a chip
containing an LED and a light sensor,
`PC817`) between the button circuit and
the logic. The button side drives the
coupler's LED through a resistor; the
sensor side pulls a logic pin low through
a pull-up resistor. The two sides share
no copper at all, so the cable's noise
stays on its side of the light gap.

**Teaches:** reading a second datasheet's
pinout, a symbol you may have to check
pin by pin (chapter 10), and keeping two
grounds genuinely separate — no ground
zone bridging the gap (chapter 8's zone
habit, deliberately withheld).

## A bench power supply's best friend

**The problem:** project boards want 5 V
or 3.3 V; the bench offers a 9 V battery
or a 12 V wall adapter, and fingers are
fallible about polarity.

**The board:** a bridge of four diodes
(any of the 1N400x family) so the input
works either way round, a `7805` (or a
`AMS1117-3.3` for the 3.3 V version)
regulator with the two capacitors its
datasheet insists on, an LED to say the
output is alive, and screw terminals at
both ends.

**Teaches:** datasheet-mandated parts —
the capacitors are not optional garnish,
they are the difference between a
regulator and an oscillator — plus a
first power net class with real current
in it (chapter 9).

## A night-light with manners

**The problem:** an LED that turns itself
on at dusk, the classic second project.

**The board:** a light-dependent resistor
and a fixed resistor forming a divider
whose voltage swings with the light,
feeding one transistor (`BC547`) that
switches a small cluster of LEDs. A
potentiometer in the divider sets how
dark "dusk" is.

**Teaches:** a design with no chip at all,
where the schematic's values genuinely
decide whether the thing works — the
class of correctness ERC cannot check
for you (chapter 6) — and laying out a
board whose one sensor must face the
world, placed at the board's edge on
purpose (chapter 8).

## An adapter the shop doesn't sell

**The problem:** a part you own exists
only in a surface-mount package; your
bench, your eyes and your other boards
are through-hole.

**The board:** the surface-mount
footprint in the middle (from the
*Package_SO* libraries), its pins fanned
out to two rows of header pins at
breadboard spacing. No schematic
subtlety at all — the whole project is
footprint, placement and routing.

**Teaches:** that KiCad projects needn't
contain a chip or a single active part
to be worth manufacturing, fan-out
routing on two layers, and how much of
real board design is mechanical: spacings,
hole sizes, and whether the result plugs
into the thing it was meant to plug into.
