# Drawing the Schematic

The schematic is the design's argument:
this part, connected to that part, for this
reason. This chapter draws Blinker's
argument in the schematic editor. It is
written as a guided tour rather than a key
list — the editor's own **Help** menu and
the cheat sheet under **Help → Keyboard
Shortcuts** cover every key; what follows
is the order of work and the ideas behind
it.

## Place the parts first

Open the schematic editor from the project
manager. Add symbols with **Place →
Symbol** (or the **A** key), and search by
name or description:

- `NE555` — in the *Timer* library. KiCad
  ships several 555 variants; pick
  `NE555P` — the P is the through-hole DIP
  version Blinker is built around (the D
  variant is the surface-mount one).
- `R` and `C` — the generic resistor and
  capacitor symbols, in the *Device*
  library. Generic symbols are the norm for
  passives: the symbol says "a resistor",
  and the value and footprint, added later,
  say which one.
- `LED` — also in *Device*.
- `Conn_01x02_Pin` — a two-pin connector,
  in the *Connector* library, for the
  battery.
- `+9V` and `GND` — power symbols, placed
  with **Place → Power Symbol**. Power
  symbols are not decoration: a `+9V`
  anywhere on the sheet is the same
  electrical net as every other `+9V`, and
  `GND` likewise. They are how a schematic
  stays readable instead of becoming a
  plate of spaghetti.

Rotate with **R**, move with **M**, and
lay the parts out roughly the way the
signal flows: battery at the left, the
555 in the middle, the LED at the right.
A schematic you can read is a schematic
you can debug.

## Fill in the values

Select each part and press **E** to edit
its properties. The value field is what a
human reads — `10k`, `47u`, `330` — and
what the bill of materials (chapter 11)
will list. Values are text; the schematic
does not calculate with them. `10k` and
`10000` are the same to KiCad and
different to the person ordering parts at
midnight, so write values the way people
write them.

## Wire it up

Draw wires with **Place → Wire** (**W**),
clicking from pin to pin. The connections
Blinker needs, in words first so the
drawing has something to be checked
against:

- J1 pin 1 (battery +) to the `+9V` net;
  J1 pin 2 to `GND`.
- 555 pin 8 (VCC) and pin 4 (RESET) to
  `+9V`; pin 1 (GND) to `GND`.
- Pin 7 (DISCH) to the top of R1; R1's
  other end to `+9V`.
- Pin 6 (THRES) and pin 2 (TRIG) joined,
  to the bottom of R2 and the top of C1;
  R2's top joins pin 7's net; C1's bottom
  to `GND`.
- Pin 5 (CONT) to C2, C2 to `GND`.
- Pin 3 (OUT) to R3, R3 to the LED's
  anode; the LED's cathode to `GND`.

Two habits make wiring painless:

- **A junction dot means connected.**
  Where wires cross without a dot, they
  pass without touching. If you meant them
  to join, drag one wire's end onto the
  other until the dot appears.
- **Name nets that matter.** Beyond the
  power symbols, **Place → Label** names a
  net — the joined pin 2/pin 6 pair is
  worth calling `TRIG_THRES`, say. Every
  wire carrying that label is the same net,
  even across the sheet. On a board this
  size labels are a courtesy; on a big one
  they are a lifeline.

## Annotate

**Tools → Annotate Schematic** numbers
every part uniquely — the two resistors
become R1 and R2 instead of both asking
`R?`. Run it before doing anything else
with the design: references are how the
schematic, the board, and the parts list
refer to the same physical part, and both
checkers speak in references. Annotating
is safe to re-run; KiCad only numbers the
parts that still have `?`s.

Check: no reference on the sheet still
ends in `?`, and every part has a value.
The drawing is now a claim that ERC can
test, which is chapter 6.
