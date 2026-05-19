# THD Calculation & Results

This document presents the detailed mathematical evaluation of the Total Harmonic Distortion (THD) using the extracted spectral measurements:

## Mathematical Substitution

Using the dominant harmonic formulation:

$$THD_{tot} = \frac{A_3^2 + A_5^2}{A_1^2}$$

$$THD_{tot} = \frac{(78.09553 \times 10^{-6})^2 + (13.63941 \times 10^{-6})^2}{(0.4982788)^2}$$

$$THD_{tot} = \frac{6.09891 \times 10^{-9} + 1.86036 \times 10^{-10}}{0.2482818}$$

$$THD_{tot} = \frac{6.28495 \times 10^{-9}}{0.2482818} = 2.53138 \times 10^{-8}$$

## Decibel Conversion

$$THD\text{ (dB)} = 10 \log_{10}(2.53138 \times 10^{-8})$$

$$THD\text{ (dB)} = -75.99643\text{ dB}$$

## Performance Conclusion
- **Required Specification**: Less than or equal to $-55\text{ dB}$.
- **Achieved Performance**: **$-75.99643\text{ dB}$**.
- **Margin**: The design exceeds the target specification by **$20.996\text{ dB}$**, demonstrating outstanding dynamic range and linearity.
