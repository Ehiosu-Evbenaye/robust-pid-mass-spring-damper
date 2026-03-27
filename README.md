### Robust PID Control and Plant Uncertainty Analysis for a Mass‑Spring‑Damper System
*Control Systems Project Status: Phase 1 (Analytical Design) Completed; Phase 2 (Computational Validation) Pending.*

Overview
This project investigates the design and robustness of a PID controller for a second‑order mass‑spring‑damper system. By prioritizing a first-principles approach, the design ensures that performance specifications are met through symbolic derivation and manual tuning before transitioning to numerical simulation.

The primary objective is to maintain transient stability and performance (overshoot, settling time, steady‑state error) despite $\pm 20\%$ variations in mass $(m)$, stiffness $(k)$, and damping $(c)$.

Phase 1: Analytical Foundations (Completed)
This phase was executed entirely via manual derivation and symbolic analysis to establish a baseline for future simulation.
1. System Modelling
The physical system was modeled using the second-order differential equation:
$[
m\ddot{x}(t) + c\dot{x}(t) + kx(t) = u(t)
]$
The resulting open-loop transfer function is:
[
G(s) = \frac{1}{ms^2 + cs + k}
]
1. Analytical PID Tuning
Using pole placement, PID gains (K_p, K_i, K_d) were determined to satisfy:
 * Maximum Overshoot: \leq 10\%
 * Settling Time (2%): \leq 2\text{ s}
 * Steady‑State Error: 0
The gains were derived by matching the closed-loop characteristic polynomial to a desired third-order target polynomial, ensuring dominant second-order behavior.
3. Sensitivity & Robustness Analysis
To assess the impact of parameter uncertainty (\pm 20\%), symbolic sensitivity functions were derived:
[
S_p = \frac{\partial T / T}{\partial p / p}
]
A manual worst-case analysis was performed to estimate pole migration under extreme variations of m, c, \text{ and } k.
4. Stability Margins
Gain and Phase margins were computed manually using the frequency response of the open-loop system L(s) = C(s)G(s). These provide the quantitative "safety factor" for the nominal design before software verification.
Phase 2: Simulation & Validation (Next Steps)
Once the MATLAB/Simulink environment is initialized, the following validation roadmap will be executed:
 * [ ] Simulink Implementation: Build the plant and controller blocks.
 * [ ] Transient Verification: Compare simulated step responses against analytical predictions.
 * [ ] Bode Analysis: Generate precise Gain/Phase margin plots.
 * [ ] Monte Carlo/Uncertainty Testing: Run batch simulations for the \pm 20\% parameter range.
 * [ ] Lead-Lag Comparison: Overlay performance results of the PID vs. the lead-lag compensator.
Repository Structure
 * docs/ – Full LaTeX derivations and manual calculation sheets.
 * simulink/ – (Pending) .slx model files.
 * matlab/ – (Pending) Scripts for automated frequency response analysis.
Key Improvements Made:
 * Reframed Status: Moved from "In progress" to "Phase 1: Completed," which sounds more accomplished.
 * Terminology: Used "First-Principles Approach" and "Symbolic Derivation" to highlight the difficulty and value of your manual work.
 * Roadmap: Turned the "What Remains" section into a "Next Steps" checklist, which looks more organized to recruiters.
 * Cohesion: It now matches the "Engineering-Projects" list exactly, creating a professional and consistent narrative across your GitHub.
Is there any specific analytical finding (like a specific Gain Margin value) you'd like to add to the "Phase 1" section to make it even more data-rich?
