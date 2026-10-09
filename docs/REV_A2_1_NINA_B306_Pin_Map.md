\# VeraLink Rev A2.1 NINA-B306 Pin Map



\## Revision History



| Revision | Date | Description |

|---|---|---|

| A2.1 Draft | 2026-10-09 | Initial NINA-B306 pin-map feasibility review |



\## Purpose



This document verifies whether the u-blox NINA-B306 nRF52840 module can support all VeraLink Rev A2.1 electrical functions before schematic redesign.



\## Design Assumptions



\- MCU/BLE module: u-blox NINA-B306

\- LoRa radio remains the E22/SX1262 module

\- VeraLink uses BLE OTA, not USB DFU

\- VeraLink uses regulated SYS\_3V3 power

\- AirTag accessory size constraint is no longer mandatory for Rev A2.1

\- PCB remains 4-layer

\- NINA-B306 integrated PCB antenna keepout must be respected



\## Required VeraLink Signals



| Function Group | Signal | Type | Required? | Notes |

|---|---|---|---|---|

| LoRa SPI | LORA\_SCK | Digital output | Yes | SPI clock |

| LoRa SPI | LORA\_MOSI | Digital output | Yes | SPI MOSI |

| LoRa SPI | LORA\_MISO | Digital input | Yes | SPI MISO |

| LoRa SPI | LORA\_NSS | Digital output | Yes | SPI chip select |

| LoRa Control | LORA\_RESET\_N | Digital output | Yes | LoRa reset |

| LoRa Control | LORA\_BUSY | Digital input | Yes | LoRa busy |

| LoRa Interrupt | LORA\_DIO1 | Digital input/interrupt | Yes | SX1262 IRQ |

| LoRa Control | LORA\_DIO2 | Digital input/output | Preferred | Needed depending radio configuration |

| LoRa RF Switch | LORA\_TXEN | Digital output | If module requires | TX enable |

| LoRa RF Switch | LORA\_RXEN | Digital output | If module requires | RX enable |

| Haptic | I2C\_SCL | Digital open-drain | Yes | DRV2605L |

| Haptic | I2C\_SDA | Digital open-drain | Yes | DRV2605L |

| Haptic | HAPTIC\_TRIG | Digital output | Preferred | Optional trigger pin |

| User Input | BUTTON\_N | Digital input | Yes | User button |

| LED | LED\_R\_N | PWM/GPIO output | Yes | RGB red |

| LED | LED\_G\_N | PWM/GPIO output | Yes | RGB green |

| LED | LED\_B\_N | PWM/GPIO output | Yes | RGB blue |

| Audio | PIEZO\_PWM | PWM/GPIO output | Yes | Passive piezo |

| Charging | CHG\_STAT | Digital input | Yes | MCP73831 status |

| Charging | CHG\_DETECT | Digital input | Yes | Magnetic charger detect |

| Battery | VBAT\_SENSE | ADC input | Yes | Must be ADC-capable |

| Programming | SWDIO | SWD | Yes | Factory programming/debug |

| Programming | SWDCLK | SWD | Yes | Factory programming/debug |

| Optional | NFC1/NFC2 | NFC/GPIO | No | Not required for Rev A2.1 |

| Optional | USB D+/D- | USB | No | Not required if BLE OTA only |



\## Required Pin Count



Approximate required user signal count:



| Category | Count |

|---|---:|

| LoRa SPI/control | 10 |

| I2C haptic | 2 |

| Haptic trigger | 1 |

| RGB LED | 3 |

| Button | 1 |

| Piezo | 1 |

| Charger status/detect | 2 |

| Battery ADC | 1 |

| SWD | 2 |

| Practical spare margin | 2-4 |



Estimated need: 23-27 usable pins.



NINA-B306 provides 38 GPIO and 8 ADC inputs according to u-blox product information. This appears sufficient, pending exact pinout assignment.



\## Preliminary Feasibility Conclusion



NINA-B306 appears feasible for VeraLink Rev A2.1 because it provides:



\- Enough GPIO margin for required signals

\- ADC-capable pins for VBAT\_SENSE

\- SPI, I2C, PWM, and GPIO support through the nRF52840

\- Integrated BLE antenna

\- SWD programming support

\- BLE/FOTA-compatible nRF52840 platform



\## Open Items Before Schematic Update



1\. Confirm exact NINA-B306 pad numbers for all assigned signals.

2\. Confirm SWDIO/SWDCLK pad locations.

3\. Confirm which pins are ADC-capable.

4\. Confirm module antenna keepout.

5\. Confirm whether any pins are reserved by u-blox bootloader or production data.

6\. Confirm whether USB is omitted from VeraLink Rev A2.1.

7\. Confirm whether NFC pins may be reused as GPIO.

8\. Confirm module supply voltage and current requirements.

9\. Confirm KiCad footprint source or create custom footprint.



\## Status



Preliminary feasible. Exact pin assignment required before schematic redesign.





\## Proposed Pin Assignment Draft 0.1



| VeraLink Signal | Proposed NINA-B306 Signal | Function Type | Routing Group | Status |

|---|---|---|---|---|

| LORA\_NSS | GPIO\_16 | Digital output | LoRa/right side | Proposed |

| LORA\_SCK | GPIO\_17 | SPI clock | LoRa/right side | Proposed |

| LORA\_MOSI | GPIO\_18 | SPI MOSI | LoRa/right side | Proposed |

| LORA\_MISO | GPIO\_20 | SPI MISO | LoRa/right side | Proposed |

| LORA\_RESET\_N | GPIO\_21 | Digital output | LoRa/right side | Proposed |

| LORA\_BUSY | GPIO\_22 | Digital input | LoRa/right side | Proposed |

| LORA\_DIO1 | GPIO\_23 | Interrupt input | LoRa/right side | Proposed |

| LORA\_DIO2 | GPIO\_24 | Interrupt/control | LoRa/right side | Proposed |

| LORA\_TXEN | GPIO\_25 | Digital output | LoRa/right side | Proposed |

| LORA\_RXEN | GPIO\_47 | Digital output | LoRa/top side | Proposed |

| I2C\_SCL | GPIO\_4 | I2C clock | Haptic/UI side | Proposed |

| I2C\_SDA | GPIO\_5 | I2C data | Haptic/UI side | Proposed |

| HAPTIC\_TRIG | GPIO\_7 | Digital output | Haptic/UI side | Proposed |

| BUTTON\_N | GPIO\_8 | Digital input | UI side | Proposed |

| LED\_R\_N | GPIO\_1 | PWM/GPIO output | UI side | Proposed |

| LED\_G\_N | GPIO\_2 | PWM/GPIO output | UI side | Proposed |

| LED\_B\_N | GPIO\_3 | PWM/GPIO output | UI side | Proposed |

| PIEZO\_PWM | GPIO\_48 | PWM/GPIO output | UI/audio side | Proposed |

| CHG\_STAT | GPIO\_49 | Digital input | Charger/sense | Proposed |

| CHG\_DETECT | GPIO\_50 | Digital input | Charger/sense | Proposed |

| VBAT\_SENSE | GPIO\_27 or verified ADC-capable GPIO | ADC input | Battery sense | Requires verification |

| SWDIO | SWDIO | Debug/programming | Factory pads | Fixed |

| SWDCLK | SWDCLK | Debug/programming | Factory pads | Fixed |

| RESET\_N | RESET\_N | Hardware reset | Test/reset | Optional |

