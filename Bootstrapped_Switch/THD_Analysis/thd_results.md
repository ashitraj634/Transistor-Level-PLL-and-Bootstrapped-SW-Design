# THD Calculation & Results

This document presents the detailed mathematical evaluation of the Total Harmonic Distortion (THD) using the extracted spectral measurements from Cadence Virtuoso:

---

## 1. Simulated FFT Spectrum
The harmonic content of the sampled output signal was evaluated by performing a Fast Fourier Transform (FFT) on the transient sampled output in Cadence Virtuoso:

![FFT Spectral Output for THD Analysis](fft_spectrum.png)

---

## 2. Mathematical Evaluation

### Extracted Spectral Amplitudes:
- **Fundamental ($A_1$)**: $498.2788\text{ mV}$ ($0.4982788\text{ V}$)
- **Third Harmonic ($A_3$)**: $78.09553\ \mu\text{V}$ ($78.09553 \times 10^{-6}\text{ V}$)
- **Fifth Harmonic ($A_5$)**: $13.63941\ \mu\text{V}$ ($13.63941 \times 10^{-6}\text{ V}$)

### Substituting into dominant harmonic formula:

$$THD_{tot} = \frac{A_3^2 + A_5^2}{A_1^2}$$

$$THD_{tot} = \frac{(78.09553 \times 10^{-6})^2 + (13.63941 \times 10^{-6})^2}{(0.4982788)^2}$$

$$THD_{tot} = \frac{6.09891 \times 10^{-9} + 1.86036 \times 10^{-10}}{0.2482818}$$

$$THD_{tot} = \frac{6.28495 \times 10^{-9}}{0.2482818} = 2.53138 \times 10^{-8}$$

### Decibel Conversion:

$$THD\text{ (dB)} = 10 \log_{10}(2.53138 \times 10^{-8})$$

$$THD\text{ (dB)} = \mathbf{-75.99643\text{ dB}}$$

---

## 3. Performance Summary
- **Target Specification Limit**: Less than or equal to **$-55\text{ dB}$**.
- **Achieved Simulated Linearity**: **$-75.99643\text{ dB}$**.
- **Compliance Margin**: The design exceeds the target specification by **$20.996\text{ dB}$**, demonstrating outstanding dynamic linearity and high SFDR.
