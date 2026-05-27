# Chapter 2 — Cavity Quantum Electrodynamics

**Pages:** 34–44  
**Reading time:** ~1.5 hrs  
**Status:** ✅ Done

---

## Core idea

This chapter is the theoretical foundation of the entire thesis. It introduces the Jaynes-Cummings Hamiltonian, works through the resonant and dispersive regimes, and then introduces the **strong dispersive regime** — a new regime that circuit QED can access but atomic systems cannot. Everything in the experimental chapters is this theory playing out in real measurements.

---

## The Jaynes-Cummings Hamiltonian

The governing equation for a two-level atom interacting with a single cavity mode:

```
H_JC = ℏωᵣ(a†a + 1/2) + ℏ(ωₐ/2)σz + ℏg(a†σ⁻ + aσ⁺)
```

Three terms, three physical meanings:

| Term | Physical meaning |
|------|-----------------|
| ℏωᵣ(a†a + 1/2) | Energy of the photon field — each photon carries ℏωᵣ |
| ℏ(ωₐ/2)σz | Energy of the two-level atom — ground or excited, separated by ℏωₐ |
| ℏg(a†σ⁻ + aσ⁺) | Coupling — atom absorbs a photon (σ⁺a) or emits one (a†σ⁻) at rate g |

The three rates that determine what regime you're in:
- **g** — coupling strength (coherent exchange rate)
- **κ** — cavity photon decay rate (κ = ωᵣ/Q)
- **γ** — qubit decay rate into non-cavity channels

**Strong coupling:** g > κ, γ — the atom and photon exchange energy faster than either can be lost.

---

## Regime 1: Resonant (ωₐ = ωᵣ)

When atom and cavity are at the same frequency, they can no longer be treated as separate. The energy eigenstates become **dressed states** — joint atom-photon superpositions:

```
|ψ±, n⟩ = (|g,n⟩ ± |e,n-1⟩) / √2
```

Energy splitting between the two dressed states at n excitations: **2g√n**

The n=1 splitting is 2g. This shows up experimentally as **two peaks** in the cavity transmission spectrum instead of one — the vacuum Rabi splitting. Observing two resolved peaks is the definitive proof of strong coupling.

**Intuition:** Think of two tuning forks at the same frequency placed near each other. They stop vibrating independently and start beating together as a coupled pair. The beat frequency is 2g.

**Vacuum Rabi oscillations:** Even with no photons to start, zero-point fluctuations of the electromagnetic field drive the atom to oscillate between ground and excited state. This is "stimulated by the vacuum" — one of the cleaner demonstrations that quantum fields are never truly empty.

**Purcell effect:** Even outside strong coupling (g < κ), the cavity modifies the atom's decay:
- If cavity is resonant with atom: decay enhanced, rate → Γ_eff = g²/κ
- If cavity is far off-resonant: decay suppressed — the photon can't fit in the cavity, so it can't be emitted

This is directly useful for quantum computing: engineering the cavity detuning lets you control qubit lifetime.

---

## Regime 2: Dispersive (Δ = ωₐ - ωᵣ ≫ g)

When the atom is far detuned from the cavity, no real photon exchange occurs. But perturbation theory (to second order in g/Δ) gives a modified Hamiltonian:

```
H_disp ≈ ℏ(ωᵣ + χσz)(a†a + 1/2) + ℏωₐσz/2
```

where **χ = g²/Δ** is the dispersive shift.

Two equivalent ways to read this Hamiltonian:

**Reading 1 — cavity perspective:**  
The cavity frequency depends on the qubit state:
- Qubit in |0⟩: cavity resonance at ωᵣ - χ  
- Qubit in |1⟩: cavity resonance at ωᵣ + χ

→ Measure the cavity frequency → learn the qubit state. This is **dispersive readout**.

**Reading 2 — qubit perspective:**  
The qubit frequency shifts by 2nχ where n is the photon number in the cavity. This is the **AC Stark shift** (or "light shift"). Each photon in the cavity shifts the qubit by χ.

→ Measure the qubit frequency → learn how many photons are in the cavity.

