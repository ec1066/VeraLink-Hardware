\# VeraLink Rev A2.1 MCU Module Decision



\## Revision History



| Revision | Date | Description |

|---|---|---|

| A2.1 Draft | 2026-10-09 | Decision to replace bare nRF52840-QIAA with nRF52840 module |



\## Decision



VeraLink Rev A2.1 will replace the bare nRF52840-QIAA aQFN73 MCU with an nRF52840 module.



The preferred module candidate is:



\- u-blox NINA-B306



The backup module candidate is:



\- Raytac MDBT50Q series



\## Reason for Change



The previous Rev A2 design used the nRF52840-QIAA aQFN73 package. During PCB routing, it became clear that several inner/back-row MCU pads could not be escaped using the intended manufacturable prototype design rules.



Continuing with the QIAA package would require advanced PCB techniques such as microvias, via-in-pad, tighter trace/space rules, or major pin reassignment. This does not align with VeraLink’s priority order:



1\. Reliability

2\. Safety

3\. Manufacturability

4\. Simplicity

5\. Cost

6\. Battery life

7\. User experience



\## Accepted Tradeoffs



Moving to an nRF52840 module will likely increase module cost and PCB area, but it reduces:



\- MCU package breakout risk

\- BLE RF layout risk

\- crystal layout risk

\- antenna tuning risk

\- assembly risk

\- prototype failure risk

\- certification complexity



The Rev A2.1 prototype will prioritize a fully functional manufacturable device over AirTag accessory size compatibility.



\## Primary Candidate: u-blox NINA-B306



Rationale:



\- nRF52840 based

\- Integrated PCB antenna

\- Industrial module vendor

\- Strong documentation and certification support

\- Sufficient GPIO count for VeraLink

\- ADC-capable pins available for battery sensing

\- Supports BLE/FOTA use case

\- Avoids unnecessary GPIO overkill while retaining margin



\## Backup Candidate: Raytac MDBT50Q Series



Rationale:



\- nRF52840 based

\- Higher GPIO margin

\- Multiple antenna variants

\- Potentially lower module cost in some quantities

\- Suitable backup if NINA-B306 pin map, availability, footprint, or antenna keepout is not acceptable



\## Rev A2.1 Design Direction



Remove from VeraLink PCB:



\- nRF52840-QIAA footprint

\- nRF52840 external 32 MHz crystal circuit

\- nRF52840 external 32.768 kHz crystal circuit if included in selected module

\- BLE RF matching network

\- BLE antenna path if module has integrated antenna

\- nRF52840 local decoupling network no longer required outside module



Retain:



\- SX1262 / E22 LoRa module

\- MCP73831 charger

\- TPS78233 3.3 V regulator unless power review changes this

\- DRV2605L haptic driver

\- RGB LED

\- user button

\- passive piezo

\- magnetic pogo charging

\- battery

\- factory SWD/test pads



\## Next Engineering Steps



1\. Perform VeraLink Rev A2.1 NINA-B306 pin map.

2\. Confirm NINA-B306 exposes enough usable GPIO and ADC pins.

3\. Confirm power requirements and regulator compatibility.

4\. Confirm SWD programming access.

5\. Confirm antenna keepout requirements.

6\. Confirm KiCad symbol/footprint availability or create custom library parts.

7\. Update schematic.

8\. Replace U3 bare MCU circuit with selected module.

9\. Restart PCB layout using module-based architecture.



\## Status



Approved for Rev A2.1 architecture development.

