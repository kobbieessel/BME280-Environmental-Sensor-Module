# BME280 Environmental Sensor Module (I2C)

A production-minded BME280 environmental sensor module designed for reliable temperature, humidity, and pressure sensing in embedded and robotic systems.
This project emphasizes power integrity, I2C reliability, and reusable hardware design, rather than just functional bring-up.

---

## Overview

Most off-the-shelf sensor breakouts are designed for quick demos and ignore system-level considerations such as power stability, address conflicts, and reuse across platforms.
The goal of this project was to design a robust, reusable BME280 sensor module suitable for real embedded systems, robotics platforms, and MCU bring-up workflows.

---

## Design Goals

- Reliable 3.3 V operation
- Stable I2C communication
- Clear address configuration for multi-sensor systems
- Compact and reusable PCB footprint
- Datasheet-driven electrical design

---

## Features

- Measures **temperature, humidity, and atmospheric pressure**
- **I2C communication interface**
- **3.3 V operation**
- On-board **I2C pull-up resistors**
- Proper **local decoupling and bulk capacitance**
- Default I2C address configured via **SDO pin**
- Test points for power and I2C lines
- Compact PCB designed for reuse in embedded systems

---

## Electrical Specifications

| Parameter           | Value                   |
| ------------------- | ----------------------- |
| Supply Voltage      | 3.3 V                   |
| Interface           | I2C                     |
| Default I2C Address | 0x76 (SDO → GND)        |
| Pull-up Resistors   | 4.7 kΩ (SDA, SCL)       |
| Decoupling Caps     | 100 nF + bulk capacitor |

---

## Hardware Architecture

### Power Integrity
 - A 100nF decoupling capacitor is placed close to the BME280 supply pin
 - Additional bulk capacitance is added to stabilize the 3.3 V rail during transient conditions
   **Why?**
   I made these decisions to improve the sensor stability and reduce random communication issues that may be caused due to power supply noise.

### I2C Reliability & Signal Integrity Considerations
 - An On-board 4.7 kΩ pull-up resistors attacted to the SDA and SCL line
 - Designed to support standard I2C bus speeds on short-to-moderate interconnect lengths
   **Trade-Off**
   The on-board pul-up resistor simplifies integration while maintaining acceptable rise time and current consumption

### Address Management

The BME280 supports two I2C addresses:
- **SDO = 0 (GND)→ 0x76 (default)**
- **SDO = 1 (VDDIO) → 0x77**

 - BME280 **SDO pin tied to GND** to set default address to 0x76
 - Enables coexistence with other I2C devices or additional BME280 sensors
   **Why this matters:**
   This will prevents address conflicts in scalable sensor architectures.

### Schematic and PCB Design
 - Clean, readable schematic with clear signal labeling
 - Compact PCB layout optimized for reuse
 - Routing and grounding aligned with mixed-signal best practices
 - Testable power and communication paths

### PCB Layout
> ![SCHEMATIC CAPTURE](Images/Schematic.png)

### PCB Layout

> ![PCB LAYOUT](Images/PCBLayout.png)

### 3D View 

> ![PCB TOP VIEW](Images/pcb_top.png) > ![PCB BOTTOM VIEW](Images/pcb_bottom.png)

### Design Notes

- **VDD and VDDIO** are powered at 3.3 V to match microcontroller logic levels.
- **I²C pull-up resistors (4.7 kΩ)** are connected to 3.3 V to ensure reliable SDA/SCL signaling.
- **Decoupling capacitors (100 nF)** are placed close to the BME280 supply pins to suppress high-frequency noise.
- A **bulk capacitor** is included to stabilize the local power rail during transient current events.
- The **SDO pin is tied to GND** by default to select the lower I2C address.
- **Test points** are provided on critical nets (3.3 V, GND, SDA, SCL) to simplify probing, debugging, and validation.

---
## Test & Validation

- Powered using a regulated **3.3 V supply**
- Successfully detected on the I2C bus
- Sensor readings verified through microcontroller-based testing
- Stable communication observed with no bus errors

---

## Lessons Learned

- Importance of reading **power-domain requirements** carefully in sensor datasheets
- Proper **pull-up resistor sizing** is critical for reliable I2C communication
- Decoupling placement has a significant impact on signal stability
- Small hardware modules benefit greatly from early validation and address planning
- Datasheet-driven design prevents subtle integration failures

---

## Intended Applications

 - Embedded system bring-up and testing
 - Environmental sensing in robotics platforms
 - Modular sensor nodes for IoT or monitoring systems
 - Reference design for I2C peripheral integration

---

## Tools Used

 - PCB Design: KiCad
 - Sensor Datasheet: Bosch BME280
 - Interface: I2C
   
---

## Files Included

- Schematic
- PCB layout
- [Gerber files](Hardware/Gerber)
- [Bill of Materials (BOM)](Hardware/BOM.xlsx)
- [BME280 datasheet](bme280-datasheet.pdf)

---

## Future Improvements (v2 Ideas)

- Optional jumper for IC address selection
- Mounting holes for mechanical integration
- SPI interface option

# Author 
**Kwabena Amoako**
Embedded Systems | Hardware & Firmware | Robotics

Social:
[LinkedIn](https://www.linkedin.com/in/kwabena-e-amoako/)

