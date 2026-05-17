# NMOS Device Characterization

## Overview

NMOS device characterization was performed in Cadence Virtuoso to extract transistor-level parameters for analog design and gm/Id methodology.

## Design Environment

| Parameter | Value |
|------------|--------|
| Tool | Cadence Virtuoso |
| Libraries | UMC18 / ts018_scl_prim / gpdk090 |
| Analysis | DC Analysis |

---

## Extracted Parameters

- ID vs VGS
- ID vs VGS for multiple VDS
- ID vs VDS
- gm vs VGS
- gm/ID vs VGS
- Vth vs VGS
- VDSAT vs VGS
- ID/W vs gm/ID
- ft vs gm/ID
- ft vs VGS
- Cgs vs VGS
- Body effect

---

## Channel Length Modulation

λ = 0.189

---

## Results

### ID vs VGS

![ID-VGS](Id_Vgs.png)

### ID vs VDS

![ID-VDS](Id_Vds.png)

### gm vs VGS

![gm](gm_Vgs.png)

### gm/ID vs VGS

![gmID](gm_Id_Vgs.png)

### Cgs vs VGS

![Cgs](Cgs_Vgs.png)

### Vth vs VGS

![Vth](Vth_Vgs.png)

### VDSAT vs VGS

![VDSAT](Vdsat_Vgs.png)

### ID/W vs gm/ID

![IDW](IdW_vs_gmId.png)

### ft vs gm/ID

![ft-gmId](ft_vs_gmId.png)

### ft vs VGS

![ft-VGS](ft_vs_Vgs.png)

### Body Effect

![BodyEffect](Body_Effect.png)

---

## Key Observations

- Drain current increases with gate voltage
- Body bias increases threshold voltage
- gm/ID decreases in strong inversion
- Channel length modulation impacts saturation current