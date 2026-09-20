# PCB V3

The earlier Micro-USB board was marked V2. This USB-C revision is V3; its
silkscreen, PCB/schematic revision fields and manufacturing files use revision 3.

This revision addresses review items 1–3, replaces Micro-USB with USB-C,
improves USB routing, and simplifies the LED circuit. The board outline and
header pinout are unchanged. U2 moves to accommodate the larger connector,
and D3/R7 move beside the programming header. The RX/TX indicator branches
are removed. See the [USB-C notes](usb-c.md) for the current connector and
the [USB routing comparison](usb-routing/README.md) for historical Micro-USB views.

## Header labels

Each J2 label is placed at the corresponding pad's Y coordinate, at 2.54 mm pitch.
The power pin is marked `3V3` rather than `VCC`. RX and TX are named from the
programmer's perspective.

| J2 pin | Label | Connection |
| --- | --- | --- |
| 1 (square pad) | GND | Ground |
| 2 | RX | Programmer RX; connect to target TX |
| 3 | TX | Programmer TX; connect to target RX |
| 4 | IO0 | Target boot strap |
| 5 | EN | Target enable/reset |
| 6 | 3V3 | Programmer 3.3 V output |

## Board edge

The project now enforces 0.3 mm copper-to-board-edge clearance. The bottom ground
bridge was moved from Y=60.6 mm to Y=60.4 mm, giving its 0.5 mm tracks 0.35 mm
clearance to the Y=61 mm outline. All zones were refilled with the new rule;
the ground fill is inset approximately 0.3005 mm from the outline.

## Regulator and output capacitor

U1 is **Texas Instruments TLV1117LV33DCYR**, LCSC/JLCPCB **C15578**. Its pinout
matches the existing SOT-223 footprint: pin 1 GND, pin 2 and tab OUT, pin 3 IN.
A project-local symbol records the exact part without relying on an AMS1117
symbol name.

C2 remains the existing 22 µF ceramic capacitor. The
[TI datasheet, section 8.2.2.1](https://www.ti.com/lit/ds/symlink/tlv1117lv.pdf)
specifies ceramic-capacitor stability with zero minimum ESR, recommends at least
1 µF nominal, and requires more than 0.5 µF effective capacitance after bias,
temperature and aging. Preserve that requirement when substituting C2.
Do not substitute an ordinary AMS1117 or TLV1117 for the specified **LV** part.

The replacement is for nominal 5 V USB input: recommended maximum input is 5.5 V
(6 V absolute maximum). This change does not establish a continuous output-current
rating or add reverse-current blocking. Disconnect J2 pin 6 when using an
independently powered target.

## Power indicator

The RX/TX activity LEDs D1/D2, their 2N7002 drivers Q3/Q4, and resistors R3–R6
are removed from the schematic, PCB, BOMs and placement files. Their UART and
supply branch traces are removed as well. The former idle-on LED erratum no
longer applies. Programming and UART connections remain intact.

D3 is the sole remaining LED. It moves to (111.20, 55.62) mm, beside J2's 3V3
label, with a `PWR` silkscreen label. Its 1 kΩ resistor R7 moves to
(107.50, 55.62) mm. Both rotate to 180 degrees; D3's cathode is on the right.
The circuit remains +3V3 → R7 → D3 → GND, so it indicates the presence of the
3.3 V rail rather than UART activity. Existing references are retained for
traceability. The 3.3 V trace to J2 is rerouted below the indicator, and copper
zones are refilled. All other component positions and orientations remain as
they were immediately before this LED change.

## Manufacturing and validation

Both `production/ESPFLASHER.zip` and `jlcpcb/gerber/GERBER-ESPFLASHER.zip` contain
the same regenerated V3 copper, solder mask, paste, silkscreen, outline and drill
files. Both BOMs are regenerated from the current schematic's JLCPCB fields,
including the sourcing updates already present in the schematic before these changes.
The backup archive under `production/backups/` remains historical.

The final USB-C J1 position is (83.18, 50.00) mm at -90 degrees in KiCad,
with U2 at (90.525, 50.80) mm. R8 is at (86.50, 43.50) mm / 0 degrees and
R9 is at (86.50, 56.25) mm / 180 degrees. Both position files include these
changes and the D3/R7 moves; the eight removed indicator components are
omitted. Other existing assembly rotation adjustments are retained. The U1
value in the JLCPCB position file is updated. Confirm J1's mating direction,
pin 1 of U1/U2 and D3's cathode in the assembler's placement preview.

KiCad 9.0.3 validation: no unrouted pads, no schematic/PCB parity issues, no
copper-edge violations, and no ERC electrical errors. After the USB-C change,
DRC reports seven footprint-library warnings and zero errors; ERC reports
27 library warnings and zero errors. The old Micro-USB footprint-type error
is gone. J1's library warning reflects silkscreen lines shortened at the board
edge; its library pad geometry is retained. The other footprint warnings
predate this change.

The USB-C conversion was checked for independent 5.1k CC resistors, both
orientations' D+/D− connections, all VBUS/GND contacts, and unused SBU pins.
Compared with the design just before conversion, R8/R9 are the only added
components, all components other than J1 retain their pad-net assignments,
and only J1/U2 change placement. The schematic PDF and board previews were
inspected. This is design-rule validation, not USB compliance certification.

This revision has not been bench-tested. Check the 3.3 V rail during startup and
load steps, regulator temperature at the intended load, USB enumeration and
repeated flashing with both USB-C plug orientations and with USB-A-to-C and
USB-C-to-C data cables before treating the revised board as hardware-validated.
