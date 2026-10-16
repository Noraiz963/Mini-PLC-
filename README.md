# STM32 Mini PLC v1.0

A compact industrial-style PLC board designed in KiCad, built around an STM32F407 microcontroller. It has 8 optically isolated digital inputs, 8 relay outputs, RS-485 communication, and USB-C serial/bootloader access, all powered from 24 VDC.

![3D view](images/3d-render-angle.png)
![3D top view](images/3d-render-top.png)
![PCB layout](images/pcb-layout.png)

## Specifications

| Parameter | Value |
|---|---|
| Microcontroller | STM32F407 |
| Supply input | 24 VDC |
| Digital inputs | 8, optically isolated |
| Relay outputs | 8, rated 250 VAC / 30 VDC, 5 A (per board silkscreen) |
| Communication | RS-485 (DB9 connector), USB-C (UART bridge) |
| Programming | 5-pin SWD header for ST-LINK |
| Design tool | KiCad |
| Board layers | 2 (verify in Board Setup) |

## Sub-systems

| Sub-system | Key components | Description |
|---|---|---|
| Power stage | J1, F1, D1, U1, U2 | Accepts 24 VDC industrial input, protected by a fuse and a reverse-polarity diode. A switching buck converter (U1) and a 3.3 V linear regulator (U2) power the logic. |
| Processing core | U13 (STM32F407), C9–C11 | Main microcontroller for application logic, with decoupling capacitors for stability. |
| Programming and debug (J5) | 3V3, SWDIO, RST, SWCLK, GND | 5-pin header for debugging and flashing with an external ST-LINK. Pin 1 is the 3.3 V reference (VTREF). |
| USB and serial | J19 (USB-C), U14 (CH340C) | USB-to-UART bridge for serial monitoring (printf debugging) and bootloader flashing. |
| Isolated digital inputs | J2, U4–U11 (optocouplers) | 8 optically isolated channels that protect the STM32 from field-side voltage transients. |
| Relay output stage | K2–K9, Q2–Q9 (MOSFETs), D13–D20, J3 | 8 electromechanical relays driven by MOSFET switches, with freewheeling diodes for inductive kickback protection. |
| Industrial communication | U12 (RS-485 transceiver), J4 | Differential serial interface for fieldbus networks. The hardware is suitable for Modbus RTU. |

## Connectors

| Ref | Function | Pins |
|---|---|---|
| J1 | 24 VDC power input | 24 V, 0 V |
| J2 | Digital inputs | X1–X8, GND |
| J3 | Relay outputs | Y1–Y8, plus common terminal (see silkscreen) |
| J4 | RS-485 (DB9) | Differential A/B, GND |
| J5 | SWD programming | 3V3, SWDIO, SWCLK, RST, GND |
| J19 | USB-C | UART bridge and bootloader |

## Repository structure

```
stm32-mini-plc/
├── README.md
├── hardware/        KiCad project (.kicad_pro, .kicad_sch, .kicad_pcb)
├── images/          3D renders and PCB layout
├── docs/            schematic PDF, BOM
└── LICENSE
```

## Status

Hardware design v1.0 is complete. The board has not been manufactured or tested yet, and no firmware has been written. Specifications above come from the design, not from measurements on a built board.

## Tools

KiCad (schematic, PCB layout, 3D model)

## License and credits

Hardware license: [CERN-OHL / MIT. Choose one and add the LICENSE file.]
Credits: [If your design is based on or inspired by another open-source board, name and link it here.]
