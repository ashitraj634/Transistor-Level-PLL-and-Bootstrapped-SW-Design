# Transistor-Level PLL & Bootstrapped Switch Design

![Foundry Nodes](https://img.shields.io/badge/Foundry_Nodes-180nm%20%7C%2090nm-blue)
![EDA Tool](https://img.shields.io/badge/EDA-Cadence_Virtuoso%20%7C%20Spectre-red)
![Verification](https://img.shields.io/badge/Verification-DRC%20%7C%20LVS%20%7C%20RCX-success)

## Overview
This repository contains a full-custom, transistor-level Mixed-Signal IP library, culminating in the physical design and verification of a **2.56 GHz Charge-Pump Phase-Locked Loop (CPPLL)** and a high-linearity **Bootstrapped Analog Sampling Switch**. 

Every component - from fundamental logic gates to complex analog amplifiers - was designed from scratch. To ensure robust performance and technology portability, the blocks were characterized and validated across three distinct Process Design Kits (PDKs): **180nm SCL**, **180nm UMC**, and **90nm GPDK**.

---

## Repository Directory Structure

* **[PLL Top-Level System Integration](PLL_Design/Top_Level_Integration/README.md)**: Integrated closed-loop schematic, system layout, transient locking waveforms, and Calibre DRC/LVS physical verification check.
* **[PLL Design Sub-Blocks](PLL_Design/Sub_Blocks/)**:
  * **[Phase Frequency Detector (PFD)](PLL_Design/Sub_Blocks/Phase_Frequency_Detector/README.md)**: PFD schematic, D-flip-flop layout, transient simulation, and DRC physical verification.
  * **[Charge Pump (CP)](PLL_Design/Sub_Blocks/Charge_Pump/README.md)**: Transistor-level schematic, current branch mirror switches, physical layout, Calibre DRC, and transient charge/discharge simulation.
  * **[Voltage Controlled Oscillator (VCO)](PLL_Design/Sub_Blocks/Voltage_Controlled_Oscillator/README.md)**: Current-starved ring oscillator schematic, symbol, LVS/DRC physical verification, and control voltage frequency tuning range characterization curves.
  * **[Divide-by-128 Frequency Counter](PLL_Design/Sub_Blocks/Divide_by_128_Counter/README.md)**: Cascaded 7-stage DFF asynchronous division schematic, layout, Calibre DRC/LVS verification checks, and frequency scaling transient plots.
* **[Bootstrapped Analog Sampling Switch](Bootstrapped_Switch/README.md)**: High-linearity sampling gate schematic, dynamic gate-boosting waveforms, on-resistance uniformity parameters, and spectral FFT harmonic distortion verification.

---

## 1. Top-Level PLL Specifications & Performance
The CPPLL integrates a custom Phase Frequency Detector, Charge Pump, passive Type-II Loop Filter, Current-Starved VCO, and a synchronous Divide-by-N Counter.

### PLL Block-Level Circuit Diagram
The functional schematic below illustrates the control interfaces, current-steering switches, and the passive Loop Filter network ($R=1\text{ k}\Omega$, $C=277\text{ pF}$) of the integrated system:

![PLL Block-Level Circuit Diagram](PLL_Design/Top_Level_Integration/pll_block_diagram.png)

### Performance Specs Summary
| Parameter | Value | Unit | Conditions |
| :--- | :--- | :--- | :--- |
| **Output Frequency** | 2.56 | GHz | Locked State |
| **Reference Clock** | 20 | MHz | Input Domain |
| **Divide Ratio (N)** | 128 | - | Integer-N |
| **VCO Tuning Range** | 0.38 - 4.09 | GHz | Vctrl = 0.6V to 1.8V |
| **VCO Gain (Kvco)** | 2.15 x 10^10 | rad/s/V | Linear Region |
| **Charge Pump Current**| 100 - 150 | uA | Programmable |
| **Loop Filter** | R = 1k, C = 277p| Ohm, F | Passive Configuration |

---

## 2. [Bootstrapped Sampling Switch](Bootstrapped_Switch/README.md)
Designed for high-speed ADC front-ends to eliminate input-dependent on-resistance ($R_{on}$) modulation. 
* **Performance:** Maintains a highly constant $V_{gs}$ across the sampling transistor, achieving a total $R_{on}$ variation of just **$\pm 3.43\%$** across a 1 $V_{pp}$ input swing at 10 MHz.

---

## 3. IP Sub-Block Architecture

### [Custom Standard Cell Library](Custom_Standard_Cells/README.md)
To construct the digital boundaries of the PLL (PFD and N-Counter), a fully custom standard cell library was developed, physically laid out, and RC-extracted.
* **Inverter:** Extracted [parasitic layout analysis](Custom_Standard_Cells/Inverter/README.md) demonstrated a 15.67% increase in propagation delay (33.67 ps to 38.94 ps) due to physical routing parasitics.
* **Logic Gates:** Custom NAND2 and NAND3 gates.
* **D-Flip-Flop:** High-speed DFFs utilized in the synchronous N-Counter chain.

### Voltage Controlled Oscillator (VCO)
A multi-stage current-starved ring oscillator. Transistor aspect ratios ($W_p = 100\ \mu\text{m}$, $W_n = 50\ \mu\text{m}$) were heavily optimized using $g_m/I_D$ design methodologies to achieve a massive 165.75% tuning range.

### [Analog Building Blocks](Analog_Building_Blocks/README.md)
Independent analog IP blocks designed for low-power operation and ADC/PLL integration:
* **Amplifiers:** [Common Source](Analog_Building_Blocks/Amplifiers/Common_Source/README.md) (100 MHz GBW) and [Cascode Amplifiers](Analog_Building_Blocks/Amplifiers/Cascode/README.md) (20 dB gain, 200 MHz bandwidth at 1 mW).
* **Current Mirrors:** [Simple and Cascode current mirrors](Analog_Building_Blocks/Current_Mirrors/README.md) engineered for high output resistance (100 uA - 500 uA).

---

## 4. Design Methodology & Verification
* **Device Characterization:** Extensive extraction of $g_m/I_D$, channel length modulation ($\lambda \approx 0.189$ for NMOS), transit frequency ($f_T$), and body effect dependencies ($\gamma$) prior to architecture design.
* **Physical Design:** Full-custom layout routing for sub-blocks and the top-level PLL.
* **Sign-off Verification:** Strict Calibre DRC (Design Rule Check) and LVS (Layout Versus Schematic) compliance.
