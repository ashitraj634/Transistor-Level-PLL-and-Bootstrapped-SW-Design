# Phase-Locked Loop (PLL) Architecture & Calculations

## 1. System Level Specifications
* **Target Output Frequency ($f_{out}$):** 2.56 GHz
* **Reference Frequency ($f_{ref}$):** 20 MHz
* **Feedback Divider Ratio ($N$):** 128
* **Supply Voltage ($V_{DD}$):** 1.8 V
* **Charge Pump Current ($I_{cp}$):** 100 µA - 150 µA

## 2. Voltage Controlled Oscillator (VCO) Characterization
The VCO is implemented as a current-starved ring oscillator. Transistor sizing was optimized to $W_p = 100 \mu m$ and $W_n = 50 \mu m$ to achieve a wide tuning range capable of overcoming PVT variations.

**Extracted Frequency Range:**
* $f_{max} = 4.09 \text{ GHz}$ at $V_{ctrl\_max} = 1.8 \text{ V}$
* $f_{min} = 382.95 \text{ MHz}$ at $V_{ctrl\_min} = 600 \text{ mV}$
* **Center Frequency ($f_{center}$):** $2.23 \text{ GHz}$
* **Tuning Range:** $165.75\%$

## 3. Passive Loop Filter
A Type-II passive loop filter was designed to integrate the charge pump current packets into a stable control voltage ($V_{ctrl}$), while suppressing ripple to minimize deterministic jitter.
* **Resistor ($R$):** $1 \text{ k}\Omega$
* **Capacitor ($C_1$):** $277 \text{ pF}$
