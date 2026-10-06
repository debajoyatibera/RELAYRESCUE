# RELAYRESCUE Master BOM Review

## Status labels

- **CANDIDATE** — suggested by Gemini but not yet verified.
- **TARGET** — desired design specification; not necessarily a finalized part selection.
- **PLANNED** — intended for implementation; not a statement that the item has been purchased.
- **MEASURED** — experimentally verified only.

There are currently **no measured hardware performance results**. No component is represented here as purchased, finally selected, or experimentally verified.

## 1. Purpose

This document reviews the Gemini-generated candidate bill of materials (BOM) against the RELAYRESCUE README, system architecture, and approved hardware specification. It applies the four-motor scout requirement, resolves the LoRa endpoint count, and identifies cost, power, interface, safety, and compatibility items that must be verified before procurement.

The candidate BOM is not verified procurement truth. Exact candidate parts remain candidates until selected and checked against the complete design.

## 2. Source/candidate BOM

The following exact part/model names were supplied as Gemini suggestions. They are **CANDIDATE** items only:

| Subsystem | Gemini candidate | Review status |
|---|---|---|
| Scout motors | IG32 Planetary 12 V motor, approximately 200 RPM, 8 kg-cm | **CANDIDATE**; quantity corrected to four; exact model not finally selected |
| Motor driver | Cytron MDD10A | **CANDIDATE**; suitability for the final four-motor electrical/drive configuration is unverified |
| Robot/base controller | ESP32 DevKit V1 | **CANDIDATE**; final board selection and allocation are unverified |
| Relay deployment | DS3218 servo | **CANDIDATE**; mechanical and electrical suitability are unverified |
| Camera | Raspberry Pi Camera V2 | **CANDIDATE**; compatibility with final software and installation requires verification |
| Microphone | INMP441 | **CANDIDATE**; interface and software compatibility require verification |
| Obstacle/distance sensing | TF-Luna | **CANDIDATE**; the architecture calls for 2–3 obstacle/distance sensors, so quantity and any additional sensor selection remain open |
| IMU | BNO085 | **CANDIDATE**; the hardware specification gives MPU6050-class as a target; final selection remains open |
| Current/voltage monitor | INA219 | **CANDIDATE**; suitability for the monitored circuit requires verification |
| Edge computer | Raspberry Pi 4 Model B, 4 GB | **CANDIDATE** against the hardware specification’s **TARGET** |
| LoRa radio | Ebyte E22-900M22S / SX1262-class module | **CANDIDATE**; module model, count, antenna, compatibility, and applicable radio requirements require verification |
| Relay controller | ESP32-C3 SuperMini | **CANDIDATE**; final board selection and interface compatibility are unverified |
| Relay battery/charging | One 18650 cell + TP4056 per relay | **CANDIDATE**; the complete battery, protection, charging, and regulated-power design is unverified |
| Main battery | 3S LiPo, 5000 mAh, 11.1 V nominal, 30C | **TARGET / CANDIDATE**; not a confirmed selection and does not establish runtime |
| Raspberry Pi regulator | XL4015 5 A buck | **CANDIDATE**; final Pi power-rail performance is unverified |

The candidate information supplied does not include a complete item-by-item price list or priced subtotals. It reports only that Gemini's PDF states approximately **₹30,800**; this is retained below as an **UNVERIFIED ESTIMATE**, not a confirmed cost.

## 3. Corrected master BOM table

Quantities below describe the intended architecture where specified. **CANDIDATE** part names do not imply approval or purchase. Items shown as TBD or “as required” need final design definition.

