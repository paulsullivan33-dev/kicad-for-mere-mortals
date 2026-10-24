# Checking the Schematic

ERC — the electrical rules check — reads
your schematic the way a careful colleague
would: not "is this a good circuit?" but
"is this the circuit you think you drew?"
Run it early and often. A schematic that
passes ERC can still be wrong, but a
schematic that fails it is *definitely*
not what you meant.

## Run it

**Inspect → Electrical Rules Checker**,
then **Run ERC**. Every complaint appears
in the list and as a marker on the sheet;
clicking a complaint takes you to the
scene of the crime. The same check runs
from the command line:

```bash
kicad-cli sch erc blinker.kicad_sch \
  --output erc-report.txt
```

Check: the report ends with a count of
errors and warnings, and — for a finished
schematic — the errors are zero and every
warning is one you can explain.

## The usual suspects

ERC knows about *pin types*: every pin is
declared an input, an output, a power pin,
a passive pin and so on, and the checker
has opinions about which may join which.
Most beginner ERC output is one of these
four:

| Complaint | Usually means | Fix |
|---|---|---|
| Pin not connected | A pin goes nowhere | Wire it, or mark it deliberate with a no-connect flag (**Place → No Connect Flag**) |
| Input pin not driven | An input joins only other inputs — nothing ever tells it what to do | Find the missing wire or the missing output |
| Output and output connected | Two pins that both drive are wired together | One of them is miswired, or a pin's type in the symbol is wrong |
| Power pin not powered | A chip's power pin joins a net nothing supplies | The most misleading message of the four — see below |

## The power flag lesson

The "power pin not powered" error catches
everyone once. The cause: ERC only trusts
that a net is powered if something on it
is declared a *power output* — and a
battery connector's pins are passive, so
a schematic fed by a connector looks, to
ERC, like a circuit fed by nothing.

The fix is a special symbol, `PWR_FLAG`,
from the *power* library: place one on
the `+9V` net and one on `GND`. The flag
promises the checker "a human has thought
about this; power arrives from off-sheet."
It changes nothing electrically. Adding
flags to nets that genuinely are unpowered
would be lying to the checker, so the rule
is: one flag per externally supplied net,
never more.

## Errors, warnings, and honesty

ERC lets you downgrade complaint classes
to warnings or silence them entirely, in
**File → Schematic Setup → Electrical
Rules**. Every working designer has a
short list of classes they treat gently —
and every bad board in history was
designed by someone who silenced the one
that mattered. The discipline this guide
teaches is narrower and safer: fix errors,
and for every warning you keep, be able
to say out loud why it is not a mistake.
If you cannot say why, it is a mistake
you have not found yet.

What ERC cannot see, stated plainly: wrong
values (a 10 Ω where 10 kΩ belongs sails
through), swapped pins of the same type,
or a design that simply will not work.
Chapter 9's DRC has the same relationship
to the board. The checkers guard the
drawing, not the idea.
