# Two-Input CMOS NAND Gate (NAND2)

## Overview
The **NAND2** standard cell is a fundamental two-input logic gate designed and verified using standard **180 nm CMOS technology** in Cadence Virtuoso. 

This cell serves as the primary logical block for building edge-triggered flip-flops and decision-making logic inside the high-performance digital boundaries of the Phase-Locked Loop (PLL), specifically in the Phase Frequency Detector (PFD) and frequency divider blocks.

---

## Transistor-Level Circuit Schematic
The full-custom transistor-level schematic capture of the NAND2 cell in Cadence Virtuoso:

![NAND2 Transistor Schematic](schematic.png)

---

## Circuit Architecture & Transistor Sizing
The NAND2 cell consists of a pull-up network comprising two PMOS transistors connected in parallel to $V_{DD}$, and a pull-down network consisting of two NMOS transistors stacked in series to $V_{SS}$:

### Transistor Dimensions (180 nm Node):
- **PMOS Transistors ($M_0, M_1$)**:
  - **Width ($W_p$)**: $0.42\ \mu\text{m}$ ($420\text{ nm}$)
  - **Length ($L_p$)**: $0.18\ \mu\text{m}$ ($180\text{ nm}$)
  - **Multiplier ($m$)**: 1
- **NMOS Transistors ($M_2, M_3$)**:
  - **Width ($W_n$)**: $0.42\ \mu\text{m}$ ($420\text{ nm}$)
  - **Length ($L_n$)**: $0.18\ \mu\text{m}$ ($180\text{ nm}$)
  - **Multiplier ($m$)**: 1

### Sizing Rationale:
- NMOS transistors stacked in series suffer from increased channel resistance. To establish symmetrical propagation rise ($t_{PLH}$) and fall ($t_{PHL}$) delays and maximize noise margin, the transistor aspect ratios are sized symmetrically with a $W_p / W_n$ ratio optimized to compensate for the lower mobility of holes relative to electrons, while matching stacked resistance parameters.

---

## Logical Truth Table

| Input A | Input B | PMOS Status | NMOS Status | Output (OUT) |
|:---:|:---:|:---:|:---:|:---:|
| **0** | **0** | $M_0$ ON, $M_1$ ON | $M_2$ OFF, $M_3$ OFF | **1** ($V_{DD}$) |
| **0** | **1** | $M_0$ ON, $M_1$ OFF | $M_2$ ON, $M_3$ OFF | **1** ($V_{DD}$) |
| **1** | **0** | $M_0$ OFF, $M_1$ ON | $M_2$ OFF, $M_3$ ON | **1** ($V_{DD}$) |
| **1** | **1** | $M_0$ OFF, $M_1$ OFF| $M_2$ ON, $M_3$ ON | **0** ($V_{SS}$) |

---

## Verification & Sign-Off
1. **Spectre Simulation**: The cell was characterized for transient rise, fall, and propagation delays, validating fast transition boundaries.
2. **Physical Layout Compliance**: Ready for full-custom layout with matched grid constraints, Calibre DRC (Design Rule Checking), and LVS (Layout Versus Schematic) physical validation.
