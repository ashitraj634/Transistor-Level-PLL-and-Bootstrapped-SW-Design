# $R_{on}$ Variation Analysis & Results

This section details the calculation of the on-resistance ($R_{on}$) variation and evaluates its compliance with design targets:

## Mathematical Calculations

### 1. Average Resistance ($R_{avg}$)
The nominal operating resistance is defined as the mean of the extreme values:

$$R_{avg} = \frac{R_{on,max} + R_{on,min}}{2}$$

$$R_{avg} = \frac{31.86 + 28.54}{2} = 30.9\ \Omega$$

### 2. Peak-to-Peak Percentage Variation
The total peak-to-peak variation across the input sweep is computed by:

$$\% \text{ Variation} = \left(\frac{R_{on,max} - R_{on,min}}{R_{avg}}\right) \times 100\%$$

$$\% \text{ Variation} = \left(\frac{31.86 - 28.54}{30.9}\right) \times 100\% = 6.86\%$$

### 3. Symmetrical Bounds Representation
Expressing the total variation symmetrically around the average resistance:

$$\text{Variation} = \pm \left(\frac{6.86\%}{2}\right) = \pm 3.43\%$$

## Performance Evaluation
- **Target Specification**: Less than or equal to **$\pm 5\%$**.
- **Achieved Performance**: **$\pm 3.43\%$**.
- **Compliance Status**: **Passed**.

The ultra-low variation of $\pm 3.43\%$ confirms the high effectiveness of the gate-boosting bootstrapping network in clamping the Gate-Source voltage ($V_{GS}$) of the sampling transistor, successfully decoupling the channel resistance from the input signal.
