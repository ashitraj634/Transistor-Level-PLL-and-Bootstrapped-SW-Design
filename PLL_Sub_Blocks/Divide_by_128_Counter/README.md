# Divide-by-128 Frequency Divider

## Overview
The Divide-by-128 Frequency Divider is a critical feedback component of the PLL loop. It divides the high-frequency output clock of the Voltage Controlled Oscillator (VCO) by a factor of 128 to generate a low-frequency feedback clock ($f_{fb} = f_{VCO} / 128$). This feedback signal is compared against the reference clock by the Phase Frequency Detector (PFD), allowing the PLL to lock the VCO at exactly 128 times the reference clock frequency.

The architecture is implemented using SCL 180 nm CMOS technology by cascading **seven D flip-flop (DFF) toggle stages** in series ($2^7 = 128$).

---

## Design Specifications

| Parameter | Value |
|-----------|-------|
| Technology Node | SCL 180 nm CMOS |
| Supply Voltage ($V_{DD}$) | 1.8 V |
| Division Ratio | 128 ($2^7$) |
| Architecture | 7-stage cascaded DFF toggle counter |
| Input Clock Frequency | VCO Output Clock ($f_{VCO}$) |
| Output Clock Frequency | Feedback Clock ($f_{fb} = f_{VCO}/128$) |
| Design Tool | Cadence Virtuoso |

---

## Circuit Architecture

The frequency divider is constructed using seven D-type flip-flops (DFF) configured in **toggle mode** (where the inverting output $\bar{Q}$ is fed back to the $D$ input). 
- Stage 1 divides the input frequency by 2 ($f_{VCO}/2$).
- Stage 2 divides by 4 ($f_{VCO}/4$).
- ...
- Stage 7 divides the clock by 128 ($f_{VCO}/128$).

### Cadence Schematic
The transistor-level schematic implementation showing the cascaded flip-flop chain structure in Cadence Virtuoso.

![Frequency Divider Schematic](schematics/counter_schematic.png)

### Symbol Design
The cell block symbol of the Frequency Divider used for top-level PLL system integration.

![Frequency Divider Symbol](schematics/counter_symbol.png)

---

## Layout & Physical Verification

### Layout Design
Physical layout of the complete 7-stage frequency divider. The layout is optimized to minimize propagation delay skew and interconnect mismatch between stages.

![Frequency Divider Layout](schematics/counter_layout.png)

### Physical Verification (DRC/LVS)
The physical layout was verified using Calibre DRC and LVS checks to ensure absolute compliance with the SCL 180 nm CMOS technology design rules. The validation results confirm a fully compliant, DRC-clean, and LVS-matched layout implementation.

![Calibre Layout Verification Check](schematics/counter_drc_lvs_check.png)

---

## Simulation & Validation Results

### Output Waveforms
The transient simulation plot captures the high-frequency input clock and the successive division waveforms through the toggle stages, culminating in a clean, symmetric divided-by-128 feedback output.

![Frequency Divider Output Waveforms](plots/output_waveform.png)

---

## Validation Summary

- **Correct Frequency Division**: Successfully verified divide-by-128 operation with input clocks matching the VCO frequency range.
- **Symmetric 50% Duty Cycle**: Toggling configuration ensures a highly symmetric 50% duty cycle output, optimizing PFD phase comparison.
- **Robust Logic Levels**: Confirmed full rail-to-rail voltage swings ($0\text{ V} - 1.8\text{ V}$) across all cascaded divider stages.
- **DRC/LVS-Clean Design**: Layout verified with zero rule violations, ready for tape-out.

---

## Observations & Inferences

1. Cascading 7 DFF toggle stages provides a robust, asynchronous binary division ratio of 128.
2. Toggling logic automatically produces a 50% duty cycle clock output from any input duty cycle.
3. Propagation delay accumulates through the asynchronous cascaded chain; timing margins have been verified to prevent setup/hold violations at maximum VCO operating frequencies.
4. Active power scales linearly with the frequency, with the first toggle stage consuming the largest dynamic power portion.

---

## Applications
- Phase-Locked Loops (PLL) feedback clock division
- Clock distribution and management networks
- High-frequency digital counters
