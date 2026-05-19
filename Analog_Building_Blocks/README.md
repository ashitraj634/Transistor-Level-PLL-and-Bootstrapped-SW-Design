# Analog Building Blocks & Mixed-Signal IP Library

This directory houses a collection of transistor-level analog building blocks designed and characterized using SCL 180 nm and GPDK 90 nm CMOS technologies. These circuits serve as fundamental high-performance sub-systems for larger mixed-signal architectures, such as Analog-to-Digital Converters (ADCs) and Phase-Locked Loops (PLLs).

---

## Directory Navigation

* **[Amplifiers](Amplifiers/)**:
  * **[Common Source (Resistive Load)](Amplifiers/Common_Source/README.md)**: Standard driving stage with resistive load, designed for high-bandwidth application using gm/ID methodology.
  * **[Common Source (Active Load)](Amplifiers/CS_Active_Load/README.md)**: Active current-source loaded CS amplifier engineered for maximized voltage gain and output swing.
  * **[Cascode Amplifier](Amplifiers/Cascode/README.md)**: High-speed, high-gain cascode configuration optimized for minimized Miller effect and enhanced reverse isolation.
* **[Current Mirrors](Current_Mirrors/README.md)**: Simple and cascode current-steering mirrors characterized for high output resistance, headroom compliance, and channel length modulation suppression.
* **[Bootstrapped Sampling Switch](Bootstrapped_Switch/README.md)**: High-linearity, low-distortion analog sampling gate engineered to suppress input-dependent on-resistance modulation.

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
│    Calibre DRC (design rules) & LVS (schematic match)  │
└────────────────────────────────────────────────────────┘
```

---

## 1. High-Gain & High-Speed Amplifiers
Optimized for mixed-signal front-ends, the amplifiers achieve excellent gain-bandwidth performance:
* **Common Source (Resistive)**: Delivers a voltage gain of $4.8\text{ V/V}$ with a $100\text{ MHz}$ Unity Gain Bandwidth (GBW) under a $5\text{ pF}$ load.
* **Common Source (Active Load)**: Sized to operate in the high-efficiency saturation region to achieve high intrinsic gain and large output voltage swings.
* **Cascode Configuration**: Increases output impedance by stacking transistors, providing massive reverse isolation and boosting voltage gain past $20\text{ dB}$ with a $200\text{ MHz}$ bandwidth.

---

## 2. Stable Current-Steering Mirrors
Accurate biasing is the foundation of robust analog design. The current mirror library includes:
* **Simple Current Mirror**: Characterized for current scaling ratio match and headroom tracking.
* **Cascode Current Mirror**: Employs cascode transistor stacking to boost output resistance to the mega-ohm range, mitigating channel-length modulation ($\lambda$) and ensuring highly stable bias currents ($100\ \mu\text{A} - 500\ \mu\text{A}$) despite fluctuating output node voltages.

---

## 3. High-Linearity Bootstrapped Analog Switch
Traditional MOS switches suffer from input-dependent on-resistance ($R_{on}$) variations, causing harmonic distortion in high-precision ADCs.
* **Design Approach**: Implements an active bootstrapping network that dynamically clamps the Gate-Source voltage ($V_{gs}$) of the sampling transistor to $V_{DD}$ during the ON phase.
* **Performance Metric**: Achieves a highly stable $R_{on}$ variation of just **$\pm 3.43\%$** across a $1\text{ }V_{pp}$ input signal swing at $10\text{ MHz}$, eliminating signal-dependent harmonic distortion.

---

## Verification & Quality Assurance
All structural blocks have successfully passed:
- **Calibre Design Rule Checking (DRC)** for clean manufacturing tolerances.
- **Layout Versus Schematic (LVS)** matching to guarantee physical netlist correspondence.
- **Spectre Post-Layout RC Extraction (RCX)** to account for interconnect parasitics and verify performance margin compliance.
