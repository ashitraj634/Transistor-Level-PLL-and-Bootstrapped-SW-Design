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

### Transition Frequency vs Gate Voltage (ft–VSG)

Shows frequency response variation.

![ft](plots/transfer/ft_vs_Vsg.png)

**Purpose**

- Determine high-frequency performance
- Study speed limitations

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

### Body Effect (ID vs VGS with Varying VSB)

Shows dependency of drain current on body bias.

![Body Effect](plots/output/Body_Effect.png)

**Purpose**

- Analyze threshold voltage shift
- Observe conduction dependency on source-body voltage

---

# gm/Id Design Analysis

---

### gm/Id vs VSG

![gmId Vsg](plots/gm_id/gm_Id_Vsg.png)

**Purpose**

- Analyze current efficiency

---

### Current Density vs gm/Id (ID/W vs gm/Id)

Shows variation of current density with efficiency.

![IdW vs gmId](plots/gm_id/IdW_vs_gmId.png)

**Purpose**

- Determine optimal transistor sizing
- Analyze strong inversion regions

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


# Tools Used

- Cadence Virtuoso
- Analog Design Environment (ADE)
- Device Simulation Setup
- Process Design Kit (PDK)

---