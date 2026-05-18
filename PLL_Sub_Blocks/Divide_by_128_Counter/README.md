# Divide-by-128 Frequency Divider

## Overview
The Divide-by-128 counter is the feedback frequency divider in the PLL loop. It divides the VCO output clock by a factor of 128, generating the feedback signal that is compared against the reference clock by the Phase Frequency Detector. This enables the PLL to lock the VCO at 128× the reference frequency.

The divider is implemented as a cascade of **seven D flip-flop toggle stages**, each dividing the frequency by 2, resulting in an overall division ratio of $2^7 = 128$.

---

## Design Specifications

| Parameter | Value |
|-----------|-------|
| Division Ratio | 128 ($2^7$) |
| Number of Stages | 7 |
| Supply Voltage ($V_{DD}$) | 1.8 V |
| Technology | UMC 180 nm |
| Implementation | Cascaded toggle flip-flops |

---

## Circuit Architecture

### Cadence Schematic
![Cadence Divider Schematic](schematics/cadence_schematic.png)

---

## Operating Principle

Each D flip-flop is configured in **toggle mode** (Q-bar fed back to D input). When clocked:
- Each stage halves the frequency of its input.
- Seven cascaded stages produce:
$$f_{out} = \frac{f_{VCO}}{2^7} = \frac{f_{VCO}}{128}$$

The output of the final stage is the feedback clock fed into the PFD.

---

## Simulation & Validation Results

### Transient / Timing Response
![Divider Transient Response](plots/transient_response.png)

### Timing Diagram
![Divider Timing Diagram](timing/timing_diagram.png)

### Validation Summary
- Division by 128 verified against VCO input frequency.
- Output frequency confirmed as $f_{VCO}/128$.
- Proper toggling behavior observed across all seven stages.

---

## Observations
1. Seven cascaded DFF toggle stages achieve $\div 128$ cleanly.
2. The output duty cycle is 50%, which is suitable for PFD operation.
3. Propagation delay accumulates across stages; timing margin must be verified at maximum VCO frequency.
4. Power consumption scales with operating frequency.

---

## Applications
- PLL feedback divider
- Frequency synthesis
- Clock division in digital systems
