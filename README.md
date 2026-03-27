# Robust PID Control and Plant Uncertainty Analysis for a Mass‑Spring‑Damper System

**Control Systems Project**  
*Status: In progress – theoretical foundations completed; software validation pending.*

## Overview

This project investigates the design and robustness of a PID controller for a second‑order mass‑spring‑damper system. The goal is to meet transient performance specifications (overshoot, settling time, steady‑state error) and evaluate how parameter variations (±20% in mass, stiffness, damping) affect closed‑loop stability and performance. A comparison with a lead‑lag compensator will be performed to highlight trade‑offs.

## Completed Work (without MATLAB/Simulink)

All analytical and manual design steps have been completed. The work so far relies solely on mathematics (pen, paper, and a calculator) and is documented below.

### 1. System Modelling
- Derived the differential equation:
  \[
  m\ddot{x}(t) + c\dot{x}(t) + kx(t) = u(t)
  \]
- Obtained the transfer function:
  \[
  G(s) = \frac{1}{ms^2 + cs + k}
  \]
- Nominal parameters selected for analysis (exact values can be chosen later).

### 2. Performance Specifications
- Transient requirements defined:
  - Maximum overshoot: ≤ 10%
  - Settling time (2% criterion): ≤ 2 s
  - Steady‑state error for a step input: 0 (due to the integrator in the PID)
- Calculated the desired closed‑loop dominant pole locations:
  - Damping ratio \(\zeta\) from overshoot formula
  - Natural frequency \(\omega_n\) from settling time
  - Target poles placed accordingly.

### 3. Analytical PID Tuning
- Used **pole placement** to determine PID gains \((K_p, K_i, K_d)\).
- The closed‑loop characteristic polynomial was matched to a third‑order target polynomial (dominant second‑order pair plus a far‑left real pole).
- Solved for the gains manually (equations derived and solved symbolically).  
- *Gain values have been computed and recorded; they will be verified with simulations.*

### 4. Sensitivity Analysis (Robustness)
- Parameter uncertainty defined as \(\pm 20\%\) variations in \(m\), \(c\), and \(k\).
- Derived the closed‑loop transfer function symbolically in terms of the uncertain parameters and the designed PID gains.
- Calculated **sensitivity functions**:
  \[
  S_p = \frac{\partial T / T}{\partial p / p}
  \]
  for each parameter, evaluated at the nominal operating point.
- Performed a **worst‑case analysis** by substituting extreme parameter values into the characteristic polynomial and estimating pole locations (solved analytically where possible, or via simple root‑finding).

### 5. Stability Margin Calculations
- Using the open‑loop transfer function \(L(s) = C(s)G(s)\) with the obtained PID gains, the gain and phase margins were computed manually:
  - **Gain margin**: solved for the frequency where \(\angle L(j\omega) = -180^\circ\), then \(GM = 1/|L(j\omega)|\).
  - **Phase margin**: solved for the gain crossover frequency (\(|L(j\omega)|=1\)), then \(PM = 180^\circ + \angle L(j\omega)\).
- These margins provide an initial quantitative assessment of robustness.

### 6. Preliminary Lead‑Lag Compensator Design
- To facilitate a later comparison, a **lead compensator** was designed analytically to meet the same transient specifications.
- The compensator’s zero and pole locations were determined based on the required phase lead, and the gain was set to satisfy the steady‑state error requirement.
- A brief comparison between the PID and lead‑lag structures has been outlined (complexity, steady‑state behavior, robustness potential).

## What Remains (to be done with MATLAB/Simulink)

The next phase involves verifying and refining the analytical results using simulation software. Once MATLAB and Simulink are installed, the following tasks will be completed:

- Implement the plant and PID controller in Simulink.
- Validate the step response against the desired specifications.
- Perform robustness analysis with ±20% parameter variations using Simulink simulations.
- Repeat the same steps for the lead‑lag compensator.
- Compute precise gain and phase margins from the simulated frequency responses.
- Generate comparative plots and finalize the report.

## Repository Contents (to be updated)

- `docs/` – Detailed derivations, calculations, and notes (LaTeX or PDF).
- `simulink/` – Simulink models (to be added after software installation).
- `matlab/` – MATLAB scripts for analysis (to be added).
- `README.md` – This file.

---

*Last updated: [Date]*  
*Software status: MATLAB/Simulink not yet installed – all theoretical work completed.*
