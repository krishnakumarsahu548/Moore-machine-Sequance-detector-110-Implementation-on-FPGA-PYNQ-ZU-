# Moore-machine-Sequance-detector-110-Implementation-on-FPGA-PYNQ-ZU-
This repository presents the design and implementation of a **Moore Finite State Machine (FSM)** based **sequence detector for the pattern "110"**, implemented on the **PYNQ-ZU FPGA board** using **Verilog HDL and Vivado**.



## 🔹 Project Overview

- **FSM Type:** Moore Machine  
- **Target Sequence:** 110  
- **Platform:** PYNQ-ZU (Zynq UltraScale+)  
- **Design Language:** Verilog HDL  
- **Verification:** Simulation + On-board FPGA testing  
- **Debugging:** Integrated Logic Analyzer (ILA)

The output is asserted **only when the FSM reaches the detection state**, consistent with Moore machine behavior.

---

## 🔹 FSM Description
<img width="1600" height="1394" alt="image" src="https://github.com/user-attachments/assets/18e6a095-2c4e-415d-af70-740145bd40b0" />

### State Encoding
| State | Binary |
|------|--------|
| A | 00 |
| B | 01 |
| C | 10 |
| D | 11 (Output = 1) |

### State Transitions
- A → B on input `1`
- B → C on input `1`
- C → D on input `0`
- Output `y = 1` only in **State D**

Overlapping sequence detection is supported.

---

## 🔹 Hardware Mapping (PYNQ-ZU)

| Signal | Board Resource |
|------|---------------|
| clock_p / clock_n | 125 MHz LVDS Clock (Si5340) |
| rst | Push Button (BTN0) |
| x | Switch (SW0) |
| y | LED (LED0) |

---

## 🔹 Features

- LVDS clock handling using `IBUFDS`
- Safe asynchronous input synchronization
- Clock-enable based divider for human-visible LED output
- ILA-based on-chip debugging
- Verified on real FPGA hardware

---

## 🔹 Repository Structure
## Verilog RTL design
<img width="1577" height="385" alt="image" src="https://github.com/user-attachments/assets/2eb8b2cc-92ea-4696-858a-22b8d6385553" />
<img width="830" height="727" alt="image" src="https://github.com/user-attachments/assets/ad12573d-deb7-4c96-98d4-00d340aa5ef5" />
<img width="1188" height="915" alt="image" src="https://github.com/user-attachments/assets/925304bb-3f7c-470c-b52b-23b438637fab" />


## 🔹 Simulation

A behavioral testbench is provided to verify FSM operation using waveform analysis.

<img width="1106" height="417" alt="image" src="https://github.com/user-attachments/assets/c589d5b5-8310-474d-a668-fe18f67bfb0b" />
## clock-enable signal
// slow_en is used as a clock-enable signal.
// In hardware, a full counter comparison is used to generate a ~1 second enable pulse.
// In simulation, a lower counter bit is selected to reduce simulation time.
// This approach preserves functional correctness while accelerating simulation.


## 🔹 FPGA Verification

The design was successfully implemented and tested on the PYNQ-ZU FPGA.  
LED output confirms correct detection of the target sequence.
## ILA Debug Setup

Signals probed using ILA:
- clock
- rst_sync
- x_sync
- pstate
- nstate
- y

ILA was used to confirm correct state transitions and output assertion.
Debug paths were excluded from timing analysis using false-path constraints.
<img width="977" height="882" alt="image" src="https://github.com/user-attachments/assets/d64ddd4d-0d75-4ae0-b166-8deb8492c10b" />
## ILA Result 
<img width="1920" height="1080" alt="Screenshot (1389)" src="https://github.com/user-attachments/assets/b71774c1-93af-4081-b9eb-549fb8af13c6" />

---

## 🔹 Timing Analysis Note

Minor hold-time warnings may appear when the ILA core is included.  
These warnings originate from debug-only paths and **do not affect functional correctness**.  
The design operates correctly on FPGA hardware.

---

## 🔹 Tools Used

- Vivado Design Suite
- Verilog HDL
- Integrated Logic Analyzer (ILA)
- PYNQ-ZU FPGA Board

---

## 🔹 Author

**Krishna Kumar Sahu**  
VLSI & Embedded Systems  

---

## 🔹 License




