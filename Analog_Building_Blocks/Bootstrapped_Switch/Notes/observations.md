# Technical Design Insights & Observations

This document details key engineering observations and trade-offs identified during the design, simulation, and optimization of the bootstrapped switch:

## 1. Bootstrap Capacitor ($C_b$) Sizing
- Sizing the bootstrap capacitor represents a trade-off between gate charge transfer and parasitic load:
  - If $C_b$ is too small, charge sharing with the parasitic gate capacitance of $M_1$ and routing parasitics will degrade the boosted gate voltage ($V_G < V_{in} + V_{DD}$), increasing $R_{on}$ variation and THD.
  - If $C_b$ is too large, it incurs significant silicon area penalties and increases the dynamic power consumption associated with cyclic charging.
  - A nominal capacitance of **$2.0\text{ pF}$** was selected, ensuring perfect gate charge transfer with minimal layout footprint.

## 2. Reliability & Voltage Stress
- During the tracking phase, the gate voltage of $M_1$ rises to $V_{in} + V_{DD} \approx 2.7\text{ V} - 3.2\text{ V}$.
- Standard 180 nm devices typically experience high electric field stress if $V_{GS}$ or $V_{GD}$ exceeds the nominal supply limit ($1.8\text{ V}$).
- In this design, although the absolute gate voltage ($V_G$) is boosted above the supply rail, the transient Gate-Source voltage ($V_{GS}$) of the main transistor $M_1$ is held constant at $V_{DD} = 1.8\text{ V}$. This ensures that no individual transistor experiences excessive voltage stress ($V_{GS} \le V_{DD}$ and $V_{GD} \le V_{DD}$), guaranteeing high operational reliability and preventing gate-oxide breakdown.
