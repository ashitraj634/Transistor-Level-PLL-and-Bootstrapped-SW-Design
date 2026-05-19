# Waveform Analysis & Simulation Outputs

This section analyzes the simulated time-domain waveforms of the bootstrapped switch obtained from transient analysis in Cadence Virtuoso:

## 1. Input and Output Transient Response
The transient simulation verifies correct sample-and-hold operation:
- **Tracking Mode ($CK = 1$)**: The output voltage ($V_{out}$) tracks the $1.0\text{ }V_{pp}$ sinusoidal input signal ($10\text{ MHz}$) centered at $0.9\text{ V}$ with negligible delay and attenuation.
- **Hold Mode ($CK = 0$)**: The output voltage ($V_{out}$) holds the sampled value on the load capacitor ($C_1$), appearing as a flat horizontal line until the next clock cycle.

## 2. Internal Charging Nodes ($V_A, V_P, V_Q$)
The waveforms of the internal nodes confirm correct charging and boosting behavior:
- **Node Q ($V_Q$)**: Clamped to ground during the hold phase. Tracks the input signal $V_{in}$ during the tracking phase.
- **Node P ($V_P$)**: Charged to $1.8\text{ V}$ ($V_{DD}$) during the hold phase. Boosted up to $V_{in} + V_{DD}$ (up to $2.7\text{ V} - 3.2\text{ V}$) during the tracking phase.
- **Node A ($V_A$, Gate of $M_1$)**: Follows the boosted voltage of Node P during the tracking phase, ensuring $V_{GS} \approx V_{DD}$ is maintained constantly.
