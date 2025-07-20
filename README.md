# 🔋 Battery SOC Estimation using A-SRUKF (SIL Simulation)

## 📌 Project Overview

This project presents a MATLAB/Simulink-based implementation of a **State of Charge (SOC) Estimation** algorithm for lithium-ion batteries using the **Adaptive Square Root Unscented Kalman Filter (A-SRUKF)**. A **2-RC Equivalent Circuit Model (ECM)** of the battery is used to simulate terminal behavior, and the estimator is tested through a **Software-in-the-Loop (SIL)** simulation environment.

## 🛠 Key Components

- **Battery Model**: A second-order (2-RC) ECM model simulated in Simulink. Parameters such as internal resistances and capacitances vary with SOC and temperature using 2D lookup tables.
- **A-SRUKF Algorithm**: SOC estimation is implemented in a MATLAB Function block using an adaptive variant of the Square Root UKF for increased numerical stability and noise adaptation.
- **SIL Testing**: The estimator is tested with current, voltage, and temperature data directly within the simulation loop (without hardware). It outputs SOC, estimated terminal voltage, and estimation error.

## 🎯 Objectives

- Simulate a dynamic battery behavior using a 2-RC ECM.
- Implement the A-SRUKF algorithm in MATLAB Function block for real-time SOC estimation.
- Validate estimator performance using SIL methodology.
- Analyze estimation accuracy through comparison with ECM-generated terminal voltage and known SOC trajectory.

## ⚙️ Simulation Setup

- **Inputs**:
  - Current profile (discharge/charge)
  - Terminal voltage from ECM
  - Temperature profile or fixed value
- **Outputs**:
  - Estimated SOC
  - Estimated terminal voltage
  - Estimation error

- **Tools Used**:
  - MATLAB R2018
  - Simulink
  - Custom MATLAB Function block for A-SRUKF

## 📈 Results

- The estimator successfully tracked the SOC over a wide range of current and voltage conditions.
- The estimated terminal voltage closely matched the ECM's actual output.
- Time-series plots confirmed the accuracy and responsiveness of the A-SRUKF estimator.

## 🧠 Algorithms Used

- **Adaptive Square Root Unscented Kalman Filter (A-SRUKF)**:
  - Nonlinear estimation method suitable for dynamic battery systems.
  - Provides better numerical stability and real-time adaptability.
  - Accounts for modeling uncertainty and noise covariance tuning.

## ✅ Project Status

- [x] ECM modeled in Simulink
- [x] A-SRUKF implemented in MATLAB Function block
- [x] Integrated and tested in SIL environment
- [x] Simulation results analyzed and documented

## 📝 Notes

> This work focuses solely on **Software-in-the-Loop (SIL)** simulation. Real-time HIL/OPAL-RT testing is not included in this repository version.

## 📚 References

1. He, H., Xiong, R., Fan, J. (2011). *Evaluation of lithium-ion battery equivalent circuit models for state of charge estimation by an experimental approach*. Energies.
2. Plett, G. L. (2004). *Extended Kalman filtering for battery management systems of LiPB-based HEV battery packs: Part 3. State and parameter estimation*. Journal of Power Sources.

---




