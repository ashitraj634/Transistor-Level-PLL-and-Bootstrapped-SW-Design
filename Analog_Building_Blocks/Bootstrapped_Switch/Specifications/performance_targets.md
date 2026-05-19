# Performance Targets

The performance targets define the sign-off criteria for the bootstrapped switch design:

- **On-Resistance Variation ($\Delta R_{on}$)**: Less than or equal to **$\pm 5\%$** across the full input signal range ($0.4\text{ V} - 1.4\text{ V}$). This is critical to guarantee uniform settling behavior.
- **Total Harmonic Distortion (THD)**: Less than or equal to **$-55\text{ dB}$** at a 10 MHz input frequency, ensuring sufficient dynamic range for high-resolution ADC interfaces.
- **Clock Slew and Delay**: Under 50 ps transition times to avoid sampling clock jitter and minimize sampling aperture error.
- **Signal-Dependent Attenuation**: Minimized attenuation across the full frequency range to ensure that the tracking phase gain remains highly flat ($A_v \approx 1\text{ V/V}$).
