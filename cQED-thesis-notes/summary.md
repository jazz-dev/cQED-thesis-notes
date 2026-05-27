# What I Learned — Thesis Summary

*This is the answer I'd give if someone asked me to summarise what Schuster's thesis is about and what I took from it.*

---

## The one-sentence version

Schuster took the idea of trapping an atom inside a mirror box (cavity QED) and rebuilt it on a microchip using a superconducting circuit as the artificial atom and a strip of wire as the cavity — then used it to demonstrate strong coupling, dispersive qubit readout, and individual photon number resolution for the first time in a solid-state system.

---

## The four-minute version

### What the system is

The thesis demonstrates **circuit QED** — quantum optics on a chip. The two components are:

A **coplanar waveguide resonator**: a flat strip of superconducting metal on silicon, with small gaps at each end acting as microwave mirrors. Photons bounce back and forth up to a million times. Cooled to 20 mK, quantum mechanically this is a harmonic oscillator whose energy levels are individual microwave photons.

A **Cooper pair box (CPB)**: a nanometre-scale superconducting island connected to a reservoir via a Josephson junction. Cooled to 20 mK, this behaves like an artificial two-level atom. Its qubit states are superpositions of zero and one Cooper pair on the island. Its effective dipole moment is ~10,000× larger than a real atom.

These two components are fabricated on the same chip. The cavity sits between input/output transmission lines. The qubit sits at the electric field maximum of the cavity.

### The key physics: three regimes

**Resonant regime (Δ ≈ 0):**  
When qubit and cavity are at the same frequency, they hybridise into dressed states. A single quantum of energy oscillates back and forth between atom and photon at rate g — the vacuum Rabi oscillation. The transmission spectrum shows two peaks separated by 2g instead of one. Observing this is proof of strong coupling (g > κ, γ).

**Dispersive regime (Δ ≫ g):**  
When qubit and cavity are far off-resonance, no real exchange occurs but a residual coupling χ = g²/Δ shifts their frequencies in a state-dependent way. The cavity frequency shifts by ±χ depending on whether the qubit is |0⟩ or |1⟩. This enables reading the qubit state by measuring the cavity — the dispersive readout. It's quantum non-demolition: you learn the qubit state without directly disturbing it.

**Strong dispersive regime (χ > γ, κ):**  
New to circuit QED. Each photon in the cavity shifts the qubit frequency by 2χ — larger than the qubit linewidth. The qubit spectrum splits into individual peaks, one per photon number. You can read the photon distribution directly from spectroscopy. No atomic system had reached this regime before.

### The experimental results

1. **Vacuum Rabi splitting** — two peaks in transmission spectrum confirmed strong coupling. Coupling ratio 4g/(κ+γ) = 16 (CPB) and 10 (transmon).

2. **Dispersive qubit readout** — phase shift of cavity transmission used to read qubit state. >95% visibility demonstrated. Foundation of all cQED measurement.

3. **AC Stark effect** — qubit frequency shifts proportional to photon number. Measurement-induced dephasing observed and quantified.

4. **Photon number splitting** — ~10 resolved peaks in qubit spectrum, each corresponding to a different Fock state of the cavity. First demonstration of strong dispersive regime in any system.

5. **On-demand single photon source** — qubit state mapped onto cavity photon state with controllable superposition. Single photons emitted on demand.

6. **The transmon** — modified CPB with large E_J/E_C ratio, exponentially suppressing charge noise sensitivity. Vacuum Rabi splitting 20× larger. Now the dominant qubit in all major superconducting quantum computers.

### Why it matters

The transmon qubit and dispersive readout scheme introduced in this thesis are the hardware and measurement foundation of IBM Quantum, Google Quantum AI, and most other superconducting quantum computing platforms. Every quantum volume benchmark, every Shor's algorithm demonstration on superconducting hardware traces back to the architecture established here.

---

## Things I'd want to understand better

- The full quantum trajectory theory behind single-shot measurement and how fidelity is optimised (Ch. 9, Wiseman & Milburn)
- How quantum feedback — measuring the cavity continuously and acting on the result — changes the qubit's dynamics (directly relevant to QuMaC work on quantum feedback and state estimation)
- The transition from dispersive readout to projective measurement — when does a weak continuous measurement become a strong projective one?
- How two-qubit gates work in this architecture (Ch. 10 outlook — not demonstrated in this thesis)

---

*Last updated: May 2026*
