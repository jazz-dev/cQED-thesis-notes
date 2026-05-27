# Concept: The Jaynes-Cummings Model

*Cross-reference: Ch. 2 (theory), Ch. 3 (circuit derivation), Ch. 8 (experiments)*

---

## What it is

The Jaynes-Cummings model is the simplest possible model of a quantum system interacting with light. It describes one two-level system (atom, qubit) coupled to one mode of the electromagnetic field (a single cavity mode). Despite its simplicity, it captures the essential physics of strong coupling and is exactly solvable.

## The Hamiltonian

```
H_JC = ℏωᵣ(a†a + 1/2) + ℏ(ωₐ/2)σz + ℏg(a†σ⁻ + aσ⁺)
```

**Term 1:** Photon field. a†a is the photon number operator — a†a|n⟩ = n|n⟩. Energy = nℏωᵣ.  
**Term 2:** Two-level atom. σz = |e⟩⟨e| - |g⟩⟨g|. Energy +ℏωₐ/2 if excited, -ℏωₐ/2 if ground.  
**Term 3:** Coupling. a†σ⁻ = create photon and de-excite atom. aσ⁺ = destroy photon and excite atom. Rate = g.

## Why the rotating wave approximation

The full dipole coupling is H_int = ℏg(a† + a)(σ⁺ + σ⁻). Expanding: four terms.

- aσ⁺ — destroy photon, excite atom ✅ (conserves excitation number)
- a†σ⁻ — create photon, de-excite atom ✅ (conserves excitation number)
- a†σ⁺ — create photon AND excite atom ❌ (changes excitation number by 2, oscillates at ωᵣ + ωₐ)
- aσ⁻ — destroy photon AND de-excite atom ❌ (changes excitation number by 2, oscillates at ωᵣ + ωₐ)

When ωᵣ + ωₐ ≫ g (always true in this experiment), the last two terms average to zero over any relevant timescale. Dropping them is the rotating wave approximation. What remains is the JC Hamiltonian above.

## The conserved quantity

Because each term in H_JC either raises a photon and lowers an atom excitation, or vice versa, the **total number of excitations** N = a†a + |e⟩⟨e| is conserved: [H_JC, N] = 0.

This means the Hamiltonian block-diagonalises into sectors of fixed N. Each sector (called the N-excitation manifold) is just a 2×2 matrix, making the problem exactly solvable.

## Exact energy levels

Energies in the n-excitation manifold:

```
E±,n = nℏωᵣ ± (ℏ/2)√(4ng² + Δ²)
```

where Δ = ωₐ - ωᵣ is the detuning.

Ground state (zero excitations): E_g,0 = -ℏΔ/2

## Two regimes from the exact solution

**Resonant (Δ = 0):**
```
E±,n = nℏωᵣ ± ℏg√n
```
Splitting = 2g√n. States are equal superpositions of |g,n⟩ and |e,n-1⟩.

**Dispersive (|Δ| ≫ g):** Taylor expand in g/Δ:
```
E±,n ≈ nℏωᵣ ± (ℏ/2)(Δ + ng²/Δ)
```
The g²/Δ term is the dispersive shift — small but physically important.

## Physical picture: the dressed states

At resonance, the bare states |g,n⟩ (ground, n photons) and |e,n-1⟩ (excited, n-1 photons) are degenerate. The coupling mixes them into dressed states:

```
|+,n⟩ = (|g,n⟩ + |e,n-1⟩)/√2   "phobit" (more photon-like)
|-,n⟩ = (|g,n⟩ - |e,n-1⟩)/√2   "quton" (more qubit-like)
```

Neither is purely an atom or a photon — they are genuinely entangled states of the combined system.

## Vacuum Rabi oscillations

Start with the qubit excited and zero photons: |ψ(0)⟩ = |e,0⟩. This is not an eigenstate — it's a superposition of the two n=1 dressed states. The time evolution:

```
|ψ(t)⟩ = cos(gt)|e,0⟩ - i sin(gt)|g,1⟩
```

The excitation oscillates between atom (|e,0⟩) and photon (|g,1⟩) at frequency g. This is the vacuum Rabi oscillation — "vacuum" because it occurs even with zero input photons, driven by zero-point fluctuations.

## What "strong coupling" means geometrically

Plot the dressed state energies as a function of detuning Δ. At Δ = 0 there is an **avoided crossing** — the two bare state energies would cross, but the coupling pushes them apart. The minimum gap is 2g.

Strong coupling (g > κ, γ) means this gap is resolvable — the linewidths of the two dressed states (set by decay rates κ and γ) are smaller than the splitting 2g. This is the condition for observing two distinct peaks in the transmission spectrum.

## Connections to control theory

The Jaynes-Cummings model is a bilinear control system: the control input (photon field) couples multiplicatively to the state (atom). The rotating wave approximation is equivalent to neglecting rapidly oscillating terms in the averaging method for ODEs. The transfer function from input field to output transmission has poles at the dressed state frequencies — this is why the transmission spectrum directly reveals the energy splitting.
