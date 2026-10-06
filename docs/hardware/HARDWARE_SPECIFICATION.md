# RELAYRESCUE Hardware Specification

## Status and evidence labels

- **Target** identifies a desired component class or nominal specification, not a confirmed selection.
- **Planned** identifies hardware intended for the design or procurement process; it does not mean the item has been purchased or tested.
- **Measured** is reserved for results obtained through testing. No hardware specifications or performance results in this document are experimentally verified.

No manufacturer part numbers, prices, or availability are specified. Final selections remain subject to the checks in [Items requiring final verification before procurement](#12-items-requiring-final-verification-before-procurement).

## 1. Purpose

This document records the approved hardware architecture for the RELAYRESCUE mobile scout, sensing, edge AI, deployable relay network, base station, power and safety hardware, and tools. It is intended to guide detailed design and procurement verification.

## 2. Hardware architecture

The planned hardware path follows the system architecture:

```text
Tracked mobile scout and sensors
  → Raspberry Pi 4 Model B (4GB) edge computer
  → ESP32-class robot controller
  → LoRa/local radio modules and deployable relay nodes
  → ESP32-class base controller / base station
  → Existing laptop/PC
```

The mobile scout uses four DC geared motors, a dual-channel motor driver, and a servo/actuator for relay-node deployment. Three to four independently powered relay nodes use ESP32-class controllers. LoRa/local radio modules and antennas support the robot, relay, and base-station links.

All items below are **Planned** unless specifically marked **Target**. No item is stated to have been purchased, and no compatibility or performance claim is **Measured**.

## 3. Mobile scout hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Tracked metal chassis | 1 chassis | **Planned** |
| DC geared motors | 4; **Target:** 12 V, approximately 150–200 RPM motor class | **Planned**; verify motor and chassis compatibility |
| Robot controller | ESP32-class | **Planned**; low-level movement and payload deployment control |
| Motor driver | Dual-channel | **Planned**; confirm channel arrangement and electrical ratings against all four motors and the selected drive scheme |
| Relay deployment actuator | Servo/actuator | **Planned**; verify mechanical travel, load, mounting, and controller interface |
| Main robot battery | 1 | **Planned**; chemistry, voltage, capacity, and current rating require final selection |

## 4. Sensing hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Camera | Raspberry Pi-compatible, approximately 8 MP class | **Target**; connector and software compatibility require verification |
| Microphone | 1 | **Planned**; interface and connection method require final selection |
| Obstacle/distance sensors | 2–3 | **Planned**; sensor type, range, and electrical interface require final selection |
| Environmental sensors | 1–2; BME280-class | **Target**; confirm selected sensor interface and operating conditions |
| IMU | MPU6050-class | **Target**; verify bus, voltage, mounting, and software support |
| Current/voltage monitor | INA219-class | **Target**; confirm voltage/current measurement suitability and connection to the monitored power path |

## 5. Edge AI hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Edge computer | Raspberry Pi 4 Model B, 4GB | **Target** |
| Storage | 32–64 GB microSD, U3/Class 10 | **Target**; confirm compatibility and capacity for the selected software and data |
| Cooling/enclosure | Active cooling/case | **Planned**; verify fit and airflow for the selected board and installation |
| Controller connection | 3.3 V UART connection to ESP32 | **Planned**; confirm signal direction, wiring, pin assignment, and common ground |
| Edge-computer power | 5 V 5 A UBEC-class supply if required by final power design | **Target / conditional**; validate against the selected board, peripherals, regulator, and power architecture before use |

## 6. Relay-node hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Relay nodes | 3–4 | **Planned** |
| Relay controllers | ESP32-class, one per relay node | **Planned** |
| LoRa/local radio modules | 3–5 total across robot, relays, and base station | **Planned**; final count and allocation depend on the selected communication design |
| Antennas | For the selected radio modules | **Planned**; connector and radio compatibility require verification |
| Relay power | Independent battery module for each relay node | **Planned**; battery specifications require final selection |
| Enclosures | For relay nodes | **Planned**; verify fit and suitability for the intended test environment |
| Mounting/deployment interfaces | For relay nodes and scout | **Planned**; verify attachment, release, and actuator compatibility |

The network communication medium is LoRa/local radio. No radio range, topology, link performance, or recovery behavior is specified as verified.

## 7. Base station hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Base controller | ESP32-class | **Planned** |
| Base radio | LoRa/local radio module compatible with the selected network modules | **Planned** |
| Operator computer | Existing laptop/PC | **Planned** use; host connection and software setup require verification |
| Data connection | USB data connection | **Planned**; verify cable, port, and controller interface |

## 8. Power hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Main robot battery | For mobile scout | **Planned**; select only after motor, controller, and regulator requirements are established |
| Relay battery modules | Independent supply for each relay node | **Planned**; select based on the final node load and operating plan |
| DC-DC buck regulators | Appropriate outputs for the selected loads | **Planned**; number and ratings require power-budget verification |
| Raspberry Pi supply | 5 V 5 A UBEC-class, if required by final power design | **Target / conditional** |
| Wiring and connectors | XT60/equivalent connectors; 16–18 AWG silicone power wire; signal/jumper wiring | **Planned**; verify current capacity, connector compatibility, polarity, and routing |
| Insulation/strain protection | Heat-shrink | **Planned** |

Battery chemistry, capacity, regulator ratings, fuse rating, connector selection, wiring lengths, and runtime are not specified. Runtime and energy performance are not **Measured**.

## 9. Safety hardware

| Component | Quantity / specification | Status and notes |
|---|---|---|
| Fuse and fuse holder | Appropriate for the final power design | **Planned**; rating and placement require final current and wiring review |
| Emergency stop | Mushroom emergency-stop | **Planned**; define and verify its effect on the powered systems before operation |
| Battery low-voltage alarms | LiPo low-voltage alarms | **Planned**; verify compatibility with the selected battery configuration |
| Power connectors | XT60/equivalent | **Planned**; verify current suitability, polarity, and connection security |
| Power wiring | 16–18 AWG silicone power wire | **Planned**; confirm suitability for the final current, length, and installation |
| Wiring insulation | Heat-shrink | **Planned** |

This list identifies safety hardware to include in detailed design. It does not establish a completed safety review or demonstrate a verified emergency-stop, fuse, or low-voltage response.

## 10. Tools

**Planned tools:**

- Digital multimeter
- 25–35 W soldering iron
- Solder and flux
- Wire stripper/cutter
- Screwdriver/hex-key set
- Measuring tape

**Optional tools:**

- Crimping tool
- Heat gun
- Pliers
- Tweezers
- Drill
- Caliper

Tool ownership, availability, and condition are not specified.

## 11. Interface/compatibility notes

- **Motors and drive:** Match the four selected motors, dual-channel driver, chassis, and drive arrangement. Verify driver voltage/current limits, motor startup/stall requirements, and thermal suitability before wiring.
- **Controller and logic levels:** The planned Raspberry Pi-to-ESP32 UART connection is 3.3 V. Verify both devices’ signal levels, pin assignments, wiring, and common-ground arrangement.
- **Sensors:** Confirm each selected sensor’s interface, supply voltage, logic levels, connector, and software support against the intended controller or edge computer.
- **Camera and microphone:** Confirm the selected camera is compatible with the Raspberry Pi 4 Model B and verify the microphone interface and software path.
- **Radio and antennas:** Use LoRa/local radio modules across the robot, relay nodes, and base station. Match modules, antennas, connectors, and configuration; verify applicable local radio requirements before operation. No specific band or range is selected here.
- **Relay deployment:** Check node enclosure dimensions, mounting interfaces, actuator travel/load, and release clearances together before finalizing the scout layout.
- **Power distribution:** Establish a load and power budget for motors, computing, sensors, controller, actuator, and radios. Size batteries, regulators, fuse, connectors, and wire from the final design rather than assuming the listed target classes are sufficient.
- **Base connection:** Verify that the selected base controller supports the planned USB data connection to the existing laptop/PC.
- **Physical integration:** Check chassis space, component mounting, cable routing, strain relief, cooling airflow, and access to the emergency-stop before assembly.

These are design checks, not claims that compatibility has been experimentally verified.

## 12. Items requiring final verification before procurement

1. Confirm the chassis dimensions, track arrangement, motor mounting, and the final four-motor drive scheme.
2. Select motors within the target 12 V, approximately 150–200 RPM class and verify their load, current, shaft, and mounting requirements.
3. Confirm the dual-channel motor driver is suitable for the selected motors and drive scheme.
4. Select the main robot battery and relay batteries, including chemistry, voltage, capacity, discharge capability, connectors, and charging approach.
5. Complete the power budget and select appropriate DC-DC regulators; determine whether the 5 V 5 A UBEC-class supply is required for the Raspberry Pi power design.
6. Determine fuse rating and placement, emergency-stop wiring/effect, and low-voltage alarm compatibility for the final battery and distribution design.
7. Confirm wire and connector suitability for expected current, installation length, and environmental/mechanical conditions.
8. Confirm the Raspberry Pi 4 Model B, camera, microSD, active cooling/case, and selected software/data requirements are compatible.
9. Verify UART signal connections between the Raspberry Pi and ESP32-class robot controller, including 3.3 V logic, pin assignments, and common ground.
10. Select compatible sensor variants and verify their interfaces, voltage levels, mounting, and software support.
11. Determine the final LoRa/local radio module count and allocation within the 3–5 total range; match modules and antennas and verify applicable local radio requirements.
12. Select relay enclosures, independent batteries, and mounting/deployment interfaces; verify fit and actuator compatibility.
13. Verify the base controller's USB data connection to the existing laptop/PC.
14. Confirm the selected tools are available and appropriate for the planned assembly work.

No procurement completion, component availability, measured specification, or experimentally verified compatibility is asserted in this document.
