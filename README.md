# Navigator

**Flight-controller Pi HAT for Azure Dynamics' Radiance ROV**

Navigator is a Raspberry Pi HAT designed to host the low-level flight controller for the Radiance ROV. It manages communication between the Raspberry Pi and the ROV's hardware, monitoring system power and routing control signals.

---

## Features

* **Flight Control:** Powered by an ESP32-S3 processor.
* **Power Management:** On-board voltage regulation supplying power directly to the Raspberry Pi and HAT logic.
* **Propulsion Signals:** Six dedicated ESC signal outputs for motor control.
* **Sensor Integration:** Includes battery voltage monitoring and I2C expansion support for added sensors (such as an IMU).
* **Mission Computer Link:** Direct hardware UART communication with the Raspberry Pi.
* **Standard Footprint:** Designed to fit the standard Raspberry Pi HAT layout with mounting holes.

---

## Board Layout & Architecture

* **Layers:** 4-layer board design.
* **Component Placement:** Most components are located on the top side, with connectors and support resistors positioned underneath.
* **Connectivity:** Features a USB-C port for programming and debugging, alongside the main Raspberry Pi GPIO header connection.

---

## Project Status

* **Schematic:** Complete (Revision 002)
* **Layout:** Waiting for review
* **Fabrication:** Not yet ordered

---

## Repository Layout

```text
navigator/
├── hardware/       KiCad project and local symbol/footprint libraries
├── fabrication/    Manufacturing outputs (BOM, Gerbers, drill files)
├── firmware/       Flight-controller code
├── docs/           Project documentation
├── LICENSE
└── README.md
```

### Local Libraries

* `hardware/library/282837-2/` — TE 282837-2 connector footprint and STEP model.
* `hardware/library/BNO086/` — BNO086 IMU symbol and footprint.
* `hardware/library/logo/` — Board logo footprint.

---

## License

Copyright (C) 2026 Azure Dynamics.

This project is licensed under the
[CERN Open Hardware Licence Version 2 - Strongly Reciprocal](LICENSE)
(`CERN-OHL-S-2.0`). See [LICENSE](LICENSE) for the full text.

Third-party symbols, footprints, and STEP models in `hardware/library/` are
included for convenience and remain subject to their original terms.
