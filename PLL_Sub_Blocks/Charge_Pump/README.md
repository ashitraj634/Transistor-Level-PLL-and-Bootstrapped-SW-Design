# Charge Pump

## Overview
The Charge Pump (CP) is designed to convert digital control pulses (**UP** and **DOWN**) from the Phase Frequency Detector (PFD) into analog current and voltage changes. This current charges or discharges the loop filter capacitor to adjust the VCO control voltage ($V_{ctrl}$), correcting any phase or frequency error in the PLL system.

The design has been implemented in SCL 180 nm CMOS technology, verified through layout design rule check (DRC), and fully validated using transient analysis in Cadence Virtuoso.

---

## Design Specifications

| Parameter | Value |
|-----------|-------|
| Technology Node | SCL 180 nm CMOS |
| Supply Voltage ($V_{DD}$) | 1.8 V |
| Input Signals | UP, DOWN (from PFD) |
| Output Nodes | OUT1, OUT2 |
| Active Blocks | Current source/sink branches, control switches |
| Tool Environment | Cadence Virtuoso, Calibre |

---

## Circuit Architecture

The charge pump circuit architecture consists of:
- **UP/DOWN Input Signals**: Receives digital control pulses from the PFD.
- **Current Source/Sink Branches**: PMOS current sources (charging path) and NMOS current sinks (discharging path).
- **Control Circuitry**: Inverter and switch structures to toggle charging/discharging branches.
- **Output Nodes**: OUT1 and OUT2 connected to capacitive loads to monitor voltage transitions.

### Cadence Schematic
The transistor-level schematic implementation showing the charge pump architecture, current source structures, and signal control pathways.

![Charge Pump Schematic](schematics/cp_schematic.png)

### Symbol Design
The structural block symbol used for higher-level hierarchical PLL integration.

![Charge Pump Symbol](schematics/cp_symbol.png)

### Testbench Setup
The simulation testbench used to verify charging, discharging, and hold behavior.

![Charge Pump Testbench](schematics/cp_testbench.png)

---

## Layout & Physical Verification

### Layout Design
Transistor-level layout implementation of the Charge Pump showing symmetrical routing of current-steering transistors to minimize mismatches.

![Charge Pump Layout](schematics/cp_layout.png)

### Physical Verification (DRC)
Verified using Calibre DRC to ensure absolute compliance with SCL 180 nm technology design rules. The validation results confirm a DRC-clean design with zero errors.

![Charge Pump DRC](schematics/cp_layout_drc.png)

---

## Simulation & Validation Results

### Output Characteristics & Transient Response
The transient simulation plots verify the voltage transition characteristics, current response behavior, and charge/discharge operations:
- **Charging operation**: UP signal active, increasing the output voltage.
- **Discharging operation**: DOWN signal active, decreasing the output voltage.
- **Hold condition**: When both UP and DOWN are inactive, the output voltage remains highly stable.
- **Minimal output ripple**: Verified minimal switching noise and charge sharing effects.

![Charge Pump Transient Response](plots/transient_response.png)

---

## Validation Summary

- **Correct Charging Operation**: Asserting the UP control pulse forces current into the load, successfully increasing output voltage.
- **Correct Discharging Operation**: Asserting the DOWN control pulse pulls current out, successfully decreasing output voltage.
- **Stable Hold Condition**: Holds the loop filter control voltage with negligible leakage when both inputs are inactive.
- **Minimal Output Ripple**: Exhibits low charge injection, clock feedthrough, and voltage ripples.
- **DRC-Clean Implementation**: Fully verified layout with zero design rule violations.

---

## Observations & Inferences

1. The charge pump circuit operates correctly by converting PFD control pulses (UP and DOWN) into corresponding analog voltage and current changes.
2. UP pulses increase the output voltage, DOWN pulses decrease the output voltage, and a stable output condition is achieved when both inputs are disabled.
3. Transistor matching between the charging (PMOS) and discharging (NMOS) current sources is key to minimizing static phase offset in the PLL.
4. Minimal output ripple verifies low charge injection and layout parasitics.

---

## Applications
- Phase-Locked Loops (PLL)
- Loop filter control
- High-performance frequency synthesis circuits