| Subsystem | Item | Quantity / target | Candidate BOM entry | Status / review |
|---|---|---:|---|---|
| Mobile scout | Tracked metal chassis | 1 | Not specified | **PLANNED**; verify geometry and motor mounting |
| Mobile scout | DC geared motors | **4**; **TARGET:** 12 V, approximately 150–200 RPM | IG32 Planetary, 12 V, approximately 200 RPM, 8 kg-cm | **CANDIDATE** model; four motors required; verify exact motor and drive arrangement |
| Mobile scout | ESP32-class robot controller | 1 | ESP32 DevKit V1 | **CANDIDATE**; verify final controller selection and interfaces |
| Mobile scout | Dual-channel motor driver | Quantity/configuration TBD | Cytron MDD10A | **CANDIDATE**; verify for the final four-motor electrical/drive configuration |
| Mobile scout | Relay deployment servo/actuator | As required by final mechanism | DS3218 servo | **CANDIDATE**; verify torque/load, supply, travel, and mechanism |
| Sensing | Raspberry Pi-compatible camera | 1; approximately 8 MP class **TARGET** | Raspberry Pi Camera V2 | **CANDIDATE**; verify connector, software, and physical fit |
| Sensing | Microphone | 1 | INMP441 | **CANDIDATE**; verify interface, pinout, and software |
| Sensing | Obstacle/distance sensors | **2–3** | TF-Luna | **CANDIDATE** sensor; one named candidate does not establish the required full quantity |
| Sensing | Environmental sensors | **1–2**, BME280-class **TARGET** | No specific candidate supplied | **PLANNED**; select and verify variant and interface |
| Sensing | IMU | 1, MPU6050-class **TARGET** | BNO085 | **CANDIDATE** alternative; resolve the target-versus-candidate selection |
| Sensing | Current/voltage monitor | 1, INA219-class **TARGET** | INA219 | **CANDIDATE**; verify electrical range and monitored circuit |
| Edge AI | Raspberry Pi edge computer | 1; Pi 4 Model B, 4 GB **TARGET** | Raspberry Pi 4 Model B, 4 GB | **CANDIDATE** against **TARGET** |
| Edge AI | microSD | 1; 32–64 GB, U3/Class 10 **TARGET** | Not specified | **PLANNED**; verify software/data needs and compatibility |
| Edge AI | Active cooling/case | 1 | Not specified | **PLANNED**; verify board fit and airflow |
| Relay network | Deployable relay nodes | **3–4** | Not a priced/complete itemized list | **PLANNED** |
| Relay network | ESP32-class relay controllers | 1 per node: **3–4** | ESP32-C3 SuperMini | **CANDIDATE**; confirm one compatible controller per deployed node |
| Relay network | LoRa/local radio endpoints | **5–6 minimum**, depending on node count | Ebyte E22-900M22S / SX1262-class module | **CANDIDATE**; see endpoint calculation; spares are additional |
| Relay network | Antennas | One compatible antenna per radio endpoint, as required by selected module | Not specified | **PLANNED**; connector and radio compatibility TBD |
| Relay network | Independent relay battery modules | 1 per node: **3–4** | One 18650 + TP4056 per relay | **CANDIDATE**; power design not validated |
| Relay network | Relay enclosures and mounting/deployment interfaces | For each node, as required | Not specified | **PLANNED**; dimensions and mechanical interfaces TBD |
| Base station | ESP32-class base controller | 1 | ESP32 DevKit V1 candidate family | **CANDIDATE**; allocation/quantity must be confirmed |
| Base station | LoRa/local radio endpoint | 1 | Ebyte E22-900M22S / SX1262-class module | **CANDIDATE**; included in total endpoint calculation |
| Base station | Existing laptop/PC and USB data connection | 1 host and compatible connection | Existing laptop/PC | **PLANNED** use; port, cable, and software setup TBD |
| Main power | Main robot battery | 1 | 3S LiPo, 5000 mAh, 11.1 V nominal, 30C | **TARGET / CANDIDATE**; battery and complete power design require verification |
| Power conversion | DC-DC buck regulators | As required by final power budget | XL4015 5 A proposed for Pi rail | **CANDIDATE** regulator; validate complete Pi rail and other required rails |
| Safety/wiring | Fuse, fuse holder, mushroom emergency-stop | As required by final design | Not itemized | **PLANNED**; ratings, placement, and stop behavior must be finalized |
| Safety/wiring | LiPo low-voltage alarms, XT60/equivalent, 16–18 AWG silicone power wire, signal/jumper wiring, heat-shrink | As required by final design | Not itemized | **PLANNED**; compatibility and ratings TBD |

No prices are supplied here for individual rows. A missing candidate entry is not evidence that the item is unnecessary or included in Gemini's aggregate estimate.

## 4. Motor and drive correction

The approved scout architecture requires **four DC geared motors**, not two.

- **TARGET:** Four motors in the 12 V, approximately 150–200 RPM class.
- **CANDIDATE:** IG32 Planetary 12 V, approximately 200 RPM, 8 kg-cm. The exact model is not finally selected.
- **CANDIDATE:** Cytron MDD10A dual-channel motor driver. It is not verified for the complete final design.

Before selecting the driver, determine how the four motors will be electrically grouped and driven. Check the final configuration against motor operating and startup/stall current, driver channel ratings, supply voltage, thermal limits, wiring, and the intended drive arrangement. Do not infer suitability from the candidate name or from a two-motor candidate BOM.

## 5. LoRa endpoint calculation

The network requires one radio endpoint on the robot, one on each deployable relay node, and one at the base station:

```text
Minimum radio endpoints = 1 robot + number of relay nodes + 1 base station
```

