# Design of a Bootstrapped Analog Sampling Switch in 180 nm CMOS

## Overview
This project presents the design, implementation, and simulation of a high-linearity bootstrapped NMOS analog sampling switch in standard 180 nm CMOS technology. The primary design objective is to mitigate the signal-dependent on-resistance ($R_{on}$) modulation inherent in conventional MOS sampling gates. This architecture stabilizes the switch transconductance, minimizes harmonic distortion, and maintains high linearity across the full dynamic range for high-speed, high-resolution Analog-to-Digital Converter (ADC) front-ends.

---

## Design Objectives & Specifications
The bootstrapped switch is designed to meet strict performance boundaries to ensure compatibility with high-speed sampling front-ends. The target parameters and simulated results are summarized below:

| Performance Metric | Design Specification | Achieved Result | Status |
|:---|:---|:---|:---|
| **Technology Node** | 180 nm CMOS | 180 nm CMOS | Passed |
| **Supply Voltage ($V_{DD}$)** | 1.8 V | 1.8 V | Passed |
| **Input Signal Range** | 1.0 Vpp (centered at 0.9 V) | 1.0 Vpp (centered at 0.9 V) | Passed |
| **Maximum Input Frequency ($f_{in}$)**| >= 10 MHz | 10 MHz | Passed |
| **Switch Type** | Bootstrapped NMOS | Bootstrapped NMOS | Passed |
| **On-Resistance Variation ($\Delta R_{on}$)** | <= +/- 5% | **+/- 3.43%** | Passed |
| **Total Harmonic Distortion (THD)** | <= -55 dB | **-75.996 dB** | Passed |

---

## Theoretical Analysis & Design Concept

### The Conventional NMOS Switch Limitation
For a simple NMOS sampling switch operating in the linear (triode) region, the on-resistance ($R_{on}$) is expressed as:

$$R_{on} = \frac{1}{\mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{TH})}$$

In a conventional configuration, the gate is driven by a constant clock voltage ($V_{CLK} = V_{DD}$), while the source terminal tracks the time-varying input voltage ($V_{in}$). Consequently:

$$V_{GS}(t) = V_{DD} - V_{in}(t)$$

As the input signal oscillates, the Gate-Source overdrive voltage ($V_{GS} - V_{TH}$) fluctuates dynamically. This yields several critical performance degradations:
- Significant variation in switch resistance with input signal amplitude.
- Signal-dependent non-linear attenuation.
- High harmonic distortion in the sampled output, limiting high-resolution ADC performance.

### The Bootstrapped Switch Solution
To achieve highly linear sampling, the bootstrapped switch dynamically floats a pre-charged capacitor ($C_b$) between the gate and source terminals of the main sampling transistor ($M_1$) during the tracking phase. This maintains a nearly constant Gate-to-Source voltage:

$$V_{GS} \approx V_{DD}$$

Since $V_{GS}$ remains constant and independent of the input signal level, the switch on-resistance ($R_{on}$) remains highly uniform across the entire dynamic range, suppressing harmonic distortion.

---

## Operating Principle & Clock Phases

The operation of the bootstrapped sampling switch is divided into two distinct clock-controlled phases: the Hold Phase ($CK = 0$) and the Sampling/Tracking Phase ($CK = 1$).

### 1. Hold Phase ($CK = 0$)
When the clock signal is low, the circuit disconnects the output from the input and prepares the bootstrap capacitor ($C_b$) for the next sampling cycle:
* **Main Switch Off**: The gate of the main sampling transistor ($M_1$) is pulled to ground through auxiliary clock-controlled transistors ($M_6$). Thus, $V_{GS} \approx 0\text{ V}$, isolating the input from the output.
* **Output Hold**: The load capacitor ($C_1$) holds the previously sampled voltage.
* **Bootstrap Capacitor Charging**: The bootstrap capacitor ($C_b$) is connected between $V_{DD}$ and ground through transistors $M_5$ and $M_4$, charging it to:
  $$V_{Cb} \approx V_{DD}$$

### 2. Sampling/Tracking Phase ($CK = 1$)
When the clock signal goes high, the pre-charged bootstrap capacitor ($C_b$) is reconfigured to drive the gate of the main switch:
* **Bootstrap Reconfiguration**: Transistors $M_4$ and $M_5$ are turned off. Auxiliary transistors $M_2$ and $M_3$ turn on, referencing the bottom terminal of $C_b$ (node Q) to the input signal $V_{in}$ and connecting the top terminal of $C_b$ (node P) to the gate of the main transistor $M_1$ (node A).
* **Gate Voltage Boosting**: The gate voltage ($V_G$) is boosted above the supply rail to track the input:
  $$V_G(t) = V_{in}(t) + V_{DD}$$
