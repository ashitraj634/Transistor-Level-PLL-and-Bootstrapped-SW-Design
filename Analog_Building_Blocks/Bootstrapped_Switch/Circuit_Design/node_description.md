# Circuit Architecture & Node Descriptions

To understand the operational mechanics of the bootstrapped switch, the schematic diagram below illustrates the interconnection of the main NMOS sampling transistor, the auxiliary clock-steering switches, and the bootstrap capacitor ($C_b$):

![Bootstrapped Switch Circuit Schematic](schematic.png)

---

## Detailed Transistor-Level Component Breakdown

- **$M_1$ (Main Sampling Switch)**: 
  - *Type / Sizing*: High-speed, thin-oxide NMOS device. Sized with a wide channel width ($W/L$) to achieve a low nominal triode resistance ($\approx 30\ \Omega$).
  - *Function*: Routes the analog input signal $V_{in}$ to the load capacitor $C_1$ during the tracking phase. It is the primary gate switch that requires a highly constant overdrive voltage.
- **$M_2$ (Input Tracking Transistor)**: 
  - *Function*: Connects the bottom plate of $C_b$ (node Q) to the input signal $V_{in}$ during the tracking phase ($CK = 1$). This forces the capacitor bottom plate to ride on the input signal.
- **$M_3$ (Gate Boost Transistor)**: 
  - *Function*: Acts as the switch that transfers the boosted charge from the top plate of $C_b$ (node P) to the gate of $M_1$ (node A) during $CK = 1$. It connects the pre-charged floating voltage source directly across the Gate-Source of $M_1$.
- **$M_4$ (Bottom Plate Clamping Switch)**: 
  - *Function*: Connects the bottom plate of $C_b$ (node Q) to ground during the hold phase ($CK = 0$). This establishes a ground reference to allow charging of the capacitor from $V_{DD}$.
- **$M_5$ (Top Plate Charging Switch)**: 
  - *Function*: Connects the top plate of $C_b$ (node P) to the $V_{DD}$ rail during $CK = 0$. In tandem with $M_4$, it pre-charges the bootstrap capacitor to $V_{DD} = 1.8\text{ V}$.
- **$M_6$ (Gate Clamping Switch)**: 
  - *Function*: Pulls the gate of the main switch ($M_1$) to ground during the hold phase ($CK = 0$). This guarantees that the main switch is completely turned off and prevents signal feedthrough during the hold state.

---

## Critical Internal Nodes

- **Node A (Gate of $M_1$)**:
  - *Behavior*: The primary gate control node. During $CK = 0$, it is clamped to ground ($0\text{ V}$). During $CK = 1$, it is boosted up to $V_{in} + V_{DD}$, reaching up to $2.7\text{ V} - 3.2\text{ V}$ to maintain $V_{GS} \approx V_{DD}$.
- **Node P (Top Plate of $C_b$)**:
  - *Behavior*: Serves as the high-potential terminal of the bootstrap capacitor. Clamped to $1.8\text{ V}$ ($V_{DD}$) during the hold phase, and boosted to $V_{in} + V_{DD}$ during the tracking phase.
- **Node Q (Bottom Plate of $C_b$)**:
  - *Behavior*: Serves as the tracking reference terminal. Tied to ground ($0\text{ V}$) during $CK = 0$ to permit charging. Connected directly to $V_{in}$ during $CK = 1$ to ride the input potential.
