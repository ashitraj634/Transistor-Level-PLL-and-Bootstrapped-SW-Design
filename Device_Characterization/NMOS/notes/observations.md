# NMOS Device Characterization – Observations

## Experiment Objective

Characterize an NMOS transistor and analyze important device parameters through simulation and extracted measurements.

Parameters analyzed:

- ID vs VGS
- ID vs VDS
- gm vs VGS
- gm/ID vs VGS
- Vth vs VGS
- VDSAT vs VGS
- ID/W vs gm/ID
- ft vs gm/ID
- VGS vs gm/ID
- ft vs VGS
- Cgs vs VGS
- Channel Length Modulation
- Body Effect

---

# Transfer Characteristics Analysis

## 1. ID vs VGS

### Observation

- Drain current remains very small below threshold voltage.
- Current begins increasing rapidly after the threshold region.
- Device transitions from weak inversion to strong inversion.

### Inference

- Below threshold, the transistor remains OFF.
- Above threshold voltage, channel formation occurs and current increases significantly.

---

## 2. gm vs VGS

### Observation

- Transconductance increases as VGS increases.
- Higher gate voltages improve current sensitivity.

### Inference

- Larger gm improves gain capability.
- Bias selection strongly affects analog performance.

---

## 3. gm/ID vs VGS

### Observation

- gm/ID ratio decreases with increasing gate voltage.

### Inference

- Weak inversion:
  - High current efficiency
  - Lower speed

- Strong inversion:
  - Higher speed
  - Lower efficiency

---

## 4. Vth vs VGS

### Observation

- Threshold voltage extraction shows the transition region where conduction starts.

### Inference

- Threshold voltage determines transistor turn-on characteristics.

---

## 5. Cgs vs VGS

### Observation

- Gate capacitance increases with increasing gate voltage.

### Inference

- Larger capacitance impacts switching speed and dynamic power consumption.

---

# Output Characteristics Analysis

## 6. ID vs VDS

### Observation

Two operating regions are visible:

### Linear Region

- Current increases approximately linearly with VDS.

### Saturation Region

- Current becomes relatively constant.

### Inference

- Device behaves as expected according to MOSFET theory.
- Saturation region shows slight slope because of channel length modulation.

---

## 7. VDSAT vs VGS

### Observation

- Saturation voltage increases with gate voltage.

### Inference

- Larger gate overdrive requires larger drain voltage to maintain saturation.

---

# gm/ID Design Methodology Analysis

## 8. ID/W vs gm/ID

### Observation

- Current density increases as gm/ID decreases.

### Inference

- Strong inversion operation produces higher current density.

---

## 9. ft vs gm/ID

### Observation

- Transition frequency decreases as gm/ID increases.

### Inference

- Tradeoff exists between speed and power efficiency.

---

## 10. VGS vs gm/ID

### Observation

- Gate voltage increases as gm/ID decreases.

### Inference

- Higher gate bias moves operation toward strong inversion.

---

## 11. ft vs VGS

### Observation

- Transition frequency increases with gate voltage.

### Inference

- High-speed operation becomes achievable at larger bias currents.

---

# Channel Length Modulation

## Calculated Value

λ = 0.189

### Observation

- Drain current in saturation shows a small positive slope instead of remaining perfectly constant.

### Inference

- Effective channel length decreases with increasing VDS.
- Output resistance becomes finite.

Relationship:

$$
I_D = I_{D(sat)}(1+\lambda V_{DS})
$$

where:

- λ = Channel length modulation coefficient

Calculated:

$$
\lambda = 0.189
$$

---

# Body Effect Analysis

Body effect was studied at:

VDS = 1.4 V

## Observed Data

| VSB (V) | ID (µA) |
|----------|----------|
| 0.1 | 312.854 |
| 0.2 | 251.645 |
| 0.3 | 193.216 |
| 0.4 | 138.366 |
| 0.5 | 88.665 |

---

### Observation

- Drain current decreases as VSB increases.

### Inference

As source-to-body voltage increases:

- Threshold voltage increases
- Channel formation becomes harder
- Drain current reduces

Threshold voltage equation:

$$
V_T = V_{T0}+\gamma[(\sqrt{2\phi+V_{SB}})-(\sqrt{2\phi})]
$$

Drain current equation:

$$
I_D=\frac{1}{2}\mu_nC_{ox}\frac{W}{L}(V_{GS}-V_T)^2
$$

Since:

- VSB ↑
- VT ↑

Therefore:

- ID ↓

---

# Overall Conclusion

The NMOS device exhibits expected MOSFET behavior in both transfer and output characteristics.

Key findings:

✓ Weak and strong inversion regions identified

✓ gm/ID methodology analyzed

✓ Channel length modulation coefficient extracted

✓ Body effect successfully studied

✓ Frequency response and capacitance effects observed

These results are useful for:

- Analog transistor sizing
- gm/ID based design
- Transistor-level PLL implementation
- Bootstrapped switch design
- Device optimization studies
