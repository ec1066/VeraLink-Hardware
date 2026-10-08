# VeraLink Rev A2 Layout Repair Pass 2

## Purpose
This pass removes the attempted Y2 / 32.768 kHz crystal routing from Pass 1.

## Reason
KiCad DRC showed that the attempted F.Cu routing for `Net-(U3-XL1/P0.00)` and
`Net-(U3-XL2/P0.01)` shorted into nearby U3 pads and violated the board minimum
track width rule. The board minimum track width is 0.200 mm, so the previous
0.150 mm routing was not acceptable under the current board rules.

## Change Made
Removed all existing track segments for:

- `Net-(U3-XL1/P0.00)`
- `Net-(U3-XL2/P0.01)`

This intentionally leaves Y2/C17/C18 unconnected so the PCB returns to a DRC-clean
routing baseline, apart from expected unconnected items.

## Engineering Decision
Do not force the Y2 crystal routes through the existing gap. The current spacing
around U3, Y2, C17, and C18 is not sufficient for two legal 0.200 mm traces on
F.Cu without collisions.

Recommended next design action:

1. Move Y2 and its load capacitors to a cleaner escape location, or
2. Convert the board setup to the approved 4-layer Rev A2 stackup and evaluate a controlled via-assisted escape, or
3. Revisit whether the 32.768 kHz crystal is required for Rev A2 prototype bring-up.

Do not route these nets again until the placement decision is made.
