# USB-C input

J1 is an HRO **TYPE-C-31-M-12**, LCSC/JLCPCB **C165948**, a compact
16-contact USB-C receptacle for USB 2.0. Its shell is approximately
8.94 × 7.35 mm. It replaces the Micro-USB connector on the existing
40 × 21 mm board outline. The CH340C and the 3.3 V regulator are unchanged.

USB-C describes the connector here: the programmer still uses USB 2.0 data
and nominal 5 V VBUS. There are no SuperSpeed signals, USB PD controller,
or higher-voltage negotiation. Avoid substituting a power-only connector
that omits the USB data contacts.

| J1 contacts | Connection |
| --- | --- |
| A4, A9, B4, B9 | VBUS, feeding the existing regulator input |
| A1, A12, B1, B12, shell S1 | GND |
| A6, B6 | D+, through U2 protection to CH340C |
| A7, B7 | D−, through U2 protection to CH340C |
| A5 / CC1 | R8, 5.1 kΩ to GND |
| B5 / CC2 | R9, 5.1 kΩ to GND |
| A8 / SBU1, B8 / SBU2 | Unconnected |

R8/R9 are separate 0603 1% resistors, UNI-ROYAL **0603WAF5101T5E**,
LCSC/JLCPCB **C23186**. The two Rd terminations allow a USB-C source to
detect the sink in either plug orientation. They do not grant an automatic
1.5 A or 3 A current allowance; this revision adds no source-current
detection and does not change the programmer's unvalidated load rating.

The connector's pin order, locating holes and shell mounting slots were
checked against the [manufacturer's drawing hosted by LCSC](https://www.lcsc.com/datasheet/C165948.pdf).
The component is listed in the [JLCPCB assembly library](https://jlcpcb.com/partdetail/TYPE-C-31-M-12/C165948).
See also [TI's USB-C sink reference circuit, Figure 2](https://www.ti.com/lit/ug/tiduem6/tiduem6.pdf)
for separate CC pull-downs and USB 2.0 contact pairing.

J1 is placed with the board edge at the drawing's recommended insertion
depth. U2 moves inward to clear the larger connector. The two copies of
each USB data signal join near J1; the D− crossover is on the connector
side of U2. Both main data routes pass through their protection pads,
then run together toward the CH340C. Ground copper is refilled, and a
short ground connection joins the connector shell to the adjacent ground
via. The board title moves into the space freed by the removed RX/TX LEDs.

The installed KiCad 3D library does not contain this connector's body model;
the rendered preview shows its footprint, rather than a populated connector.
Use the schematic, PCB footprint and manufacturer drawing for assembly review.

KiCad reports no DRC electrical/clearance errors, unconnected pads or
schematic/PCB mismatches. ERC has no electrical errors. Library-comparison
warnings are described in the [revision notes](revision-2.md).

Hardware is not yet tested. Verify USB enumeration and repeated flashing
with a data-capable USB-A-to-C cable and USB-C-to-C cable, with the plug
inserted both ways. Also verify supply startup and the intended target load.