| Relay nodes | Robot | Relay radios | Base station | Minimum total endpoints |
|---:|---:|---:|---:|---:|
| 3 | 1 | 3 | 1 | **5** |
| 4 | 1 | 4 | 1 | **6** |

With four relay nodes, the minimum network requires **6 radio modules**. Spares are additional. Thus, the previous 3–5 total module range is insufficient for four relay nodes and must not be used as the complete system quantity. Final module choice and allocation remain **CANDIDATE** pending interface, antenna, configuration, and regulatory checks. The communication medium remains LoRa/local radio.

## 6. Relay power review

**CANDIDATE:** One 18650 cell plus a TP4056 charging module per relay node.

This is not a validated relay power design. Before selecting or procuring it, verify for the actual cell, charger, relay controller, and radio:

- Battery protection, including suitability of the complete protection arrangement.
- Charging method and safe compatibility with the selected battery.
- Required regulated voltage and regulator arrangement.
- ESP32 and radio current requirements, including relevant peak/transient loads.
- Intended operating time under the planned workload.

Do not treat the candidate cell/charger combination as an approved or tested assembly. Final cell specifications, charging and protection implementation, regulation, connectors, and enclosure integration are procurement blockers.

## 7. Main power architecture

**TARGET / CANDIDATE:** 3S LiPo, 5000 mAh, 11.1 V nominal, 30C. This is not a confirmed battery selection and does not establish operating time.

**CANDIDATE:** XL4015 5 A buck regulator for the Raspberry Pi rail. The final Pi power rail must be verified for:

- Voltage stability at the Pi under steady and changing loads.
- Available current capacity for the Pi and any loads assigned to that rail.
- Transient load response.
- Regulator thermal performance in the planned installation.

Never connect the raw 3S LiPo directly to the Raspberry Pi. Complete a rail-by-rail power design before procurement, including suitable DC-DC conversion, fuse and emergency-stop arrangements, battery protection, wiring, and connectors. The servo must use a suitable regulated supply rather than the ESP32 power pin.

The Gemini runtime claim of approximately **1.89 hours** is not measured or verified. If retained for traceability, it can only be described as an **UNVERIFIED ESTIMATE**; it is not a runtime result or a procurement guarantee. A defensible runtime estimate requires, at minimum:

- Battery usable energy under the selected battery and operating conditions.
- Regulator efficiency at the relevant loads.
- Motor operating current for the actual terrain and drive duty.
- Raspberry Pi load.
- Sensor load.
- Radio load.
- Servo activity.
- An explicit safety margin.

No measured runtime is available.

## 8. Corrected cost calculation

The only cost information supplied is that Gemini's PDF states approximately **₹30,800**. No itemized prices, candidate line-item quantities, or priced subtotals were provided for recalculation. The figure below is therefore not a confirmed procurement cost.

| Cost view | Amount / calculation | Interpretation |
|---|---|---|
| Candidate subtotal | Approximately **₹30,800**, as stated in Gemini's PDF | **UNVERIFIED ESTIMATE**; itemization, included scope, quantities, and price basis are unavailable |
| Corrected subtotal | **Cannot be calculated from the supplied price information** | Four motors are required, but the price of a motor and the number priced in the Gemini estimate are not provided |
| Conditional motor correction | If the ₹30,800 estimate included exactly two motors at a common candidate unit price, revised estimate = approximately ₹30,800 + the cost of 2 additional motors | Arithmetic structure only; unit price and original quantity assumption are unverified, so no numeric corrected total is stated |

The following prices still require verification from an itemized candidate BOM and current vendor quotations: four motors, driver, scout/relay/base controllers, servo, camera, microphone, all required distance and environmental sensors, IMU, current/voltage monitor, Pi and storage, cooling/case, radio modules for every endpoint plus any spares, antennas, relay batteries/chargers/protection/regulators, main battery, Pi and other regulators, enclosures, deployment hardware, fuse/emergency-stop components, wiring/connectors, and any other omitted items.

Do not use ₹30,800 as a confirmed cost, corrected BOM total, purchase commitment, or evidence of availability.

## 9. Candidate wiring/interfaces

The following are Gemini-proposed **CANDIDATE** interfaces, not verified wiring instructions:

