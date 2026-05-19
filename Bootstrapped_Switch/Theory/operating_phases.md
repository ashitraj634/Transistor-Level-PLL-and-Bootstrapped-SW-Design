# Operating Phases

The operation of the bootstrapped switch is divided into two distinct, non-overlapping phases controlled by the clock signal ($CK$):

## 1. Hold Phase ($CK = 0$, $CK\_bar = 1$)
During the hold phase, the main sampling switch is turned off, and the bootstrap capacitor is charged to the supply voltage:
- **Switch Isolation**: The gate of the main switch ($M_1$) is pulled to ground through transistor $M_6$. The gate-to-source voltage is:
  $$V_{GS} \approx 0\text{ V}$$
  This isolates the input signal ($V_{in}$) from the load capacitor ($C_1$).
- **Capacitor Pre-charging**: The bottom terminal of $C_b$ (node Q) is tied to ground via transistor $M_4$. The top terminal of $C_b$ (node P) is connected to $V_{DD}$ via transistor $M_5$. As a result, the capacitor is charged to:
  $$V_{Cb} = V_P - V_Q \approx V_{DD}$$
  This pre-charges the "floating battery" for the next phase.

## 2. Sampling/Tracking Phase ($CK = 1$, $CK\_bar = 0$)
During the tracking phase, the pre-charged capacitor is reconfigured to boost the gate of the main switch:
- **Switch Activation**: Transistors $M_4$ and $M_5$ are turned off to isolate $C_b$ from $V_{DD}$ and ground.
- **Dynamic Reconfiguration**: Transistor $M_2$ turns on, connecting the bottom terminal of $C_b$ (node Q) directly to the input signal $V_{in}$. Simultaneously, transistor $M_3$ turns on, connecting the top terminal of $C_b$ (node P) to the gate of $M_1$ (node A).
- **Gate Voltage Boosting**: Because the voltage across $C_b$ is fixed at $V_{DD}$, referencing the bottom terminal to $V_{in}$ shifts the gate voltage upwards:
  $$V_G(t) = V_{in}(t) + V_{DD}$$
- **Constant Overdrive**: The Gate-Source voltage is stabilized:
  $$V_{GS} = V_G(t) - V_{in}(t) = V_{DD}$$
  This constant gate drive maintains a highly uniform on-resistance.
