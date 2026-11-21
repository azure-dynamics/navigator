# Navigator: Design Notes

Rev 003. Raspberry Pi HAT-form-factor controller for the Azure ROV: ESP32-S3 drives six BLDC ESC signals, reads sensors over I2C, and talks to a Raspberry Pi over UART.

## Decisions and rationale

### MCU
- **ESP32-S3-MINI-1U module**, not a bare SoC. A bare SoC plus crystal and flash adds layout risk for no benefit, since no RF is used.
- **No microSD.** Not needed.

### Power
- **Input:** 4S LiPo now, designed for 4-6S in case a better ESC means moving to 6S.
- **Buck:** MPM3550EGLE module, 5 V at up to 3 A. Replaced the original LM2576 + large inductor design, which took about half the board. TPSM656x0 was considered but out of stock.
- **Protection:** bidirectional SMCJ26CA TVS across +BATT at the battery connector.
- **5V rail:** diode-OR of USB_5V and BUCK_5V, so the board can be flashed over USB without the battery. 3V3 from an AP2112K-3.3.
- **Battery sensing:** INA226 measures bus voltage only (shunt inputs tied to GND).

### Pi link
- UART between the ESP32-S3 and Pi GPIO14/15. No separate UART daughterboard link, since UART is not a bus.

### Sensors / I2C
- Single I2C bus on IO7/IO8 with 2k2 pull-ups on the board. These are the only board pull-ups; the sensor modules add their own, so don't add more.
- **BNO086 chip removed from the board.** It clock-stretches over I2C, and moving it off-board doesn't remove that, so firmware needs a generous I2C timeout. The IMU is now an external STEMMA QT module, which keeps the wiring to one cable (no SPI or UART).
- **Two different connector families on purpose** so cables can't be swapped:
  - J9: barometer (MS5837-02BA), JST GH, Blue Robotics precrimped cable.
  - J10: IMU, JST SH (STEMMA QT).

### Layout
- 4 layers. Wide top-layer trace for BUCK_5V; inner 2 is 3V3 only. Ground stitching vias around the buck.
- I2C routed short; USB D+/D- on the back layer.

## Connector pinouts

| Connector | Function | Pin 1 | Pin 2 | Pin 3 | Pin 4 |
|---|---|---|---|---|---|
| J9 (JST GH) | Barometer MS5837 | +3V3 | I2C_SCL | I2C_SDA | GND |
| J10 (JST SH) | IMU, STEMMA QT | GND | +3V3 | I2C_SDA | I2C_SCL |

## Other connectors
- J1-J6: six 3-pin BLDC signal connectors on IO1-IO6, each signal with a 10k pull-down.
- Battery input and Pi GPIO header: see the schematic.

