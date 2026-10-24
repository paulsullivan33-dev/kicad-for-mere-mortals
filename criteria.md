# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Built and verified 2026-10-24 against
**KiCad 8.0.9** (the 8.0 release branch's
current build on build day), from the
project's own stable PPA for Ubuntu 24.04
— the install route chapter 3 recommends.

**Primary sources read, not remembered:**
the installed 8.0.9 symbol and footprint
libraries themselves (the NE555P pinout,
every footprint name in chapter 7 and the
connector's library all come from the
files on disk, not from memory), the
`kicad-cli` help text of the installed
binary (which is how the guide knows what
7.0's CLI lacks), and the reports ERC and
DRC produced in the lab.

**Ran for real** (transcripts in
`kicad-lab/transcripts/`; the finished
project is `kicad-lab/blinker/`): because
the lab machine is headless, the sample
board was authored as files — a schematic
written in KiCad's own format with the
genuine library symbols embedded, and a
board built by a `pcbnew` script loading
the genuine footprints — and then checked
by the same tools a reader uses:

- t00 — `kicad-cli --version` → 8.0.9.
- t01 — ERC on the finished schematic:
  0 errors, 0 warnings.
- t02 — the exported netlist, read net by
  net against the intended circuit: all
  seven nets (+9V, GND, TIMING, DIS, CV,
  OUT, LED_A) carry exactly the pins the
  design says they should.
- t03 — the BOM export: the eight parts
  of chapter 4's table, each with its
  chapter 7 footprint.
- t04 — DRC on the finished board:
  0 violations, 0 unconnected pads,
  0 footprint errors.
- t05 — manufacturing exports: the full
  Gerber set with its job file, the
  Excellon drill file (two tools —
  0.4 mm vias, 0.8 mm component holes),
  and the position file.

**Errors hit and diagnosed for real,**
written into the chapters and the lab
notes: the first ERC run's 68 findings —
47 off-grid endpoints from a layout not
drawn on the 1.27 mm connection grid, 19
warnings for library tables the sandbox
account lacked, and one real error, the
555's discharge pin unconnected because
its wire ended on the *middle* of another
wire with no junction (the fix in chapter
6 is the fix the lab used). The first
DRC runs reported chapter 9's catalogue
in miniature: two pairs of crossing
tracks, a ground branch shorting a
capacitor pad it passed on its way to
the right one, and a via drilled 0.18 mm
from a chip pin's hole against a
0.2495 mm minimum. Each was re-routed
and re-checked; only the clean reports
are kept as transcripts.

**Documented only, and labelled as such
in the chapters:** everything done by
clicking in the two editors (menus and
keys are described, and the lab drove
the same operations through the file
formats and the CLI instead); filling
the ground zone, which is a GUI act —
KiCad 8.0's zone filler crashes in the
standalone scripting module, with or
without a virtual display, so the lab
board also routes ground as tracks under
the zone and says so in the lab notes;
placing a real order with a fabrication
house (the files a fab consumes were
generated and inspected; no order was
sent and no board was made); the 3D
viewer and its model library, which the
lab did not install; and circuit
simulation, which chapter 1 places
honestly at the tool's edge (ngspice
hooks, not a taught workflow). One environmental
note: the build VM's system package
state was busy with another job, so the
lab unpacked the genuine PPA and Ubuntu
packages into a private directory and
ran them from there — the binaries and
libraries under test are the
distribution's own; only their location
is unusual.

## How to use this guide

Read chapters 1 and 2 before installing
anything — knowing which file holds what
turns later confusion into a named
problem. Build Blinker alongside chapters
4 to 11 rather than reading them in the
abstract: every chapter ends with a check
that passes on the sample board, and the
lab's copy of that board, with its clean
ERC and DRC reports, lives in
`kicad-lab/` if you want to compare. The
lab's transcripts live in
`kicad-lab/transcripts/`; its notes are
`examples/lab-notes.txt`.