| Connection | Candidate interface | Required verification |
|---|---|---|
| Raspberry Pi ↔ ESP32 | UART, 115200 baud | Confirm voltage levels, signal directions, selected UART, common ground, software settings, and final pins |
| ESP32 ↔ motor driver | PWM/DIR | Confirm driver-specific control interface, logic levels, channel arrangement, motor grouping, and final pins |
| ESP32 ↔ TF-Luna | UART or other supported sensor interface as selected | Confirm actual sensor interface, voltage levels, bus allocation, and final pins |
| ESP32 ↔ SX1262-class radio | SPI | Confirm module interface requirements, logic/power levels, control lines, bus sharing, and final pins |
| ESP32 ↔ servo | PWM | Confirm control signal, servo supply/ground arrangement, current requirements, and final pins |

**Pin assignments require final verification.** No pin map is approved by this review. Check selected board variants, boot/strapping constraints, bus conflicts, connector mapping, logic levels, and supply requirements before producing wiring diagrams or connecting hardware.

## 10. Compatibility checks required

1. Confirm the exact motor count is four and select the final chassis/drive arrangement.
2. Verify candidate motor voltage, speed, torque, current, mounting, shaft, and operating requirements against the actual scout.
3. Verify Cytron MDD10A suitability against the final four-motor wiring/grouping, current demand, supply, and thermal design.
4. Confirm controller board variants and quantities for the robot, every relay node, and the base station; verify the ESP32-C3 SuperMini candidate against relay radio and power interfaces.
5. Resolve the 2–3 obstacle/distance sensor requirement; one TF-Luna candidate does not define the complete sensing BOM. Select and price all remaining required sensors.
6. Resolve the environmental sensor selection; the approved hardware target is 1–2 BME280-class sensors, but no Gemini candidate part or price was supplied.
7. Resolve BNO085 candidate versus MPU6050-class target and verify interface, mounting, power, and software compatibility.
8. Verify camera, microphone, current/voltage monitor, Raspberry Pi, storage, and cooling compatibility with the intended interfaces and physical installation.
9. Allocate at least one compatible LoRa/local radio to the robot, each of 3–4 relays, and the base station. Confirm total module count is 5 for three relays or 6 for four relays, before spares.
10. Verify radio module variants, antenna/connector compatibility, configuration, interface, power demand, and applicable local radio requirements.
11. Validate relay battery protection, charging method, regulated voltage, ESP32/radio load, and operating time for the final relay hardware.
12. Complete the main power budget; verify the 3S LiPo candidate against motor and regulator needs and verify the Pi rail's voltage stability, current capacity, transient load response, and thermal performance.
13. Verify servo supply/regulation independently of the ESP32 power pin; integrate fuse, emergency-stop, and battery protection into the final power design.
14. Finalize candidate UART/PWM/DIR/SPI/sensor interfaces and verify every pin assignment, logic level, shared bus, ground, connector, and power connection.
15. Recalculate the BOM from a complete, itemized quantity and price list using four motors and the corrected radio endpoint count; check all prices, included items, and omitted items before establishing a procurement estimate.

## 11. Procurement blockers

Procurement should wait until the following are resolved:

- Complete itemized BOM with quantities, unit prices, and scope; the approximate ₹30,800 statement cannot be corrected numerically from the supplied information.
- Exact motor selection and four-motor drive configuration.
- Motor-driver suitability for that final configuration.
- Relay-node count and radio module allocation, including at least six endpoints for four relays and any additional spares.
- Final relay battery/protection/charging/regulator design.
- Main battery and complete power budget, including the Raspberry Pi rail and servo supply.
- Final selection and quantity of obstacle/distance sensors and environmental sensors.
- Resolution of candidate-versus-target sensor and controller variants.
- Pin-level wiring and interface compatibility review.
- Fuse, emergency-stop, low-voltage alarm, and battery-protection design.
- Verification of all prices, availability, compatibility, and included accessories from current procurement sources. No availability or purchasing status is established by this document.

## 12. Final status summary

- The approved mobile scout requirement is **four** 12 V, approximately 150–200 RPM-class geared motors. The IG32 Planetary suggestion remains **CANDIDATE**, not a final selection.
- Cytron MDD10A remains **CANDIDATE** pending review against the final four-motor drive and electrical configuration.
- LoRa/local radio is retained. A four-relay network requires six minimum radio endpoints; spares are additional.
- One 18650 cell plus TP4056 per relay, the 3S LiPo 5000 mAh main battery, and XL4015 Pi regulator are **CANDIDATE / TARGET** design suggestions requiring verification.
- The approximately ₹30,800 figure and approximately 1.89-hour runtime are not measured or verified. A corrected numeric cost cannot be calculated without itemized prices and motor-price basis; runtime requires a complete power/load assessment.
- Gemini's exact model suggestions and proposed interfaces remain **CANDIDATE**. Final selections, wiring, pin assignments, and procurement status are not established.
- There are currently **no MEASURED hardware performance results**.
