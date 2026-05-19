# Analog Building Blocks & Mixed-Signal IP Library

This directory houses a collection of transistor-level analog building blocks designed and characterized using **SCL 180 nm**, **UMC 180 nm**, and **GPDK 90 nm CMOS** technologies. These circuits serve as fundamental high-performance sub-systems for larger mixed-signal architectures, such as Analog-to-Digital Converters (ADCs) and Phase-Locked Loops (PLLs).

---

## Directory Navigation

* **[Amplifiers](Amplifiers/)**:
  * **[Common Source (Resistive Load)](Amplifiers/Common_Source/README.md)**: Standard driving stage with resistive load, designed for high-bandwidth application using gm/ID methodology.
  * **[Common Source (Active Load)](Amplifiers/CS_Active_Load/README.md)**: Active current-source loaded CS amplifier engineered for maximized voltage gain and output swing.
  * **[Cascode Amplifier](Amplifiers/Cascode/README.md)**: High-speed, high-gain cascode configuration optimized for minimized Miller effect and enhanced reverse isolation.
* **[Current Mirrors](Current_Mirrors/README.md)**: Simple and cascode current-steering mirrors characterized for high output resistance, headroom compliance, and channel length modulation suppression.
* **[Bootstrapped Sampling Switch](../Bootstrapped_Switch/README.md)**: High-linearity, low-distortion analog sampling gate engineered to suppress input-dependent on-resistance modulation.

---

## 1. Analog Library Performance Catalog

To establish robust circuit boundaries, all analog blocks are systematically characterized under nominal PVT conditions ($V_{DD} = 1.8\text{ V}$, $T = 27^\circ\text{C}$, standard $15\text{ fF}$ load):

### Dynamic Performance Specifications Matrix

| Analog Circuit block | Technology Node | Supply $V_{DD}$ | Open-Loop Gain ($A_v$) | Phase Margin ($PM$) | Gain-Bandwidth ($GBW$) | Power ($P_{diss}$) | Output Resistance ($R_{out}$) | Calibre/Assura DRC/LVS |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Common Source (Resistive)** | 180 nm CMOS | $1.8\text{ V}$ | $4.80\text{ V/V}$ ($13.62\text{ dB}$) | $82.4^\circ$ | $100\text{ MHz}$ | $180\ \mu\text{W}$ | $1.5\text{ k}\Omega$ | Passed (Clean) |
| **Common Source (Active)** | 180 nm CMOS | $1.8\text{ V}$ | $28.50\text{ V/V}$ ($29.09\text{ dB}$) | $68.5^\circ$ | $85\text{ MHz}$ | $240\ \mu\text{W}$ | $28.4\text{ k}\Omega$ | Passed (Clean) |
| **Cascode Amplifier** | 180 nm CMOS | $1.8\text{ V}$ | $124.20\text{ V/V}$ ($41.88\text{ dB}$) | $61.2^\circ$ | $200\text{ MHz}$ | $1.08\text{ mW}$ | $385.6\text{ k}\Omega$ | Passed (Clean) |
| **Simple Current Mirror** | 180 nm CMOS | $1.8\text{ V}$ | Mirror Error: $<0.82\%$ | - | - | $180\ \mu\text{W}$ | $18.5\text{ k}\Omega$ | Passed (Clean) |
| **Cascode Current Mirror** | 180 nm CMOS | $1.8\text{ V}$ | Mirror Error: $<0.11\%$ | - | - | $360\ \mu\text{W}$ | $2.42\text{ M}\Omega$ | Passed (Clean) |

---

## 2. Transistor Sizing & Design Parameters

Transistor geometries were calculated using the $g_m/I_D$ design methodology to establish optimum trade-offs between speed, power, and gain.

### Detailed Transistor Dimension Catalog

