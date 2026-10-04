# Robotics & Embedded Systems (IoT) Roadmap

![Status](https://img.shields.io/badge/status-in%20progress-orange.svg) ![License](https://img.shields.io/badge/license-MIT-green.svg) ![language](https://img.shields.io/badge/language-C%20%7C%20python-blue.svg) ![hardware](https://img.shields.io/badge/hardware-ESP32%20%7C%20Pico-orange.svg)

From blinking an LED to a robot that senses, decides, and moves. Embedded firmware, control theory, ROS 2, and connected devices, starting in simulation so you can begin without hardware.

## Table of Contents

1. [Workflow Overview](#workflow-overview)
2. [Prerequisites](#prerequisites)
3. [Phase 1: Embedded Basics](#phase-1-embedded-basics)
4. [Phase 2: RTOS & Connectivity](#phase-2-rtos--connectivity)
5. [Phase 3: Control & Kinematics](#phase-3-control--kinematics)
6. [Phase 4: ROS 2 & Simulation](#phase-4-ros-2--simulation)
7. [Phase 5: Secure & Integrate](#phase-5-secure--integrate)
8. [Capstone Projects](#capstone-projects)
9. [Repository Layout](#repository-layout)
10. [Engineering Rules](#engineering-rules)
11. [Exit Criteria](#exit-criteria)

---

## Workflow Overview

```
 Electronics + C --> RTOS + connectivity --> Control theory
                                                  |
 IoT dashboard <-- MQTT <-- Sensors/actuators <---+
                                                  |
                           ROS 2 + simulation <---+--> Capstone robot
```

## Prerequisites

- [ ] C basics (see the Architecture and Systems roadmap, Phase 2)
- [ ] Python
- [ ] Algebra and basic calculus; linear algebra helps from Phase 3
- [ ] A microcontroller kit (ESP32 or Raspberry Pi Pico) by Phase 1, or use the simulator

## Phase 1: Embedded Basics

Goal: Write firmware that talks to hardware.

| Resource | Type | Why |
|----------|------|-----|
| [Wokwi Simulator](https://wokwi.com/) | Simulator | Run ESP32, Pico, and Arduino projects without hardware |
| [Arduino Documentation](https://docs.arduino.cc/) | Docs | Fast first projects |
| [Raspberry Pi Pico C/C++ SDK](https://www.raspberrypi.com/documentation/microcontrollers/c_sdk.html) | Docs | Move from Arduino to real C firmware |
| [PlatformIO Documentation](https://docs.platformio.org/) | Docs | Proper build system for embedded |
| [Interrupt by Memfault](https://interrupt.memfault.com/) | Blog | Professional embedded practices |

- [ ] GPIO, PWM, ADC, timers, and interrupts
- [ ] Serial, I2C, and SPI with one real sensor each
- [ ] Read a datasheet and write a driver from it

**Deliverables**
- [ ] `firmware/drivers/` with sensor drivers
- [ ] `docs/datasheet_notes.md`

## Phase 2: RTOS & Connectivity

Goal: Run multiple tasks reliably and connect devices.

| Resource | Type | Why |
|----------|------|-----|
| [Mastering the FreeRTOS Real Time Kernel](https://www.freertos.org/Documentation/02-Kernel/07-Books-and-manual/01-RTOS_book) | Free book | Tasks, queues, semaphores |
| [ESP-IDF Programming Guide](https://docs.espressif.com/projects/esp-idf/en/stable/) | Docs | ESP32 networking and drivers |
| [MQTT Getting Started](https://mqtt.org/getting-started/) | Docs | Standard IoT messaging protocol |

- [ ] Create tasks, queues, and mutexes; find a priority inversion on purpose
- [ ] Connect an ESP32 to Wi-Fi and publish sensor data over MQTT
- [ ] Add watchdog and low-power sleep

**Deliverables**
- [ ] `firmware/sensor_node/` publishing to an MQTT broker
- [ ] Dashboard in Grafana or similar showing live data

## Phase 3: Control & Kinematics

Goal: Make machines move accurately.

| Resource | Type | Why |
|----------|------|-----|
| [Feedback Systems (Åström & Murray)](https://fbswiki.org/wiki/index.php/Main_Page) | Free book | Feedback and control fundamentals |
| [Modern Robotics (Lynch & Park)](http://hades.mech.northwestern.edu/index.php/Modern_Robotics) | Free book | Kinematics, dynamics, motion planning |
| [PythonRobotics](https://github.com/AtsushiSakai/PythonRobotics) | Repo | Readable implementations of core algorithms |

- [ ] PID control: tune on a motor or simulated plant
- [ ] Forward and inverse kinematics for a 2-link arm
- [ ] Kalman filter for sensor fusion
- [ ] Path planning: A*, RRT

**Deliverables**
- [ ] `src/control/` with PID, Kalman filter, kinematics, typed and tested
- [ ] Plots of step response and tracking error in `docs/control_report.md`

## Phase 4: ROS 2 & Simulation

Goal: Use the standard robotics middleware.

| Resource | Type | Why |
|----------|------|-----|
| [ROS 2 Tutorials](https://docs.ros.org/en/rolling/Tutorials.html) | Docs | Nodes, topics, services, actions |
| [Gazebo Documentation](https://gazebosim.org/docs) | Docs | Physics simulation |
| [Nav2 Documentation](https://docs.nav2.org/) | Docs | Navigation stack |
| [Introduction to Autonomous Robots](https://github.com/Introduction-to-Autonomous-Robots/Introduction-to-Autonomous-Robots) | Free book | Concepts for mobile robots |

- [ ] Write publisher, subscriber, service, and action nodes
- [ ] Simulate a differential-drive robot in Gazebo
- [ ] Run SLAM and autonomous navigation with Nav2

**Deliverables**
- [ ] `ros2_ws/src/` with your packages and launch files
- [ ] Video of the simulated robot navigating to goals

## Phase 5: Secure & Integrate

Goal: Ship devices that are safe to deploy.

| Resource | Type | Why |
|----------|------|-----|
| [OWASP Internet of Things Project](https://owasp.org/www-project-internet-of-things/) | Reference | Common IoT vulnerabilities |
| [The Rust Embedded Book](https://docs.rust-embedded.org/book/) | Free book | Optional: memory-safe firmware |

- [ ] Threat-model your sensor node: what can an attacker on your Wi-Fi do?
- [ ] Add TLS to MQTT and signed OTA updates
- [ ] Integrate firmware, broker, and dashboard end to end

**Deliverables**
- [ ] `docs/iot_threat_model.md`
- [ ] Integrated system with documented failure behavior

## Capstone Projects

- [ ] Hardware: a line-following or self-balancing robot with PID control and logged tuning data
- [ ] IoT: three ESP32 sensor nodes publishing over MQTT with a live dashboard and alerts
- [ ] Simulation: a ROS 2 differential-drive robot mapping a room and navigating autonomously
- [ ] Write a design report that states what failed and what you changed

## Repository Layout

```
robotics-embedded/
├── README.md
├── firmware/
│   ├── drivers/
│   ├── sensor_node/
│   └── platformio.ini
├── src/
│   └── control/              # PID, Kalman, kinematics (host-testable)
├── ros2_ws/
│   └── src/
├── hardware/                 # schematics, BOM, wiring photos
├── tests/
│   ├── host/                 # unit tests that run on your PC
│   └── sim/
└── docs/
    ├── datasheet_notes.md
    ├── control_report.md
    └── iot_threat_model.md
```

## Engineering Rules

These are strict. A phase is not complete until its deliverables follow all of them.

### 1. Daily 1:3 Theory-to-Building Ratio

- [ ] For every 1 hour of reading or watching, spend 3 hours building, solving, or running labs
- [ ] Log hours in `docs/log.md` at the end of each session
- [ ] No new chapter until the previous one has working code or a written lab report

### 2. Git Branch Hygiene

- [ ] `main` is always green and never receives direct commits
- [ ] One branch per deliverable: `phase-N/short-description`
- [ ] Small commits with imperative messages; squash-merge via PR after checks pass
- [ ] Delete branches after merge

### 3. Quality Gates

- [ ] Firmware builds with warnings as errors; `clang-format` and `cppcheck` pass
- [ ] Logic is host-testable: unit tests run on your PC with [Unity](https://github.com/ThrowTheSwitch/Unity), no board required
- [ ] Python control code passes `mypy --strict` and `pytest`
- [ ] Test in the simulator before touching hardware

### 4. Branch-Specific Rules

- [ ] Handle lithium batteries correctly: use protected cells, proper chargers, and never charge unattended
- [ ] Never work on mains voltage; use low-voltage supplies only
- [ ] Power off before rewiring and double-check polarity before applying power
- [ ] Define a safe failure state for every actuator and test it (motor stops when the sensor dies)
- [ ] Never commit Wi-Fi credentials or keys; use a git-ignored config file

## Exit Criteria

- [ ] Write a sensor driver from a datasheet and verify it with a logic analyzer or scope trace
- [ ] Tune a PID loop and show the response curves
- [ ] Explain why a task in your RTOS missed a deadline
- [ ] Run an autonomous navigation demo in simulation and explain each node
