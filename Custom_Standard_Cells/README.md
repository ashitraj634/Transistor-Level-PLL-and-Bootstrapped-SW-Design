# Custom CMOS Standard Cell Library

This directory contains the physical design, characterization, and verification of a custom-designed CMOS Standard Cell Library implemented in **SCL 180 nm CMOS technology** in Cadence Virtuoso. These digital standard cells serve as the fundamental high-speed building blocks for the digital blocks of the Phase-Locked Loop (PLL), specifically the Phase Frequency Detector (PFD) and the Divide-by-128 feedback frequency counter.

---

## Directory Navigation

* **[Inverter (INV)](Inverter/README.md)**: Full-custom CMOS inverter design, DC transfer characteristics (VTC), transient propagation delay analysis, layouts, RC parasitic extraction (RCX), and Calibre/Assura DRC/LVS physical verification checks.
* **Logic Gates & Storage Elements**:
  * **[NAND2](NAND2/README.md)**: Two-input custom NAND logic cell schematic and transistor aspect ratio matching.
  * **[NAND3](NAND3/README.md)**: Three-input CMOS NAND logic cell sizing and leakage power minimization.
  * **[D-Flip-Flop (DFF)](D_Flip_Flop/README.md)**: High-speed edge-triggered storage element utilized for toggle division in the Divide-by-128 counter.

---

## 1. Standard Cell Performance Catalogue

To construct a robust digital boundaries grid for the Phase-Locked Loop blocks, each cell underwent extensive pre-layout and post-layout characterization under standard loads ($C_L = 15\text{ fF}$, $V_{DD} = 1.8\text{ V}$, $T = 27^\circ\text{C}$):

### Comparative Standard Cell Specs Matrix

| Standard Cell | Function | PMOS Sizing ($W_p/L_p$) | NMOS Sizing ($W_n/L_n$) | Switching Threshold ($V_{sp}$) | Pre-Layout Delay ($t_{pd1}$) | Post-Layout Delay ($t_{pd2}$) | Parasitic Delay Penalty (%) | Dynamic Power | Calibre/Assura DRC/LVS |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Inverter (INV)** | Logical NOT | $1.20\ \mu\text{m} / 0.18\ \mu\text{m}$ | $0.60\ \mu\text{m} / 0.18\ \mu\text{m}$ | $0.90\text{ V}$ | $33.67\text{ ps}$ | $38.95\text{ ps}$ | **$15.67\%$** | $32.4\ \mu\text{W}$ | Passed (Clean) |
| **NAND2 Gate** | 2-Input NAND | $0.42\ \mu\text{m} / 0.18\ \mu\text{m}$ | $0.42\ \mu\text{m} / 0.18\ \mu\text{m}$ | $0.85\text{ V}$ | $42.50\text{ ps}$ | $49.80\text{ ps}$ | **$17.18\%$** | $48.6\ \mu\text{W}$ | Passed (Clean) |
| **NAND3 Gate** | 3-Input NAND | $0.42\ \mu\text{m} / 0.18\ \mu\text{m}$ | $1.26\ \mu\text{m} / 0.18\ \mu\text{m}$ | $0.82\text{ V}$ | $58.20\text{ ps}$ | $69.40\text{ ps}$ | **$19.24\%$** | $62.8\ \mu\text{W}$ | Passed (Clean) |
| **D-Flip-Flop (DFF)**| Master-Slave Storage | Hierarchical Transmission Gate | Hierarchical Transmission Gate | - | $120.00\text{ ps}$ ($t_{C2Q}$) | $138.00\text{ ps}$ ($t_{C2Q}$) | **$15.00\%$** | $145.2\ \mu\text{W}$ | Passed (Clean) |

---

## 2. Standard Cell Layout Grid & Physical Sizing Rules

Full-custom physical layout of standard cells follows strict geometry-matching design rules to enable seamless multi-cell row integration:

1. **Standard Cell Row Height (Grid Abutment)**: All cell boundaries are locked to a standardized vertical height of **$8.0\ \mu\text{m}$**. The power ($V_{DD}$) and ground ($V_{SS}$) rails are placed symmetrically at the cell boundaries using high-thickness Metal-1 lines, allowing cells to share power paths directly upon horizontal placement (abutment).
2. **Symmetrical Rise and Fall Delay Sizing**:
   - For the Inverter, holes in silicon have about half the mobility ($\mu_h \approx 0.5 \mu_e$) of electrons. PMOS is sized twice as wide as NMOS ($W_p / W_n = 2.0$) to guarantee symmetrical rising ($t_{PLH}$) and falling ($t_{PHL}$) switching delays.
   - For multi-input NAND gates, series NMOS transistors stack up to increase channel resistance. For NAND2, NMOS widths are scaled up to compensate for the stack ($W_n = 0.42\ \mu\text{m}$). For NAND3, the NMOS width is scaled to three times the minimum ($W_n = 1.26\ \mu\text{m}$) to compensate for the three-transistor stacking resistance.
3. **Substrate Tap & Well Tap Placement**: Integrated guard rings and well taps are distributed adjacent to boundary edges to lower well-to-substrate resistance, preventing catastrophic CMOS latch-up and shielding sensitive digital logic nodes from high-frequency analog substrate noise coupling.

---

## 3. Cell Functional Logic & Timing Overview

### A. High-Speed Master-Slave D-Flip-Flop (DFF)
Used in the Divide-by-128 feedback ripple counter. The latching master-slave transmission gates eliminate timing setup/hold glitches, ensuring reliable multi-GHz toggle frequency operation:
- **Setup Time ($t_{setup}$)**: **$85.0\text{ ps}$** (Minimum stable input window before active clock edge).
- **Hold Time ($t_{hold}$)**: **$45.0\text{ ps}$** (Minimum stable input window after active clock edge).
- **Clock-to-Q delay ($t_{C2Q}$)**: Pre-layout propagation delay is $120\text{ ps}$, which increases to $138\text{ ps}$ post-layout due to physical metal line parasitics (a parasitic delay penalty of **$15.00\%$**).

### B. High-Speed PFD Reset Control (`NAND3`)
The Phase Frequency Detector (PFD) utilizes a custom-designed three-input NAND gate (`NAND3`) in its asynchronous DFF reset feedback loop. Sizing is optimized to balance switching thresholds ($V_{sp} \approx 0.82\text{ V}$) and supply leakage power:
- **Delay Budget**: The post-layout propagation delay ($69.40\text{ ps}$) introduces a controlled delay to avoid dead-zones, matching the active turn-on times of the charge pump switches.

---

## Standard Cell CAD Design Flow & Methodology

Digital standard cells are designed to fit together seamlessly in a row-based placement grid:

```
┌────────────────────────────────────────────────────────┐
│               1. Transistor-Level Sizing               │
│  Symmetrical Wp/Wn ratios for matched delay properties │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│               2. DC & AC Dynamic Analysis              │
│       VTC switching threshold & pre-layout timing      │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│               3. Full-Custom Grid Layout               │
│ Standardized height, Power rail routing, Well/Sub taps │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│         4. Assura & Calibre DRC & LVS Sign-Off         │
│  Design rule compliance & matching schematic netlists  │
└───────────────────────────┬────────────────────────────┘
                            ▼
┌────────────────────────────────────────────────────────┐
│           5. Parasitic RC Extraction (PEX)             │
│    Post-layout simulations to extract delay penalty    │
└────────────────────────────────────────────────────────┘
```
