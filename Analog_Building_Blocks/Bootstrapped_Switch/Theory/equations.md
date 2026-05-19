# Governing Mathematical Equations

This document summarizes the core equations dictating the operation, sizing, and performance limits of the bootstrapped switch:

## 1. On-Resistance ($R_{on}$) in Triode Region
The resistance of the main sampling switch ($M_1$) during the tracking phase is defined by:

$$R_{on} = \frac{1}{\mu_n C_{ox} \left(\frac{W}{L}\right)_1 (V_{GS} - V_{TH})}$$

In the bootstrapped configuration, $V_{GS} \approx V_{DD}$, so:

$$R_{on} \approx \frac{1}{\mu_n C_{ox} \left(\frac{W}{L}\right)_1 (V_{DD} - V_{TH})}$$

## 2. Gate Voltage Boosting
The boosted gate voltage ($V_G$) at node A during the tracking phase is defined by:

$$V_G(t) = V_{in}(t) + V_{DD}$$

This forces the maximum gate voltage at the peak of the input signal to exceed the supply rail:

$$V_{G,max} = V_{in,max} + V_{DD} = 1.4\text{ V} + 1.8\text{ V} = 3.2\text{ V}$$

## 3. On-Resistance Variation Ratio
The percentage variation of the on-resistance is calculated as:

$$R_{avg} = \frac{R_{on,max} + R_{on,min}}{2}$$

$$\% \text{ Variation} = \left(\frac{R_{on,max} - R_{on,min}}{R_{avg}}\right) \times 100\%$$

For a symmetrical bounds presentation, this is expressed as:

$$\text{Resistance Variation} = \pm \left(\frac{\% \text{ Variation}}{2}\right)$$

## 4. Total Harmonic Distortion (THD)
The harmonic distortion of the sampled sinusoid is calculated from the fundamental ($A_1$) and harmonic spectral components ($A_3, A_5$):

$$THD_{tot} = \frac{\sum_{i > 1} A_i^2}{A_1^2} \approx \frac{A_3^2 + A_5^2}{A_1^2}$$

$$THD\text{ (dB)} = 10 \log_{10}(THD_{tot})$$
