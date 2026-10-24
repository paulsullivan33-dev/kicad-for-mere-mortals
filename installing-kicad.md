# Installing KiCad

KiCad is one download containing the
whole suite: the project manager, both
editors, the libraries and `kicad-cli`.
This chapter covers getting it onto
Windows, Mac and Linux, and then verifying
the install in a way that takes one
minute and saves several.

## Windows and Mac

Download the installer for your system
from the KiCad website's download page
and run it. Two things worth knowing:

- **Take the libraries.** The installer
  offers the symbol, footprint and 3D
  libraries as components. Accept them
  all unless disk space is genuinely
  short — a KiCad without its footprint
  library is a word processor without a
  dictionary, and chapter 7 leans on
  those libraries constantly. The 3D
  library is the largest and the only
  one this guide treats as optional
  (chapters 3 and 12 explain why).
- **Version numbers are years, roughly.**
  KiCad releases one major version about
  once a year (7 in 2023, 8 in 2024, and
  so on). Files from a newer major
  version open in that version and later,
  not in older ones — a fact to remember
  when sharing projects with a friend on
  last year's KiCad.

## Linux

On Ubuntu, install KiCad the way the
project itself recommends on its
download page — from KiCad's own stable
repository (a PPA), which carries the
current release:

```bash
sudo add-apt-repository ppa:kicad/kicad-8.0-releases
sudo apt update
sudo apt install kicad
```

Other distributions package KiCad too
(`sudo dnf install kicad` on Fedora,
and so on). One honest caveat about
distribution packages: they can lag a
full release behind, and the gap matters
to this guide in exactly one place. The
terminal checks in chapters 6 and 9 run
through `kicad-cli`, whose `erc` and
`drc` subcommands arrived in KiCad 8 —
Ubuntu 24.04's distribution package is
7.0.11, whose `kicad-cli` can export but
cannot check. The GUI's own ERC and DRC
(under **Inspect**) work in every
version, so a distribution install is
still a perfectly good way to learn the
craft; just run those two checks in the
GUI. The lab behind this guide ran the
PPA build, 8.0.9 on Ubuntu 24.04, and
every command in the guide was tested
against it (see the verification notes
in `criteria.md`).

## Verify the install

Open KiCad once, so it creates its
configuration, then — the one-minute
check that proves the half of KiCad this
guide automates — ask the command-line
tool who it is:

```bash
kicad-cli --version
```

Check: it prints a version and exits
quietly. On Windows the tool lives in the
install folder's `bin` directory (the
installer offers to add it to the path;
if it didn't, the full path works the
same).

Then open the project manager, create a
throwaway project, and place one symbol
in its schematic. If the symbol chooser
offers thousands of parts, the libraries
are in. That, plus the version line, is
a working install.

## First-run choices worth making

- **The library prompt.** A fresh KiCad
  asks whether to copy the default global
  library tables. Say yes: that is the
  step that wires the installed libraries
  into every new project.
- **Nothing else.** Themes, hotkey sets
  and update checks can all wait. In
  particular, let the update checker
  be: mid-project is no time to change
  major versions, and KiCad will not
  force you.

Disk space, honestly: a full install
with all libraries is a few gigabytes,
most of it the 3D models. On a small
machine, install everything except the
3D packages and lose nothing this guide
does electrically.
