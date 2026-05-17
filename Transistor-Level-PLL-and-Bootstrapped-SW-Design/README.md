# Transistor-Level PLL & Bootstrapped Switch Design

![Foundry Nodes](https://img.shields.io/badge/Foundry_Nodes-180nm%20%7C%2090nm-blue)
![EDA Tool](https://img.shields.io/badge/EDA-Cadence_Virtuoso%20%7C%20Spectre-red)
![Verification](https://img.shields.io/badge/Verification-DRC%20%7C%20LVS%20%7C%20RCX-success)

## Overview
This repository contains a full-custom, transistor-level Mixed-Signal IP library, culminating in the physical design and verification of a **2.56 GHz Charge-Pump Phase-Locked Loop (CPPLL)** and a high-linearity **Bootstrapped Analog Sampling Switch**. 

Every component—from fundamental logic gates to complex analog amplifiers—was designed from scratch. To ensure robust performance and technology portability, the blocks were characterized and validated across three distinct Process Design Kits (PDKs): **180nm SCL**, **180nm UMC**, and **90nm GPDK**.

## 1. Top-Level PLL Specifications & Performance
The CPPLL integrates a custom Phase Frequency Detector, Charge Pump, passive Type-II Loop Filter, Current-Starved VCO, and a synchronous Divide-by-N Counter.

| Parameter | Value | Unit | Conditions |
| :--- | :--- | :--- | :--- |
| **Output Frequency** | 2.56 | GHz | Locked State |
| **Reference Clock** | 20 | MHz | Input Domain |
| **Divide Ratio (N)** | 128 | - | Integer-N |
| **VCO Tuning Range** | 0.38 - 4.09 | GHz | $V_{ctrl}$ = 0.6V to 1.8V |
| **VCO Gain ($K_{vco}$)** | 2.15 $\times 10^{10}$ | rad/s/V | Linear Region |
| **Charge Pump Current**| 100 - 150 | µA | Programmable |
| **Loop Filter** | R = 1k, C = 277p| O, F | Passive Configuration |

## 2. Bootstrapped Sampling Switch
Designed for high-speed ADC front-ends to eliminate input-dependent on-resistance ($R_{on}$) modulation. 
* **Performance:** Maintains a highly constant $V_{gs}$ across the sampling transistor, achieving a total $R_{on}$ variation of just **$\pm 3.43\%$** across a 1 $V_{pp}$ input swing at 10 MHz.

## 3. IP Sub-Block Architecture

### Custom Standard Cell Library
To construct the digital boundaries of the PLL (PFD and N-Counter), a fully custom standard cell library was developed, physically laid out, and RC-extracted.
* **Inverter:** Extracted parasitic layout analysis demonstrated a 15.67% increase in propagation delay (33.67 ps to 38.94 ps) due to physical routing parasitics.
* **Logic Gates:** Custom NAND2 and NAND3 gates.
* **D-Flip-Flop:** High-speed DFFs utilized in the synchronous N-Counter chain.

### Voltage Controlled Oscillator (VCO)
A multi-stage current-starved ring oscillator. Transistor aspect ratios ($W_p$ = 100µm, $W_n$ = 50µm) were heavily optimized using $g_m/I_D$ design methodologies to achieve a massive 165.75% tuning range.

### Analog Building Blocks
Independent analog IP blocks designed for low-power operation:
* **Amplifiers:** Common Source (100 MHz GBW) and Cascode Amplifiers (20 dB gain, 200 MHz bandwidth at 1 mW).
* **Current Mirrors:** Simple and Cascode current mirrors engineered for high output resistance (100 µA - 500 µA).

## 4. Design Methodology & Verification
* **Device Characterization:** Extensive extraction of $g_m/I_D$, channel length modulation ($\lambda \approx 0.189$ for NMOS), transit frequency ($f_T$), and body effect dependencies ($\gamma$) prior to architecture design.
* **Physical Design:** Full-custom layout routing for sub-blocks and the top-level PLL.
* **Sign-off Verification:** Strict Calibre DRC (Design Rule Check) and LVS (Layout Versus Schematic) compliance.
