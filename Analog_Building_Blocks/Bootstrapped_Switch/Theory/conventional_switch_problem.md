# Conventional Switch Limitation

## The Signal Dependence of On-Resistance
For a simple NMOS transistor operating as an analog switch in the linear (triode) region, the channel current is dictated by the drain-to-source voltage and the overdrive voltage. The on-resistance ($R_{on}$) is given by:

$$R_{on} = \frac{1}{\mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{TH})}$$

In a conventional switch driven by a constant clock voltage ($V_{CLK} = V_{DD}$):
- The gate terminal is clamped to $V_{DD}$ during tracking.
- The source terminal is connected to the time-varying input voltage ($V_{in}(t)$).
- Thus, the gate-to-source voltage is highly signal-dependent:
  $$V_{GS}(t) = V_{DD} - V_{in}(t)$$

Substituting this into the resistance equation yields:

$$R_{on}(t) = \frac{1}{\mu_n C_{ox} \frac{W}{L} (V_{DD} - V_{in}(t) - V_{TH})}$$

## Performance Consequences
As the input voltage ($V_{in}$) increases, the overdrive voltage ($V_{GS} - V_{TH}$) decreases, leading to a significant increase in $R_{on}$. This non-linear resistance modulation has several adverse effects:

1. **Signal-Dependent Bandwidth Attenuation**: The low-pass cut-off frequency of the sampling network ($f_c = \frac{1}{2\pi R_{on} C_L}$) shifts dynamically with the input voltage, creating a non-linear transfer function.
2. **Harmonic Distortion**: The variation in $R_{on}$ introduces input-dependent phase lag and amplitude attenuation, generating strong odd-order harmonics (especially the 3rd and 5th harmonics) in the sampled output.
3. **Reduced Resolution**: For high-speed, high-resolution converters (e.g., >= 10-bit ADCs), this distortion limits the Spurious-Free Dynamic Range (SFDR) and Signal-to-Noise-and-Distortion Ratio (SNDR).
