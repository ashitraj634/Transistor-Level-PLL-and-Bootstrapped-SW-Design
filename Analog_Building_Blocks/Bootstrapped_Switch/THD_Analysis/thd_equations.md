# THD Calculation Equations

This document details the mathematical framework for computing the Total Harmonic Distortion (THD) of the sampled output signal:

## 1. Definition of THD
Total Harmonic Distortion (THD) measures the ratio of the power contained in the higher-order harmonics to the power of the fundamental frequency component:

$$THD_{tot} = \frac{A_2^2 + A_3^2 + A_4^2 + A_5^2 + \dots}{A_1^2}$$

In a fully differential layout or symmetric design, even-order harmonics (e.g. $A_2, A_4$) are mostly cancelled or negligible. Therefore, the third ($A_3$) and fifth ($A_5$) harmonics dominate the distortion profile:

$$THD_{tot} \approx \frac{A_3^2 + A_5^2}{A_1^2}$$

## 2. Decibel Conversion
To convert the distortion ratio into decibels (dB) for standard reporting:

$$THD\text{ (dB)} = 10 \log_{10}(THD_{tot})$$