* **Constant Overdrive**: The Gate-Source voltage of $M_1$ is stabilized at:
  $$V_{GS} = V_G - V_{in} = (V_{in} + V_{DD}) - V_{in} = V_{DD}$$
  This constant gate drive maintains a highly uniform triode resistance.

---

## Transistor-Level Circuit Implementation

The physical schematic of the bootstrapped switch integrates the main sampling transistor alongside five auxiliary control transistors and the bootstrap capacitor ($C_b$):

- **Main Sampling Transistor ($M_1$)**: The primary switch routing $V_{in}$ to $V_{out}$.
- **Auxiliary Network ($M_2, M_3, M_4, M_5, M_6$)**: Clocked switch network managing capacitor charging and gate boosting.
- **Bootstrap Capacitor ($C_b$)**: Energy storage element ($V_{DD}$ offset source).
- **Load Capacitor ($C_1$)**: Hold capacitor ($5\text{ pF}$) storing the sampled output.

---

## Simulation Results & Performance Verification

### 1. Output and Internal Node Waveforms
Transient simulation in Cadence Virtuoso validates correct sample-and-hold functionality:
- When $CK = 0$, the output remains perfectly stable, holding the sampled value.
- When $CK = 1$, the output tracks the $1.0\text{ }V_{pp}$ sinusoidal input ($10\text{ MHz}$) centered at $0.9\text{ V}$.
- The gate node voltage ($V_A$) rises dynamically up to $2.7\text{ V}$ ($V_{in,max} + V_{DD}$), verifying the operation of the charge-boosting network.

### 2. Total Harmonic Distortion (THD) Analysis
To quantify sampling linearity, a Fast Fourier Transform (FFT) was performed on the sampled output waveform at a $10\text{ MHz}$ input frequency. The measured fundamental and harmonic spectral components are:
- **Fundamental Amplitude ($A_1$)**: $498.2788\text{ mV}$ ($0.4982788\text{ V}$)
- **Third Harmonic ($A_3$)**: $78.09553\ \mu\text{V}$ ($78.09553 \times 10^{-6}\text{ V}$)
- **Fifth Harmonic ($A_5$)**: $13.63941\ \mu\text{V}$ ($13.63941 \times 10^{-6}\text{ V}$)

Using the definition for Total Harmonic Distortion:

$$THD_{tot} = \frac{A_3^2 + A_5^2 + \dots}{A_1^2}$$

$$THD_{tot} = \frac{(78.09553 \times 10^{-6})^2 + (13.63941 \times 10^{-6})^2}{(0.4982788)^2} = 2.53138 \times 10^{-8}$$

$$THD\text{ (dB)} = 10 \log_{10}(2.53138 \times 10^{-8}) = -75.996\text{ dB}$$

The achieved THD of **$-75.996\text{ dB}$** is significantly superior to the target design specification of $\le -55\text{ dB}$, confirming excellent linearity.

### 3. On-Resistance ($R_{on}$) Variation Analysis
To evaluate resistance stability across the input voltage range, a constant current load of $10\ \mu\text{A}$ was applied across the sampling switch:
- **Maximum On-Resistance ($R_{on,max}$)**: $31.86\ \Omega$ (at maximum input voltage)
- **Minimum On-Resistance ($R_{on,min}$)**: $28.54\ \Omega$ (at minimum input voltage)

$$R_{avg} = \frac{R_{on,max} + R_{on,min}}{2} = \frac{31.86 + 28.54}{2} = 30.9\ \Omega$$

$$\text{Total Variation} = \frac{R_{on,max} - R_{on,min}}{R_{avg}} \times 100\% = \frac{31.86 - 28.54}{30.9} \times 100\% = 6.86\%$$

The total peak-to-peak variation is $6.86\%$, which equates to a highly uniform resistance variation of **$\pm 3.43\%$**. This is well within the design constraint of $\le \pm 5\%$.

---

## Conclusion
The transistor-level bootstrapped NMOS sampling switch design satisfies all performance and physical layout constraints in SCL 180 nm CMOS technology. By stabilizing the gate-to-source drive voltage to a constant $V_{DD}$, the design achieves an on-resistance variation of only $\pm 3.43\%$ and a Total Harmonic Distortion of $-75.996\text{ dB}$ at $10\text{ MHz}$. These performance parameters verify that the proposed architecture is highly suitable for high-speed, high-resolution analog-to-digital converters.
