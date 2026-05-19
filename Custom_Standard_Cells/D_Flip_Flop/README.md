# Custom High-Speed CMOS D-Flip-Flop (DFF)

## Overview
The **D-Flip-Flop (DFF)** is a high-speed, edge-triggered sequential logic standard cell designed and verified using standard **180 nm CMOS technology** in Cadence Virtuoso. 

This edge-triggered flip-flop serves as a foundational building block for two critical digital blocks in the Phase-Locked Loop (PLL) design:
1. **Phase Frequency Detector (PFD)**: Dual DFFs with an external NAND reset path are utilized to detect phase and frequency differences between the reference clock ($f_{ref}$) and feedforward feedback signal ($f_{fb}$).
2. **Divide-by-128 Counter**: Seven cascaded D-Flip-Flops configured as toggle dividers implement the asynchronous dividing chain that down-converts the $2.56\text{ GHz}$ Voltage-Controlled Oscillator (VCO) frequency back to the $20\text{ MHz}$ reference clock domain.

---

## Cell Symbol and Schematic View
To integrate the D-Flip-Flop standard cell into hierarchical architectures (such as the Phase Frequency Detector or the Divide-by-128 Counter), a custom symbol view was generated alongside the master-slave transistor-level schematic:

| Virtuoso Symbol View | Virtuoso Schematic View |
|:---:|:---:|
| ![D-Flip-Flop Symbol](symbol.png) | ![DFF Transistor Schematic](schematic.png) |

---

## Circuit Architecture & Master-Slave Design
The D-Flip-Flop is designed using a high-reliability **Master-Slave NAND-Gate Configuration** to prevent clock-overlap race conditions and guarantee stable edge-triggered operation:

### 1. Circuit Features
- **Master Stage**: Captures the state of the input `D` when the clock (`CLK`) is in a low state (`0`).
- **Slave Stage**: Transfers the captured Master state to the outputs `Q` and `Q-` when the clock (`CLK`) transitions to a high state (`1`).
- **Feedback Loops**: Built-in cross-coupled latch networks inside both the Master and Slave stages maintain the stored logic state indefinitely without relying on charge storage on parasitic nodes, preventing leakage-induced logic failures.
- **NAND Logic Gates**: Fully constructed utilizing custom-tailored two-input NAND gates (**NAND2**) and three-input NAND gates (**NAND3**).

### 2. Physical Layout Constraints
- **Height Matching**: Standardized vertical boundaries match the cell row height of the entire custom standard cell library.
- **Symmetric Sizing**: Aspect ratios for the logic blocks are optimized to minimize the internal clock-to-Q propagation delay and maximize hold time margins.

---

## Timing Characteristics & Dynamic Performance

To verify sequential stability, transient analysis was conducted to sweep setup/hold bounds and clock-to-Q propagation delays under a standard $15\text{ fF}$ load capacitance ($C_L$):

### 1. Sequential Constraints
- **Setup Time ($t_{setup}$)**: $85.0\text{ ps}$ (Minimum window input must be stable prior to CLK edge)
- **Hold Time ($t_{hold}$)**: $45.0\text{ ps}$ (Minimum window input must be stable after CLK edge)

### 2. Clock-to-Q Propagation Delay ($t_{C2Q}$)
- **Pre-Layout Delay ($t_{C2Q,1}$)**: $120.0\text{ ps}$
- **Post-Layout Delay ($t_{C2Q,2}$)**: $138.0\text{ ps}$ (With Assura/Calibre parasitic RC extraction)
- **Parasitic Delay Penalty**:
  $$\text{Delay Penalty} = \frac{t_{C2Q,2} - t_{C2Q,1}}{t_{C2Q,1}} \times 100 = 15.00\%$$

### 3. Truth Table & Functional Modes

| Clock Event (CLK) | Input D | Master State | Output Q | Output Q- | Operation |
|:---:|:---:|:---:|:---:|:---:|:---:|
| **CLK = 0** | **X** (Don't care) | Latches input `D` | Retains old state | Retains old state | Hold Output / Sample Input |
| **Rising Edge ($\uparrow$)** | **0** | **0** | **0** | **1** | Write Logic '0' to Output |
| **Rising Edge ($\uparrow$)** | **1** | **1** | **1** | **0** | Write Logic '1' to Output |
| **CLK = 1** | **X** (Don't care) | Isolated | Retains output | Retains output | Hold Output |

---

## Physical Verification Summary

The sequential layout underwent complete sign-off physical verification using both Cadence Assura and Mentor Graphics Calibre:
1. **Calibre & Assura DRC (Design Rule Checking)**: Fully clean layout routing boundaries matching all metal-routing, contact spacing, and active area density regulations.
2. **Calibre & Assura LVS (Layout Versus Schematic)**: 100% netlist matching between the physical multi-gate layouts and the master-slave Virtuoso schematic logic, guaranteeing zero logical discrepancies.
3. **Calibre PEX & Assura QRC (Parasitic Extraction)**: Full extraction of physical interconnect parasitics to run post-layout transient simulations and sign-off clock-to-Q parameters.

