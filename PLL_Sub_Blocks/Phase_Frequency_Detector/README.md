# Phase Frequency Detector (PFD)

## Overview
The Phase Frequency Detector (PFD) is a key sub-block of the Phase-Locked Loop system. It compares the phase and frequency of the reference clock against the feedback clock from the frequency divider. Based on this comparison, it generates UP and DOWN control pulses that drive the charge pump to correct the VCO frequency.

The PFD is implemented using a dual-edge-triggered D flip-flop architecture with an asynchronous reset path to suppress dead-zone effects.

---

## Design Specifications

| Parameter | Value |
|-----------|-------|
| Supply Voltage ($V_{DD}$) | 1.8 V |
| Reference Frequency | — |
| Technology | UMC 180 nm |
| Output Signals | UP, DOWN |

---

## Circuit Architecture

### Cadence Schematic
![Cadence PFD Schematic](schematics/cadence_schematic.png)

---

## Operating Principle

The PFD operates on the following logic:
- If the **reference clock leads** the feedback clock → **UP pulse** is generated → Charge pump increases $V_{ctrl}$ → VCO speeds up.
- If the **feedback clock leads** the reference clock → **DOWN pulse** is generated → Charge pump decreases $V_{ctrl}$ → VCO slows down.
- When both clocks are aligned in phase and frequency → UP and DOWN pulses are simultaneously reset via the AND gate feedback → **locked state**.

---

## Simulation & Validation Results

### Timing / Transient Response
![Transient Response](plots/transient_response.png)

### Timing Diagram
![Timing Diagram](timing/timing_diagram.png)

### Validation Summary
- UP and DOWN pulse generation verified across multiple phase offsets.
- Dead-zone suppression confirmed via reset path delay.
- Lock condition verified with matched reference and feedback signals.

---

## Observations
1. The dual-DFF topology minimizes dead-zone compared to XOR-based PFDs.
2. The reset AND gate introduces a small but intentional delay to prevent dead-zone.
3. Output pulses are narrow and rail-to-rail at lock condition.

---

## Applications
- PLL frequency/phase acquisition
- Clock synchronization circuits
- CDR (Clock and Data Recovery) systems
