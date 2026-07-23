# Moody v4.1 JLCPCB assembly files

Status: **UPLOAD-READY PARTIAL ASSEMBLY - PCB NOT RELEASED**

Generated and catalog-checked on 2026-07-23.

Sources:

- PCB: `../v4.0.10c_SK6812.kicad_pcb`
- Schematic: `../v4.0.10c.kicad_sch`
- KiCad CLI: 10.0.0
- JLCPCB BOM: `moody-v4.1_BOM.csv`
- JLCPCB CPL: `moody-v4.1_CPL.csv`

The two PCB files in `v4.1/` were byte-identical when these files were
generated.

## Factory assembly scope

The BOM and CPL contain exactly the same nine fitted references:

- `C1`, `D1`, `D2`, `J2`, `R1`, `R2`, `R3`, `U2`, `U4`

JLCPCB catalog selections:

| Ref | JLCPCB part | MPN | Selection |
| --- | --- | --- | --- |
| C1 | C49678 | CC0805KRX7R9BB104 | Basic, 0805, 100 nF, 50 V, X7R, +/-10% |
| D1 | C397616 | DSL14 | Extended, SOD-123, 40 V, 1 A Schottky |
| D2 | C52941386 | WS2812B-MINI-V6 | Extended, SMD3535-4P, 3.3 V-compatible addressable RGB LED |
| J2 | C160404 | SM04B-SRSS-TB(LF)(SN) | Extended, JST SH, 4-pin, right-angle |
| R1, R2 | C17414 | 0805W8F1002T5E | Basic, 0805, 10 kOhm, +/-1%, 125 mW |
| R3 | C28636 | 0805W8F5600T5E | Basic, 0805, 560 Ohm, +/-1%, 125 mW |
| U2 | C221530 | OS102011MA1QS1 | Extended, wave soldering, Standard PCBA only |
| U4 | C19189385 | XIAO ESP32C3 | Extended, LCC-14 castellated module |

The capacitor and resistor part numbers replace the earlier low/out-of-stock
selections with footprint-compatible JLCPCB Basic parts.

## Not placed by JLCPCB

- `U3`: left unpopulated. The intended TSIC 206 TO92 is not stocked as a
  JLCPCB/LCSC assembly part. Its physical TO-92 pinout is GND, Signal, VDD,
  while the PCB pad nets are Signal, 3.3 V, GND. An analog sensor family such
  as LMT86 can use the PCB's Signal, VDD, GND pad order, but is not
  protocol-compatible with TSIC/ZACwire firmware and therefore is not a safe
  BOM-only substitution.
- `J1`: breakaway copper-pad connector, not a fitted JST connector.
- `U1`: PCB battery/castellated pads, not a fitted component.
- `U5`: unpopulated two-pin test point.
- `mouse-bite-2mm-slot`: board feature.
- `G***`: logo.

## Release blockers

1. PCB DRC reports a hard short between `/B-` and `/esp-gnd` at `U5` pad 2,
   plus a front solder-mask bridge at the same location.
2. Fresh KiCad ERC reports 5 errors and 31 warnings. Fresh PCB DRC reports 86
   violations: 2 errors and 84 warnings.
3. Schematic parity checking cannot run because the schematic is not fully
   annotated.
4. The schematic source values still name 0402 parts for `C1`, `R1`, `R2`,
   and `R3`, while the PCB uses 0805 footprints. The upload BOM uses
   footprint-compatible 0805 replacements.
5. `D2` still uses the `SK6812` schematic symbol, whose pin numbering does
   not match `C52941386`: the schematic/board currently assigns pad 1 as
   unconnected, pad 2 as GND, pad 3 as `/Licht`, and pad 4 as 3.3 V, while
   `WS2812B-MINI-V6` specifies 1=VDD, 2=DOUT, 3=VSS, and 4=DIN. Resolve this
   mapping and verify D2 orientation in JLCPCB's placement preview before
   production.
6. `U2` requires **Standard PCBA** because JLCPCB classifies `C221530` as a
   wave-soldered, Standard-only part.
7. JLCPCB lists `U4` as an assembly-supported Extended part, but does not show
   public stock on its part page. Confirm availability or pre-order/global
   source `C19189385` during the quote.

## Upload checklist

1. Fix or formally resolve the PCB short and all ERC/DRC errors before
   releasing Gerbers.
2. Select **Standard PCBA** if JLCPCB is to fit `U2`.
3. Upload the BOM and CPL together. Their reference sets are identical.
4. Confirm `C19189385` availability for `U4`.
5. In JLCPCB's placement preview, verify every orientation-sensitive part,
   especially `D1`, `D2`, `J2`, `U2`, and `U4`.
6. Resolve D2's symbol-to-part pin mapping and decide how `U3` will be
   redesigned or fitted manually.
