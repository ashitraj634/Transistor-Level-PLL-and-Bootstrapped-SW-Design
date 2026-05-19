# Circuit Architecture & Node Descriptions

This document describes the function of each transistor and critical internal node within the bootstrapped switch schematic:

## Transistor Descriptions

- **$M_1$ (Main Sampling Switch)**: High-speed NMOS switch. Sized with a large aspect ratio to minimize absolute on-resistance, while balancing parasitic source/drain capacitances.
- **$M_2$ (Input Tracking Control)**: Connects the bottom plate of $C_b$ (node Q) to the input signal $V_{in}$ during $CK = 1$, allowing the capacitor voltage to ride on the input.
- **$M_3$ (Gate Boost Switch)**: Connects the top plate of $C_b$ (node P) to the gate of $M_1$ (node A) during $CK = 1$, transferring the boosted charge.
- **$M_4$ (Bottom Plate Grounding)**: Connects the bottom plate of $C_b$ (node Q) to ground during the hold phase ($CK = 0$) to allow charging.
- **$M_5$ (Top Plate VDD Connection)**: Connects the top plate of $C_b$ (node P) to $V_{DD}$ during the hold phase ($CK = 0$) to charge the capacitor to $V_{DD}$.
- **$M_6$ (Gate Grounding Switch)**: Pulls the gate of the main switch ($M_1$) to ground during the hold phase ($CK = 0$), turning it off completely.

## Critical Internal Nodes

- **Node A (Gate of $M_1$)**: The gate control node of the main switch. During the tracking phase, it is boosted to $V_{in} + V_{DD}$ (up to $2.7\text{ V} - 3.2\text{ V}$). During the hold phase, it is pulled to ground.
- **Node P (Top Plate of $C_b$)**: Clamped to $V_{DD}$ during $CK = 0$. Boosted to $V_{in} + V_{DD}$ during $CK = 1$.
- **Node Q (Bottom Plate of $C_b$)**: Clamped to ground during $CK = 0$. Directly tracks the input signal $V_{in}$ during $CK = 1$.
