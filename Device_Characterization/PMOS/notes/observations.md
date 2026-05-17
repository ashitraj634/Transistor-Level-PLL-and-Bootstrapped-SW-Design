# PMOS Device Characterization – Observations

## Experiment Objective

Characterize a PMOS transistor and analyze important device parameters through simulation and extracted measurements.

Parameters analyzed:

- ID vs VGS
- ID vs VDS
- ID vs VDS with different VGS
- gm/ID vs VGS
- ID/W vs gm/ID
- ft vs VGS
- ft vs gm/ID
- ID vs VGS with varying VSB
- Channel Length Modulation
- Body Effect

---

# Transfer Characteristics Analysis

## 1. ID vs VGS

### Observation

- Drain current remains small before threshold voltage magnitude is reached.
- Current magnitude increases rapidly after threshold.
- PMOS moves from weak inversion to strong inversion operation.

### Inference

- Channel formation occurs once the gate voltage exceeds threshold requirements.
- Drain current magnitude increases due to increased hole concentration.

---

## 2. gm/ID vs VGS

### Observation

- gm/ID decreases with increasing gate voltage magnitude.

### Inference

Weak inversion region:

- Higher current efficiency
- Lower speed

Strong inversion region:

- Higher speed
- Lower efficiency

---

## 3. ID/W vs gm/ID

### Observation

- Current density increases as gm/ID decreases.

### Inference

- Larger current density corresponds to strong inversion operation.

---

# Output Characteristics Analysis

## 4. ID vs VDS

### Observation

Two operating regions were observed:

### Linear Region

- Drain current increases approximately linearly with VDS.

### Saturation Region

- Current approaches saturation and becomes relatively constant.

### Inference

- PMOS behaves according to expected MOSFET theory.
- Saturation region exhibits slight variation due to channel length modulation.

---

## 5. ID vs VDS for Different VGS

### Observation

- Increasing gate voltage magnitude increases current magnitude.
- Multiple curves show increased conduction with larger gate bias.

### Inference

- Larger gate overdrive increases channel charge density.

---

# Frequency Response Analysis

## 6. ft vs VGS

### Observation

- Transition frequency increases with increasing gate voltage magnitude.

### Inference

- Higher operating speed becomes achievable at larger bias currents.

---

## 7. ft vs gm/ID

### Observation

- Transition frequency decreases with increasing gm/ID.

### Inference

- Tradeoff exists between current efficiency and speed.

---

# Body Effect Analysis

## ID vs VGS with Varying VSB

### Observation

Drain current varies as body bias changes.

As source-body voltage changes:

- Threshold voltage magnitude changes
- Current magnitude decreases

### Inference

Body effect occurs because:

$$
V_{SB}>0
$$

Threshold voltage relationship:

$$
V_T=V_{T0}+\gamma[(\sqrt{2\phi+V_{SB}})-(\sqrt{2\phi})]
$$

Drain current relationship:

$$
I_D=
\frac{1}{2}
\mu_p C_{ox}
\frac{W}{L}
(V_{SG}-V_T)^2
$$

As:

- VSB increases
- VT increases

Therefore:

- ID decreases

---

# Channel Length Modulation

## Given Values

VDS₁ = -1.8 V

IDS₁ = -254.744 µA

VDS₂ = -2.0 V

IDS₂ = -250.36 µA

Using:

$$
\frac{I_{DS1}}{I_{DS2}}
=
\frac{1-\lambda V_{DS1}}
{1-\lambda V_{DS2}}
$$

Calculated:

$$
\lambda=0.153
$$

### Observation

- Saturation current shows a slight variation with increasing drain voltage.

### Inference

- Effective channel length decreases with increasing drain voltage magnitude.
- Output resistance becomes finite.

---

# Overall Experimental Inference

The PMOS device characteristics were successfully obtained and analyzed.

Observed characteristics:

✓ Drain current variation with gate voltage

✓ Linear and saturation operating regions

✓ Body effect dependency

✓ Channel length modulation effects

✓ Frequency response behavior

✓ gm/ID design methodology trends

---

# Applications

Results obtained from PMOS characterization can be used for:

- Analog transistor sizing
- Current mirror design
- CMOS logic implementation
- Differential amplifier design
- Transistor-level PLL implementation
- Bootstrapped switch design

---
