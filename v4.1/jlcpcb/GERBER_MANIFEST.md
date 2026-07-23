# Moody v4.1 Gerber package

Status: **GENERATED - NOT RELEASED FOR PRODUCTION**

- Archive: `moody-v4.1_GERBERS.zip`
- SHA-256: `7da54cb49fbd92bff581fd25d352b93a4640cbd47d3f23ccc4d6aed05f925baf`
- Source board: `../v4.0.10c_SK6812.kicad_pcb`
- Source project commit: `23c461f`
- Generated: 2026-07-23
- Generator: KiCad CLI 10.0.0
- Stackup: 2 copper layers, 1.6 mm FR-4
- Board size reported by Gerber job: 18.9 mm x 43.8027 mm
- Drills: 26 plated and 14 non-plated holes

The upload archive contains:

- Front and back copper
- Front and back solder mask
- Front and back silkscreen
- Board outline
- Separate plated and non-plated Excellon drill files
- Gerber job file

Archive integrity, Gerber headers/terminators, drill headers/terminators, and
Gerber job references were validated after generation.

## Release blockers

A fresh DRC on the source board found 86 violations: 2 errors and 84 warnings.
The two errors are:

1. A hard short between `/B-` and `/esp-gnd` at U5 pad 2.
2. A front solder-mask bridge between items on those different nets.

Do not submit this package for production until those errors and the other
release blockers in `PRE_PRODUCTION_NOTES.md` have been resolved or formally
accepted.
