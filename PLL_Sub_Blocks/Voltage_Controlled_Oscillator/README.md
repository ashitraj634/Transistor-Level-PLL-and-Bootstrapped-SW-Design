# Voltage Controlled Oscillator (VCO)

## Overview
The Voltage Controlled Oscillator (VCO) is the frequency-generating core of the PLL. It produces an output clock whose frequency is controlled by the input control voltage ($V_{ctrl}$) from the loop filter. The VCO is implemented as a **current-starved ring oscillator**, where the oscillation frequency is set by the bias current flowing through each inverter stage.

---

## Design Specifications

| Parameter | Value |
|-----------|-------|
| Supply Voltage ($V_{DD}$) | 1.8 V |
| PMOS Width ($W_p$) | 100 μm |
| NMOS Width ($W_n$) | 50 μm |
| Technology | UMC 180 nm |
| Architecture | Current-starved ring oscillator |

---

## Circuit Architecture

### Cadence Schematic
![Cadence VCO Schematic](schematics/cadence_schematic.png)

---

## Operating Principle

In a current-starved ring oscillator:
- The control voltage $V_{ctrl}$ sets the bias current through stacked PMOS and NMOS current sources flanking each inverter.
- Higher $V_{ctrl}$ → higher bias current → faster charging/discharging of node capacitances → **higher oscillation frequency**.
- Lower $V_{ctrl}$ → lower bias current → **lower oscillation frequency**.
- An odd number of inverter stages ensures sustained oscillation.

---

## Simulation & Validation Results

### Tuning Characteristic (Frequency vs. $V_{ctrl}$)
![VCO Tuning Curve](plots/tuning_curve.png)

### Transient Oscillation
![VCO Transient Response](plots/transient_response.png)

### Validation Summary
- Oscillation verified across the target frequency range.
- Monotonic frequency-voltage tuning characteristic confirmed.
- Transistor sizing ($W_p = 100\ \mu\text{m}$, $W_n = 50\ \mu\text{m}$) provides wide tuning range to overcome PVT variations.

---

## Observations
1. Current-starved topology provides a wide and linear tuning range.
2. Transistor width sizing balances drive strength and power consumption.
3. Ring oscillator frequency is sensitive to supply voltage variations; robust biasing is critical.
4. An odd number of stages is required to sustain oscillation.

---

## Applications
- PLL frequency synthesis
- Clock generation circuits
- Frequency modulation