**Why this is so powerful:** Both measurements are **QND — quantum non-demolition**. The dispersive Hamiltonian commutes with both the photon number and qubit state operators, meaning the measurement doesn't change what it's measuring. You can repeat it to improve fidelity.

**Critical photon number ncrit = Δ²/4g²:**  
The dispersive approximation requires that the photon number stays below this limit. Above ncrit, the perturbation expansion diverges and you're back in the resonant regime. This sets an upper limit on measurement power.

**Indirect decay in the dispersive regime:**  
The qubit acquires a small photonic component (of order g/Δ) and can decay through the cavity at rate γ_κ ≈ (g/Δ)²κ. Similarly photons acquire a qubit-like component and decay through the qubit at rate κ_γ ≈ (g/Δ)²γ. Both rates are small in the dispersive limit — the cavity protects the qubit from its environment.

---

## Regime 3: Strong dispersive (χ > γ, κ) — new to circuit QED

This is Schuster's contribution to cQED theory, and it defines a new frontier.

In the dispersive regime you have the AC Stark shift: each photon in the cavity shifts the qubit by χ. In the *weak* dispersive regime (χ < γ), these shifts are smaller than the qubit linewidth — they blur together into a broadened peak. You can't tell how many photons are present.

In the **strong dispersive regime** (χ > γ), each shift is larger than the qubit linewidth. The qubit spectrum splits into a separate peak for each photon number:
- Peak at ωₐ — zero photons in cavity
- Peak at ωₐ - 2χ — one photon
- Peak at ωₐ - 4χ — two photons
- Peak at ωₐ - 6χ — three photons
- ...

You can literally read off the photon number distribution from the qubit spectrum. This is called **photon number splitting** and it's the key result of Chapter 8.

No atomic cavity QED system had reached this regime before. The enormous g values in circuit QED (from the large dipole moment and compressed 1D field) are what make it possible.

---

## The cQED phase diagram (Fig. 2.4)

Schuster plots a phase diagram in g/Γ vs Δ/Γ space (where Γ = max[γ, κ]):

| Region | Condition | Physics |
|--------|-----------|---------|
| Blue (resonant) | Δ ≈ 0 | Vacuum Rabi oscillations, dressed states |
| Red (weak dispersive) | χ < Γ | QND readout using many photons, no single-photon resolution |
| White (strong dispersive) | χ > Γ, g/Δ < 1 | Single photon resolution, QND with <1% demolition |
| Green (quasi-dispersive) | χ > Γ, g/Δ ~ 1 | Single photon sensitive but larger back-action |
| Yellow (anharmonic cavity) | nκ < 1 | Cavity itself becomes non-linear at single photon level |

Circuit QED sits in the top-right corner — deep in the strong dispersive regime that Rydberg atoms and alkali atoms couldn't reach.

---

## Key equations summary

| Equation | Meaning |
|----------|---------|
| g > κ, γ | Strong coupling condition |
| χ = g²/Δ | Dispersive shift per photon |
| ncrit = Δ²/4g² | Maximum photon number in dispersive regime |
| 2g√n | Vacuum Rabi splitting at n excitations |
| γ_κ ≈ (g/Δ)²κ | Qubit decay rate through cavity (Purcell, dispersive) |
| χ > γ, κ | Strong dispersive condition — photon number resolution |

---

## Connections to my background

From control systems: the dispersive readout is essentially a **state observer** — you infer the hidden state (qubit) from an indirect output measurement (cavity frequency). The QND condition means the observation doesn't perturb the state, analogous to a non-invasive sensor in classical control. The input-output formalism in the appendix (Walls & Milburn Ch. 7) is essentially a transfer function approach to the cavity-qubit system.

---

## Open questions

- The dispersive Hamiltonian is derived to second order in g/Δ. How do fourth-order terms matter experimentally? (Section 8.3.2 addresses this — they give a photon-number-dependent cavity anharmonicity)
- What exactly causes dephasing in the dispersive regime when photons are present? (The photon number fluctuations cause the qubit frequency to jump randomly — addressed in Ch. 8)
- Is there a quantum version of the Bode gain-phase relationship constraining what you can learn vs what back-action you must impose? (Related to the Heisenberg limit on measurement)
