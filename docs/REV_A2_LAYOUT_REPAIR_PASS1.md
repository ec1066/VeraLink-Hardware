# VeraLink Rev A2 PCB Layout Repair Pass 1

## Scope
This pass makes a controlled KiCad text-level PCB edit. It does **not** represent final fabrication approval. Open the board in KiCad and run DRC before continuing.

## Changes made
- Replaced the partial/failed Y2 32.768 kHz crystal routing.
- Added separate F.Cu routes for:
  - U3 XL1/P0.00 to Y2 pad 2 and C17 signal pad.
  - U3 XL2/P0.01 to Y2 pad 1 and C18 signal pad.
- Used 0.15 mm routing for these low-speed crystal nets to reduce congestion.

## Notes for review
- The Y2 routing is intentionally treated as less critical than the 32 MHz Y1 routing, but it should still be short, clean, and free of DRC violations.
- C17 and C18 ground-side pads are left for the later ground strategy / copper-pour pass.
- This project PCB currently appears to be configured with only F.Cu and B.Cu copper layers in the `.kicad_pcb` file. VeraLink Rev A2 design intent is a 4-layer PCB, so the layer stack must be corrected/confirmed in KiCad before final routing/manufacturing.

## Required user validation
1. Open `hardware/RevA2/VeraLink_RevA2.kicad_pcb` in KiCad.
2. Inspect the Y2/C17/C18 area visually.
3. Run PCB DRC.
4. Report any violations before continuing with routing.
