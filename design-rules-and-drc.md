# Design Rules and DRC

Where ERC guards the schematic's meaning,
DRC — the design rules check — guards the
board's *manufacturability*: can a factory
actually make this, and is everything
connected that the schematic says is?
This chapter explains where the rules
live, which of them matter at this scale,
and how to reach a clean DRC honestly.

## Where the rules live

**File → Board Setup** holds the board's
own constitution:

- **Design Rules → Constraints** — the
  floor values nothing may break: minimum
  clearances, track widths, via sizes.
- **Design Rules → Net Classes** — rules
  per *kind* of net. A net class is a
  named bundle (clearance, track width,
  via size) that nets belong to. Every
  board starts with one class, `Default`.
  Blinker's one refinement is a second
  class, `Power`, with a wider track
  width, holding the `+9V` and `GND` nets
  — wider copper for the nets that carry
  the whole circuit's current.
- **Layers and stackup** — how many copper
  layers, and what the fab house makes
  them from. Two layers is the standard
  choice this guide assumes throughout.

The values KiCad starts with suit typical
low-cost fabrication comfortably. The
honest rule for beginners is to leave the
minimums alone — they encode what cheap,
fast board houses can reliably build —
and to make your *own* rules stricter,
never looser, when in doubt. A track
drawn at 0.3 mm on a board whose rules
allow 0.15 mm is not clever; it is a
board that costs the same and works
harder to fail.

## Run DRC, read DRC

**Inspect → Design Rules Checker**, then
**Run DRC**. Two families of complaint
arrive:

| Family | Example | Meaning |
|---|---|---|
| **Clearances** | Track too close to a pad | Two pieces of copper that must not touch nearly do — or a zone fill kept a polite distance *from your own track* |
| **Unconnected items** | Two pads listed by net and reference | The schematic says these join; the copper doesn't, yet |

Unconnected items are the ratsnest in
report form: count them to know how much
routing is left. Clearances are geometry:
click the complaint and KiCad shows the
two offenders. Fixes are moved tracks,
moved *parts* (the honest fix more often
than beginners expect), or a via to the
other layer.

The command line runs the same check,
which is how scripts — and this guide's
lab — ask the question:

```bash
kicad-cli pcb drc blinker.kicad_pcb \
  --output drc-report.txt
```

Check: the report's violation count is
zero, and its unconnected count is zero.

## Clean, not quiet

Like ERC, DRC lets you mark individual
complaints as exclusions and move on.
Used properly, exclusions are how a
designer records "I have looked at this
specific overlap and it is deliberate" —
a mounting hole's clearance ring over a
zone, say. Used badly, they are how bad
boards get shipped with paperwork. The
rule from chapter 6 applies unchanged:
zero is the goal, and every exception
must be explainable out loud to a person
who was not you at midnight.

One class of DRC output deserves a
warning of its own: **courtyard overlaps**
and silkscreen complaints are about
whether parts physically fit and labels
stay readable. Beginners often silence
them because the board "still works".
It works on the bench; whether two
parts' bodies collide is exactly the
class of thing you cannot see in plan
view, and the 3D viewer (chapter 8) is
the tiebreaker.

## Rules are the fab house's, too

When you graduate to tighter boards, the
direction reverses: serious fab houses
publish *their* minimums, and Board
Setup is where those numbers go, so DRC
checks your design against the factory
that will build it rather than against
defaults. At Blinker scale the defaults
and the factories agree, which is one
more reason a small, checked board is
the right first board.
