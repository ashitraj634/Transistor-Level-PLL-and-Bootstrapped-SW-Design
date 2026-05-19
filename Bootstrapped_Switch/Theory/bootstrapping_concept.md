# Bootstrapping Concept

To eliminate the signal-dependence of the switch on-resistance, the gate-to-source overdrive voltage ($V_{GS} - V_{TH}$) must be kept constant regardless of the input signal level. The bootstrapping technique accomplishes this by implementing a dynamic gate drive circuit:

## Floating Battery Analogy
The core design concept relies on using a capacitor ($C_b$) as a floating DC voltage source (or battery):
1. **Charging Phase**: During the non-tracking phase, the capacitor is charged to the supply voltage ($V_{DD}$).
2. **Bootstrapping Phase**: During the tracking phase, the charging paths are disconnected, and the capacitor is connected directly between the gate and source terminals of the main switch ($M_1$).

## Overdrive Stabilization
By connecting the pre-charged capacitor $C_b$ between the gate ($V_G$) and source ($V_S = V_{in}$) of the main NMOS transistor:
- The gate voltage is boosted above the power rail:
  $$V_G(t) = V_{in}(t) + V_{DD}$$
- The resulting gate-to-source voltage is fixed:
  $$V_{GS} = V_G - V_{in} = (V_{in} + V_{DD}) - V_{in} = V_{DD}$$

Since $V_{GS} \approx V_{DD}$ is held constant, the switch on-resistance remains virtually flat across the entire input range, ensuring highly linear sampling.
