# Custom CMOS Standard Cell Library

This directory contains the physical design, characterization, and verification of a custom-designed CMOS Standard Cell Library implemented in SCL 180 nm CMOS technology. These digital standard cells serve as the fundamental high-speed building blocks for the digital blocks of the Phase-Locked Loop (PLL), specifically the Phase Frequency Detector (PFD) and the Divide-by-128 feedback frequency counter.

---

## Directory Navigation

* **[Inverter (INV)](Inverter/README.md)**: Full-custom CMOS inverter design, DC transfer characteristics (VTC), transient propagation delay analysis, layouts, RC parasitic extraction (RCX), and Calibre DRC/LVS physical verification checks.
* **Logic Gates & Storage Elements**:
  * **[NAND2](NAND2/README.md)**: Two-input custom NAND logic cell schematic and transistor aspect ratio matching.
  * **[NAND3](NAND3/README.md)**: Three-input CMOS NAND logic cell sizing and leakage power minimization.
  * **[D-Flip-Flop (DFF)](D_Flip_Flop/README.md)**: High-speed edge-triggered storage element utilized for toggle division in the Divide-by-128 counter.

---

## Design Flow & cell Layout Methodology

Digital standard cells are designed to fit together seamlessly in a row-based placement grid:

1. **Height Sizing**: All cells share a uniform height constraint with aligned VDD and VSS power rails to support automatic routing and abutment.
2. **Symmetrical Sizing**: Transistor widths ($W_p$ and $W_n$) are balanced using transconductance modeling to establish equal rise and fall transition delays and high noise margins.
3. **Guard Rings**: Integrated substrate and well taps prevent latch-up and shield the sensitive digital gates from surrounding analog noise.
4. **Sign-off Physical Verification**: Symmetrical layouts are verified using Calibre Design Rule Checking (DRC) and Layout Versus Schematic (LVS) comparison to ensure absolute silicon manufacturing readiness.

---

## 1. High-Performance CMOS Inverter Cell
The standard cell characterization details the switching boundaries of the inverter:
* **DC Voltage Transfer Characteristics (VTC)**: Characterized to determine the switching threshold ($V_{sp} \approx 0.9\text{ V}$) for maximum symmetric noise margins.
* **Parasitic Degradation**: Standard cell transient sweeps compare pre-layout schematic responses against post-layout RC-extracted simulations. Physical interconnect resistance and parasitic capacitances result in a **15.67% propagation delay increase** (slowing from $33.67\text{ ps}$ pre-layout to $38.94\text{ ps}$ post-layout).

---

## 2. NAND Logic Gates
Multi-input logic gates are characterized for dynamic switching limits:
* **NAND2 & NAND3**: Designed using stacked NMOS structures and parallel PMOS pull-up networks. Transistor widths are scaled appropriately ($2\times$ and $3\times$) to compensate for the stacked channel resistances and maintain symmetric rising/falling slew rates.

---

## 3. High-Speed D-Flip-Flop (DFF)
Edge-triggered storage elements form the backbone of the frequency counter:
* **Topology**: Engineered using transmission-gate logic to achieve low propagation delay, high clock-to-Q switching speeds, and robust timing hold margins.
* **PLL Feedback Application**: Serves as the fundamental dividing block inside the Divide-by-128 feedback network, operating stably at multi-GHz clock rates.
