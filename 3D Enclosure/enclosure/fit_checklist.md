# AFIB Carrier Rev B enclosure fit checklist

## Before finalising the CAD

- Import `carrier_assembly_without_daughterboards.step` in millimetres.
- Confirm the STEP axes: X right, Y upward in CAD, Z upward. Drawing Y values
  therefore become negative STEP Y values.
- Check the four 3.2 mm NPTH mounting holes at 82 x 72 mm spacing.
- Keep all standoffs, inserts, screws, battery material and cable loops out of
  the ESP32 antenna clearance zone.
- Keep the module-specific openings parametric until the physical parts arrive.

## Measurements to collect with calipers

- MAX30003 board length, width and total fitted height.
- Position and diameter of the MAX30003 3.5 mm ECG jack.
- Required bend radius and strain-relief length for the ECG cable.
- BO-10186 overall fitted height and pin orientation.
- Exact 1-cell LiPo length, width, thickness and lead exit position.
- Exact TP4056 module dimensions, USB connector type and connector position.
- Final tactile-button actuator diameter and travel.
- Final power-switch slider position and travel.

## Test-print sequence

1. Print a 2 mm thick hole-and-port gauge containing the four buttons,
   microSD opening, power-switch slot and ECG cable opening.
2. Check the gauge against the populated PCB before printing the complete lid.
3. Print the base and confirm all four screws enter freely without bending the
   PCB.
4. Confirm at least 4 mm clearance below the PCB and no sharp edges near the
   battery.
5. Install the modules and cables, then verify there is no lid contact or cable
   preload.
6. Test microSD insertion and removal without opening the case.
7. Test all four buttons and the power switch through their final actuators.
8. Run a BLE range test with the final case, battery and wiring installed.
9. Perform body-connected tests only on battery power with charging and all
   mains-referenced programming or measurement equipment disconnected.

## Deliverables from the mechanical designer

- Editable parametric CAD source.
- STEP and STL for the base, lid, buttons and any removable port inserts.
- An assembly STEP showing the carrier, modules, battery and charger.
- A dimensioned drawing with wall thickness, clearances, screw specification
  and overall size.
- An exploded view and short assembly order.
- A one-page record of the physical measurements used to replace provisional
  envelopes.
