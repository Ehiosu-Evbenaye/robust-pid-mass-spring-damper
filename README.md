### Robust PID Control and Plant Uncertainty Analysis for a Mass‑Spring‑Damper System
*Control Systems Project Status: Phase 1 (Analytical Design) Completed; Phase 2 (Computational Validation) Pending.*

Overview
This project investigates the design and robustness of a PID controller for a second‑order mass‑spring‑damper system. By prioritizing a first-principles approach, the design ensures that performance specifications are met through symbolic derivation and manual tuning before transitioning to numerical simulation.

The primary objective is to maintain transient stability and performance (overshoot, settling time, steady‑state error) despite $\pm 20\%$ variations in mass $(m)$, stiffness $(k)$, and damping $(c)$.

## Phase 1: Analytical Foundations (Completed)<br>
This phase was executed entirely via manual derivation and symbolic analysis to establish a baseline for future simulation.
1. System Modelling<br>
The physical system was modeled using the second-order differential equation:<br>
$[
m\ddot{x}(t) + c\dot{x}(t) + kx(t) = u(t)
]$ <br>
The resulting open-loop transfer function is:<br>
$[
G(s) = \frac{1}{ms^2 + cs + k}
]$ <br>
<br>

2. Analytical PID Tuning<br>
Using pole placement, PID gains $(K_p, K_i, K_d)$ were determined to satisfy:
 * Maximum Overshoot: $\leq 10\%$
 * Settling Time (2%): $\leq 2\text{ s}$
 * Steady‑State Error: 0 <br>
 
The gains were derived by matching the closed-loop characteristic polynomial to a desired third-order target polynomial, ensuring dominant second-order behavior.
<br>
<br>

3. Sensitivity & Robustness Analysis<br>
To assess the impact of parameter uncertainty $(\pm 20\%)$, symbolic sensitivity functions were derived:
$[
S_p = \frac{\partial T / T}{\partial p / p}
]$
A manual worst-case analysis was performed to estimate pole migration under extreme variations of $m, c, \text{ and } k$.
<br>

4. Stability Margins<br>
Gain and Phase margins were computed manually using the frequency response of the open-loop system $L(s) = C(s)G(s)$. These provide the quantitative "safety factor" for the nominal design before software verification.


## Phase 2: Simulation & Validation (Next Steps)<br>
Once the MATLAB/Simulink environment is initialized, the following validation roadmap will be executed:
 * [ ] Simulink Implementation: Build the plant and controller blocks.
 * [ ] Transient Verification: Compare simulated step responses against analytical predictions.
 * [ ] Bode Analysis: Generate precise Gain/Phase margin plots.
 * [ ] Monte Carlo/Uncertainty Testing: Run batch simulations for the $\pm 20\%$ parameter range.
 * [ ] Lead-Lag Comparison: Overlay performance results of the PID vs. the lead-lag compensator.
