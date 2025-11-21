# Stochastic Epidemics — From Langevin to Spatial Zombie Invasion

This repository gathers two mini-projects carried out in the *Processus Stochastiques* course (ENSEEIHT, 2nd year).  
We start from the **Langevin description of a Brownian particle** and finish with **agent-based zombie outbreaks** on a lattice, highlighting the role of fluctuations at every scale.

---

## TD1 — Langevin Dynamics & Mean-Field Zombie Model

We solve two emblematic stochastic problems:

1. **Brownian motion of a 50 µm pollen grain in water (300 K)**  
   - Derive the Ornstein-Uhlenbeck SDE for velocity  
   - Prove exponential relaxation of ⟨u(t)⟩ and linear growth of ⟨x²(t)⟩ for t≫τν  
   - Extract τν = 3.23×10⁻⁵ s and Du = 1.92×10⁻⁵ m s⁻¹ from 10⁴ Python trajectories  
   - Verify equipartition: σ²(u) = 3kBT/mp and diffusion coefficient from ⟨x²⟩ vs t

2. **S-Z-R zombie epidemic (Gillespie algorithm)**  
   - Continuous-time Markov chain with transitions  
     S + Z → 2Z (rate βSZ/N)  Z + S → R + S (rate κSZ/N)  
   - Compare deterministic ODE limit with stochastic realisations  
   - Key observation: identical final state, but extinction probability and convergence speed depend on κ/β ratio and initial number of zombies

### 🎯 Objectives

- Master stochastic calculus (Itô, Wiener increments, correlation functions)  
- Link microscopic random forces to macroscopic transport coefficients  
- Quantify how demographic noise alters epidemic thresholds and extinction times

### 📘 Scientific Background

#### Langevin equation
$$
m_p \,\mathrm d u = -3\pi\mu D u\,\mathrm d t + m_p\sqrt{D_u}\,\mathrm d W
\quad\text{with}\quad
\langle\mathrm d W_i\,\mathrm d W_j\rangle=\delta_{ij}\,\mathrm d t
$$

#### Velocity variance & energy
$$
\langle E_c\rangle=\tfrac12 m_p\sigma^2=\frac{3k_B T}{2}
\;\Rightarrow\;
D_u=\frac{2\sigma^2}{3\tau_\nu}
$$

#### Epidemic invariant
$$
Q=\frac{\beta Z}{N}+\frac{(\beta-\kappa)S}{N}
\;\Rightarrow\;
\frac{\mathrm dQ}{\mathrm dt}=0
$$
and
$$
\chi(t)=Z(t)-(N-R(t))
\;\text{satisfies}\;
\frac{\mathrm d\chi}{\mathrm dt}=-(\kappa-\beta)\chi
$$

---

## TD2 — Spatial Stochastic Propagation

We extend the mean-field model to **local contacts on a 2-D lattice**.

- Only nearest-neighbour S-Z pairs can react; simulation stops when no contact remains  
- Sweep lattice sizes 10×10 → 100×100 and κ/β ∈ [0.2, 0.9]  
- Measure extinction time distribution and human-survival probability  
- Compare with deterministic PDE integrated on the same domain

### 🧪 Key Results

| κ/β | lattice | typical extinction time | human survival |
|-----|---------|-------------------------|----------------|
| 0.4 | 10²     | 3×10³ steps             | 0 %            |
| 0.4 | 100²    | 2×10⁴ steps             | 0 %            |
| 0.9 | 100²    | 300 steps               | 95 %           |

- Patchy front morphology emerges; deterministic model misses local extinction clusters  
- For κ/β ≥ 0.8 spatial stochastic model converges **faster** to the healthy state than the ODE  
- Final bulk fractions still match the mean-field prediction, proving that geometry mainly affects **transient routes**, not **endpoints**

---

## 🧰 Repository Structure
