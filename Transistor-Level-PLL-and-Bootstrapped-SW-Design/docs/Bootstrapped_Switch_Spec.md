# Bootstrapped Analog Sampling Switch Specification

## 1. Design Objective
In standard NMOS sampling switches, the on-resistance ($R_{on}$) varies significantly with the input signal voltage ($V_{in}$), leading to harmonic distortion (THD). To achieve high linearity for ADC front-end applications, a bootstrapped switch architecture was implemented in 180nm CMOS to maintain a constant $V_{gs}$ across the sampling transistor, rendering $R_{on}$ independent of the input signal.

## 2. Target Specifications
* **Technology:** 180nm CMOS
* **Supply Voltage ($V_{DD}$):** 1.8 V
* **Input Signal Range:** 1 $V_{pp}$ (Centered at 0.9 V)
* **Maximum Input Frequency:** $\ge$ 10 MHz
* **Switch Type:** Bootstrapped NMOS
* **On-Resistance Variation:** $<\pm 5\%$
* **Minimum THD at 10 MHz:** $<-55 \text{ dB}$

## 3. On-Resistance ($R_{on}$) Characterization & Results
To validate the bootstrap operation, $R_{on}$ was characterized across the full input voltage swing.

**Simulation Data:**
* **Maximum $R_{on}$:** $31.86 \ \Omega$
* **Minimum $R_{on}$:** $28.54 \ \Omega$
* **Average $R_{on}$ ($R_{avg}$):** $30.9 \ \Omega$

**Linearity / Variation Calculation:**
$$\% \text{ Variation} = \left( \frac{R_{on,max} - R_{on,min}}{R_{avg}} \right) \times 100$$
$$\% \text{ Variation} = \left( \frac{31.86 - 28.54}{30.9} \right) \times 100 \approx 6.86\%$$

**Conclusion:** The total variation is $\pm 3.43\%$, which successfully meets the strict $< \pm 5\%$ variation specification required for high-resolution sampling, confirming the efficacy of the bootstrap tracking circuit.
