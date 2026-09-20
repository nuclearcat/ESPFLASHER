# USB-C connector model

`HRO_TYPE-C-31-M-12.step` is the HRO TYPE-C-31-M-12 model from
[Keebio-Parts.pretty](https://github.com/keebio/Keebio-Parts.pretty/blob/1486bef23f020c31bf69123c93da199850cc7243/3dmodels/HRO%20%20TYPE-C-31-M-12.step),
copied without modifying its contents. The STEP header credits `ryotagoto`.
The upstream repository's MIT license is included in `LICENSE.keebio`.

J1 references `${KIPRJMOD}/3dmodels/HRO_TYPE-C-31-M-12.step`, so the model
travels with the project and does not require a system library installation.
KiCad model settings:

| Setting | X | Y | Z |
| --- | ---: | ---: | ---: |
| Scale | 1 | 1 | 1 |
| Rotation (degrees) | -90 | 0 | 0 |
| Offset (mm) | -4.47 | -3.65 | 0 |

The rotation and Y/Z offsets follow the upstream assembly footprint, which
uses the same shell mounting-hole coordinates as J1. The X offset centers the
model's 8.94 mm width precisely (upstream uses -4.45 mm). Its shell leg centers
then match the footprint's X = ±4.32 mm mounting slots. The body rests at the
PCB top surface and its opening faces the left board edge. Placement was
checked in KiCad top and oblique renders; the model is for visualization,
with the manufacturer drawing remaining the assembly reference.