| Circuit Block | Device | Type | Width ($W$) | Length ($L$) | Multiplier ($m$) | Operating Region |
|:---|:---:|:---:|:---|:---|:---:|:---|
| **CS Amplifier (Resistive)** | $M_0$ | NMOS | $12.0\ \mu\text{m}$ | $0.18\ \mu\text{m}$ | 1 | Saturation (Strong Inversion) |
| **CS Amplifier (Active)** | $M_0$ (Driver) | NMOS | $15.0\ \mu\text{m}$ | $0.18\ \mu\text{m}$ | 1 | Saturation ($g_m/I_D \approx 12$) |
| | $M_1$ (Load) | PMOS | $30.0\ \mu\text{m}$ | $0.36\ \mu\text{m}$ | 1 | Saturation (High Output resistance) |
| **Cascode Amplifier** | $M_0$ (Input CS) | NMOS | $24.0\ \mu\text{m}$ | $0.18\ \mu\text{m}$ | 1 | Saturation (Minimized Miller effect) |
| | $M_1$ (Cascode CG)| NMOS | $24.0\ \mu\text{m}$ | $0.18\ \mu\text{m}$ | 1 | Saturation (High isolation) |
| | $M_2$ (PMOS Mirror)| PMOS | $48.0\ \mu\text{m}$ | $0.36\ \mu\text{m}$ | 1 | Saturation (Biasing current mirror) |
| **Simple Current Mirror** | $M_{ref}$ (Ref) | NMOS | $10.0\ \mu\text{m}$ | $0.36\ \mu\text{m}$ | 1 | Saturation (Biasing current reference) |
| | $M_{mirror}$ (Mir) | NMOS | $10.0\ \mu\text{m}$ | $0.36\ \mu\text{m}$ | 1 | Saturation (Matched Current output) |
| **Cascode Current Mirror** | $M_0, M_1$ (Bottom) | NMOS | $10.0\ \mu\text{m}$ | $0.36\ \mu\text{m}$ | 1 | Saturation (Biasing current reference) |
| | $M_2, M_3$ (Top Cas)| NMOS | $10.0\ \mu\text{m}$ | $0.36\ \mu\text{m}$ | 1 | Saturation (Shielding nodes) |

---

## 3. Mathematical Principles & Sizing Equations

### A. Common Source with Active PMOS Load
The active load CS amplifier replaces the passive drain resistor with a PMOS transistor operating as a constant current source. The small-signal open-loop voltage gain ($A_v$) is:

$$A_v = -g_{m1} (r_{o1} \parallel r_{o2})$$

Where:
- $g_{m1}$ is the transconductance of the NMOS driver.
- $r_{o1} = \frac{1}{\lambda_n I_D}$ and $r_{o2} = \frac{1}{\lambda_p I_D}$ represent the small-signal channel output resistances of NMOS and PMOS, respectively.
- Sizing PMOS with a larger length ($L_p = 0.36\ \mu\text{m}$) minimizes $\lambda_p$, boosting $r_{o2}$ and yielding a gain enhancement of over **$15.4\text{ dB}$** compared to resistive loading.

### B. High-Speed Cascode Amplifier
By stacking a Common-Gate (CG) stage above the Common-Source (CS) driver, the Miller multiplication of the input gate-drain capacitance ($C_{gd}$) is suppressed. The input stage sees a low input resistance:

$$R_{in,CG} \approx \frac{1}{g_{m2} + g_{mb2}}$$

This holds the drain node of the driver stable, boosting the high-frequency response and extending the Gain-Bandwidth Product to **$200\text{ MHz}$**. The overall cascode gain is:

$$A_v \approx -g_{m1} \left( [g_{m2} r_{o2} r_{o1}] \parallel [g_{m3} r_{o3} r_{o4}] \right)$$

This boosts the open-loop gain to **$41.88\text{ dB}$** ($124.2\text{ V/V}$).

### C. Current Mirror Output Impedance
- **Simple Current Mirror**: Output resistance is simple $R_{out} = r_{o} \approx 18.5\text{ k}\Omega$. Dynamic fluctuations in the drain voltage modulate the mirror current via channel length modulation.
- **Cascode Current Mirror**: Stacking the cascode device boosts the output resistance by the intrinsic gain of the cascode device:

$$R_{out,cascode} \approx g_{m2} r_{o2} r_{o1} \approx 2.42\text{ M}\Omega$$

This massive output resistance shields the mirror branches, holding the current mismatch error below **$0.11\%$** even when output voltages fluctuate up to the supply limit.

---

## Mixed-Signal Design Flow & Methodology

Every analog block inside this library was developed and sign-off verified using a rigorous industry-standard design flow in Cadence Virtuoso:

```
┌────────────────────────────────────────────────────────┐
│               1. Technology Characterization            │
│  Extract gm/ID, fT, lambda, and body-effect parameters │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                  2. Schematic Entry                    │
│    Sizing based on analytic specs & loop bandwidth     │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                3. Simulation & Validation              │
│       Spectre AC, DC, Transient & parametric sweeps    │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                  4. Physical Design                    │
│  Full-custom symmetric layout with guard ring isolation│
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│                5. Physical Verification                │
│    Assura / Calibre DRC & LVS checks                   │
└────────────────────────────────────────────────────────┘
```

---

## Verification & Quality Assurance
All structural blocks have successfully passed:
- **Design Rule Checking (DRC)**: Verified using both Cadence Assura and Mentor Graphics Calibre to ensure complete adherence to minimum layout spacing rules.
- **Layout Versus Schematic (LVS)**: Signed off via both Assura LVS and Calibre LVS tools, confirming 100% device and connectivity correspondence.
- **Parasitic RC Extraction (RCX/PEX)**: Extracted using Assura QRC and Calibre PEX to perform post-layout validation under real parasitics.
