# PMOS Device Characterization

## Overview

This section presents transistor-level characterization of a PMOS device for analog and mixed-signal circuit design applications. The objective is to study PMOS behavior under different biasing conditions and extract parameters used for transistor sizing and gm/Id design methodologies.

The characterization includes:

- Transfer characteristics
- Output characteristics
- Threshold voltage extraction
- Transconductance analysis
- gm/Id methodology
- Gate capacitance behavior
- Transition frequency analysis
- Saturation characteristics
- Channel length modulation
- Body effect analysis

---

## Device Schematic

The following schematic was used for PMOS characterization.

![PMOS Schematic](schematics/Schematic.png)

---

# Transfer Characteristics

Transfer characteristics show how drain current and small-signal parameters vary with gate-source voltage.

---

### Drain Current vs Gate Voltage (ID–VSG)

Shows variation of drain current with gate voltage.

![Id vs Vsg](plots/transfer/Id_Vsg.png)

**Purpose**

- Observe PMOS turn-on behavior
- Determine weak and strong inversion regions
- Analyze current variation

---

### Transconductance vs Gate Voltage (gm–VSG)

Shows sensitivity of drain current with respect to gate voltage.

![gm vs Vsg](plots/transfer/gm_Vsg.png)

**Purpose**

- Analyze gain capability
- Determine optimum operating region

---

### Threshold Voltage Extraction

Shows extracted threshold voltage characteristics.

![Vth](plots/transfer/Vth_Vsg.png)

**Purpose**

- Determine PMOS turn-on voltage
- Verify device characteristics

---

### Transition Frequency vs Gate Voltage (ft–VSG)

Shows frequency response variation.

![ft](plots/transfer/ft_vs_Vsg.png)

**Purpose**

- Determine high-frequency performance
- Study speed limitations

---

### Gate Voltage vs gm/Id

Shows relationship between gate voltage and gm/Id.

![Vsg gmId](plots/transfer/Vsg_gm_Id.png)

**Purpose**

- Support transistor sizing
- Determine operating efficiency

---

# Output Characteristics

Output characteristics describe current variation with drain-source voltage.

---

### Drain Current vs Drain Voltage (ID–VSD)

![Id vs Vsd](plots/output/Id_Vsd.png)

**Purpose**

- Identify operating regions
- Observe saturation characteristics

---

### Drain Current vs Gate Voltage for Multiple VSD

![Multiple Vsd](plots/output/Id_Vsg_multiple_Vsd.png)

**Purpose**

- Study bias dependence
- Observe short-channel behavior

---

### Saturation Voltage vs Gate Voltage

![Vdsat](plots/output/Vdsat_Vsg.png)

**Purpose**

- Determine saturation conditions

---

# gm/Id Design Analysis

---

### gm/Id vs VSG

![gmId Vsg](plots/gm_id/gm_Id_Vsg.png)

**Purpose**

- Analyze current efficiency

---

### gm/Id vs VSD

![gmId Vsd](plots/gm_id/gm_Id_Vsd.png)

**Purpose**

- Study bias sensitivity

---

### Gate Capacitance vs Gate Voltage

![Cgs](plots/gm_id/Cgs_Vsg.png)

**Purpose**

- Analyze dynamic performance

---

### Transition Frequency vs gm/Id

![ft gmId](plots/gm_id/ft_vs_gmId.png)

**Purpose**

- Study speed-efficiency tradeoffs

---

# Key Observations

- PMOS characteristics are complementary to NMOS behavior
- Device operation observed in linear and saturation regions
- gm/Id methodology used for transistor sizing
- Frequency and capacitance effects analyzed
- Device characteristics useful for analog and mixed-signal design

---

# Future Work

- Parameter extraction
- PMOS vs NMOS comparison
- Transistor sizing analysis
- PLL circuit integration
- Bootstrapped switch implementation

---

# Tools Used

- Cadence Virtuoso
- Analog Design Environment (ADE)
- Device Simulation Setup
- Process Design Kit (PDK)

---