# Your First Project

This chapter makes an empty project and
says what everything in it is, so the
next chapters can get on with drawing.
The example project used throughout the
guide is **Blinker**: a small board that
flashes one LED about once a second, built
around the 555 timer chip, running from a
9-volt battery. It is the traditional first
board because it has a handful of parts, no
software, and an instantly visible answer
to "does it work?".

## Make the project

In the project manager:

1. **File → New Project**, choose a folder
   you can find again, and name it
   `blinker`.
2. Leave "create a new folder" ticked, so
   the project gets a folder of its own.

KiCad writes a small set of files into
that folder: the project file
(`blinker.kicad_pro`), an empty schematic
(`blinker.kicad_sch`) and an empty board
(`blinker.kicad_pcb`). Everything you do
from here edits one of those three.

Check: the project manager's file list
shows all three names. If it shows only
the project file, the editors have not
been opened yet — the two drawings are
created the first time you open them.

## A word about saving

KiCad does not autosave your drawings the
way a web app does. **Ctrl+S** in each
editor, often, is the habit that separates
a relaxing evening from a retold one. The
editors do keep backups — the project's
`-backups` folder holds zipped copies —
but needing them is a bad day, not a
workflow.

## The sample circuit

So the later chapters can point at real
parts, here is everything Blinker contains:

| Ref | Part | Job |
|---|---|---|
| U1 | NE555 timer chip | The oscillator — decides the flash rate |
| R1 | 10 kΩ resistor | Half of the timing pair |
| R2 | 10 kΩ resistor | The other half |
| R3 | 330 Ω resistor | Limits the LED's current |
| C1 | 47 µF electrolytic capacitor | With R1 and R2, sets the timing |
| C2 | 10 nF ceramic capacitor | Keeps the 555's control pin quiet |
| D1 | Red LED, 5 mm | The point of the exercise |
| J1 | 2-pin screw terminal | Where the 9 V battery connects |

Nine parts, eight distinct jobs, one chip.
Chapter 5 draws them; chapters 7 and 8 put
them on a board about the size of a matchbox.

## What "done" looks like

A finished project in this guide means:

- the schematic drawn and annotated
  (every part has a unique reference —
  R1, not two parts both called R),
- ERC passing with no unexplained errors
  (chapter 6),
- footprints assigned to every part,
- the board laid out, routed, and passing
  DRC (chapter 9),
- and the manufacturing files exported
  (chapter 11).

Nothing about that list requires the board
to be clever. It requires the board to be
*checked*, which is the whole habit this
guide is teaching.
