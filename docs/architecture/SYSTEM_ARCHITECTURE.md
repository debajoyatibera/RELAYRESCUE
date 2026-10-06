# RELAYRESCUE System Architecture

## Project identification

| Item | Details |
|---|---|
| Project | RELAYRESCUE |
| Competition | Vishwakarma Awards 2026–27 |
| Theme | Physical AI for Resilience and Inclusion |
| Sub-theme | Autonomous Search, Rescue & Tactical Robotics |
| Application ID | VK26-AU-PAI-0372 |

## Status and evidence labels

- **Target** describes the intended system configuration or an evaluation objective. No numeric target values are specified here.
- **Planned** describes work or an experiment intended for evaluation; it is not a completed result.
- **Measured** is reserved for results recorded from an experiment. No measured performance results are included in this document.

The architecture below describes the intended system. Relay-failure recovery is a **Planned** experiment; automatic recovery is not claimed as demonstrated.

## System overview

RELAYRESCUE is organized as a tracked mobile scout, an onboard sensing and edge-computing path, deployable relay nodes, and a base station connected to an operator PC/dashboard.

```text
Tracked scout
  Camera and robot sensors
          |
          v
Raspberry Pi 4-class edge computer (Edge AI)
          |
          v
ESP32-class robot controller
          |
          v
LoRa/local radio
          |
          v
Deployable relay nodes (3–4; ESP32-class controllers)
          |
          v
Base station/gateway
          |
          v
Operator PC/dashboard
```

This shows the project’s specified forward system flow. No reverse command path or particular message format is specified here.

## Architecture layers

### 1. Mobile Scout Layer

The scout is a tracked mobile robot. An ESP32-class controller handles low-level movement and payload deployment. A Raspberry Pi 4-class edge computer is carried as the edge-computing component.

**Target:** Use the mobile scout to carry the sensing and relay payloads through the evaluation area. No mobility, payload-capacity, or operating-environment performance is claimed here.

### 2. Multimodal Sensing Layer

The robot sensing set consists of:

- Camera
- Microphone
- Environmental sensors
- Obstacle/distance sensors
- IMU
- Current/voltage monitoring

Robot sensor and camera information enters the edge-computing path. The architecture does not specify sensor models, sampling rates, or a sensor-fusion method.

### 3. Edge Intelligence Layer

The Raspberry Pi 4-class edge computer hosts Edge AI and receives robot sensor/camera information. Its position in the specified flow is before the ESP32-class controller.

**Planned evaluation:** AI performance may be characterized using precision/recall, false alerts, and AI uncertainty. No AI accuracy or other AI result is asserted.

### 4. Deployable Network Layer

The scout carries **3–4 deployable relay nodes**. Each relay node uses an ESP32-class controller, and the network uses **LoRa/local radio** to pass information toward the base station/gateway.

The radio choice remains LoRa/local radio; no particular range, topology, routing behavior, or communication protocol details are asserted.

### 5. Operator Station Layer

The base station/gateway connects the relay network to the operator PC/dashboard. The dashboard is the operator-facing endpoint for information delivered through the system.

No dashboard functions beyond this role, or a reverse control channel from the dashboard, are specified here.

### 6. Power/Safety Layer

Current/voltage monitoring is part of the robot’s sensing set. It provides measurements for observing electrical conditions during operation and evaluation.

No battery specification, runtime, power cutoff, or other unlisted safety mechanism is claimed.

## Data flow

1. The camera and robot sensors produce information, including microphone, environmental, obstacle/distance, IMU, and current/voltage readings.
2. Sensor and camera information flows to the Raspberry Pi 4-class edge computer for Edge AI.
3. The specified system flow continues from Edge AI to the ESP32-class robot controller.
4. Information is sent over LoRa/local radio through the deployable relay nodes to the base station/gateway.
5. Information delivered to the gateway is made available at the operator PC/dashboard.

The architecture does not define data schemas, prioritization, buffering, or image/audio encoding.

## Control flow

The ESP32-class robot controller is responsible for low-level movement and payload deployment. In the specified forward flow, the Raspberry Pi Edge AI precedes this controller. Control-related behavior beyond those responsibilities—including operator-issued commands, decision logic, and command formats—is not specified here.

## Communication flow

The intended forward communication path is:

```text
ESP32-class robot controller
  → LoRa/local radio
  → 3–4 deployable relay nodes
  → Base station/gateway
  → Operator PC/dashboard
```

The relays are intended to carry information toward the gateway. Communication range, link reliability, network topology, and failover behavior remain to be established through testing.

## Planned relay-failure/recovery experiment

**Planned:** Evaluate information delivery with the deployable relay network under a controlled relay-failure condition. Record whether and when information delivery resumes, and compare communication measurements before, during, and after the failure condition.

This experiment is intended to assess relay-failure/recovery behavior; it does not establish that automatic recovery has already been implemented or demonstrated. The failure procedure, repetitions, and acceptance thresholds are not specified here.

## Key measurable metrics

**Planned measurement categories** for system evaluation:

- Packet delivery ratio and packet loss
- Latency and end-to-end information delivery time
- Usable communication range
- Recovery time during the planned relay-failure/recovery experiment
- AI precision/recall, false alerts, and AI uncertainty
- Runtime
- Energy per message

These are measurement categories, not reported results. Numeric targets and **Measured** values are not supplied in this document.
