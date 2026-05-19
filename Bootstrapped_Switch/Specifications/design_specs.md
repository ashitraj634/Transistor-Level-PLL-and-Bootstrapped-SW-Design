# Design Specifications

This section details the physical design specifications and environmental parameters established for the bootstrapped NMOS sampling switch design:

- **Technology Node**: SCL 180 nm CMOS process.
- **Supply Voltage ($V_{DD}$)**: 1.8 V (nominal rail voltage).
- **Analog Input Voltage Range**: 1.0 Vpp sinusoidal signal centered around a common-mode voltage of 0.9 V ($0.4\text{ V} \le V_{in} \le 1.4\text{ V}$).
- **Maximum Input Signal Frequency**: >= 10 MHz.
- **Switch Device Configuration**: High-speed NMOS transistor ($M_1$) utilizing a bootstrap gate-drive circuit.
- **Output Load Capacitance ($C_1$)**: 5.0 pF (equivalent sampling hold capacitor).
- **Bootstrap Capacitor ($C_b$)**: 2.0 pF (sized to balance gate charge sharing without taking up excessive silicon area).
