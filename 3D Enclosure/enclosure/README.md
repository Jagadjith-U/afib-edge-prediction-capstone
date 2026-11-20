# Rev B carrier 3D reference and enclosure handoff

This folder supplies the actual carrier geometry for designing the prototype
case. It is **not** a finished case model or a set of printable case parts.

## Files

- `cad/carrier_assembly_without_daughterboards.step`: populated carrier datum
  without the MAX30003 and BO-10186 daughterboard bodies.
- `cad/bare_board.step`: board-only mechanical fit and standoff reference.
- `cad/carrier_outline_nominal.step`: nominal board outline.
- `cad/afib_carrier-Edge_Cuts.dxf`: 2D board perimeter.
- `mechanical_design_parameters.csv`: verified board and component coordinates
  plus explicitly provisional module and enclosure values.
- `fit_checklist.md`: measurement and prototype fit sequence.
- `AFIB_Carrier_RevB_3D_Modelling_Handoff.pdf`: full drawing explanation.
- `visuals/`: carrier isometric and mechanical/vertical-clearance diagrams;
  these are reference visuals, not photographs of a final printed case.

Import the assembly STEP in millimetres. Use the handoff and CSV to preserve
the four board mounts, microSD access, button positions, left ECG cable exit,
switch travel and ESP32 antenna clearance. Check actual fitted module, battery,
and charger sizes before freezing case dimensions. See `../../docs/APP_AND_ENCLOSURE.md`.

`case/` is reserved for the final editable CAD, STEP/STL, drawing, and fit
photographs after the real enclosure files are supplied and measured.
