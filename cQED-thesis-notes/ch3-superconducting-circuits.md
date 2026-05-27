# Chapter 3 — Cavity QED with Superconducting Circuits

**Pages:** 45–73  
**Reading time:** ~1 hr  
**Status:** ✅ Done

---

## Core idea

This chapter builds the theory from the ground up using circuit language starting with a capacitor and an inductor, ending with the full Jaynes-Cummings Hamiltonian derived from first principles. The goal is to connect electrical engineering intuition to quantum optics. If Chapter 2 gave you the physics, Chapter 3 gives you the hardware.

---

## Part 1: The cavity — from LC circuit to quantum resonator

### The LCR oscillator

Start with a simple parallel LC circuit (inductor L, capacitor C, resistor R for losses). This is a classical harmonic oscillator. The equation of motion for the charge on the capacitor gives oscillations at frequency:

```
ω₀ = 1/√(LC)
```

with decay rate κ = 2/RC. The quality factor Q = ω₀RC is the number of oscillations before the energy decays: the higher, the better for a cavity.

### From lumped elements to transmission line

At microwave frequencies (5 GHz → wavelength ~3 cm), any wire becomes comparable to a wavelength. You can no longer treat a circuit as lumped. The solution: model the transmission line as an infinite series of tiny LC sections, each capturing the inductance and capacitance per unit length.

A **coplanar waveguide (CPW)** resonator is a flat strip of superconducting metal on a silicon chip:
- Centre conductor (width a, typically ~10 µm)
- Gap on either side (width s)
- Ground planes extending on both sides

The ratio s/a determines the characteristic impedance Z₀ (designed to be ~50 Ω to match standard microwave equipment). The 1D geometry is key: by compressing the field into a narrow channel, the energy density is ~10⁶ times higher than a 3D microwave cavity.

**Gaps at both ends** of the centre conductor act as microwave mirrors, small capacitors that reflect most incident power but transmit a little. The quality factor from these coupling capacitors:

```
Q_ext = nπ/(2q²)   where q = ωCᵢₙZ₀
```

By controlling the coupling capacitor size, you engineer κ (and therefore the measurement bandwidth).

### Quantising the LC circuit

The crucial step: the charge q on the capacitor and flux δ = LI in the inductor are **canonical conjugate variables**, exactly like position x and momentum p in quantum mechanics:

```
[q̂, δ̂] = -iℏ
```

This means you can directly write the Hamiltonian as a quantum harmonic oscillator:

```
H = ℏω(a†a + 1/2)
```

where a and a† are photon annihilation and creation operators. The vacuum fluctuations of the voltage across the cavity are:

```
V₀ = √(ℏωᵣ/2C)
```

This zero-point voltage is what couples to the qubit. It's small (~µV) but real and physical — it drives the atom-photon interaction.

### Superconductor-specific physics: kinetic inductance

In a normal metal, inductance comes from magnetic field energy. In a superconductor, there's an additional contribution from the kinetic energy of the Cooper pair condensate, **kinetic inductance** L_K ∝ λ_L² (where λ_L is the London penetration depth). This makes the resonant frequency temperature-dependent and sensitive to magnetic field — important for characterising the device (Ch. 7) and for understanding systematic drifts.

---

## Part 2: The Cooper pair box — the artificial atom

### Why you need non-linearity

A harmonic oscillator has equally spaced energy levels. If you try to use it as a qubit, any microwave drive that hits the 0→1 transition also hits 1→2, 2→3, etc. You can't selectively address just two levels. You need **anharmonicity** , unequally spaced levels. This comes from the Josephson junction.

### The Josephson junction

A sandwich: two superconducting islands separated by a ~1 nm insulating barrier. Cooper pairs can quantum tunnel through this barrier. The junction has two effects:
1. **Josephson energy E_J:** the energy gained when a Cooper pair tunnels — acts like a non-linear kinetic energy
2. **Capacitance C_J:** the geometric capacitance of the junction — contributes to charging energy

The Josephson junction is the only known **dissipation-free non-linear circuit element** at low temperatures. This is what makes superconducting qubits possible.

### The CPB Hamiltonian

The Cooper pair box = superconducting island (total capacitance C_Σ) connected to a reservoir via a Josephson junction, with a gate voltage V_g applied through a gate capacitor C_g.

Two competing energy scales:

| Energy | Symbol | Meaning |
|--------|--------|---------|
| Charging energy | E_C = e²/2C_Σ | Energy cost to add one electron to island |
| Josephson energy | E_J | Energy from Cooper pair tunneling |

**Charge basis Hamiltonian:**

```
H_CPB = 4E_C(N̂ - nₘ/2)² - (E_J/2)Σₙ(|n⟩⟨n+1| + |n+1⟩⟨n|)
```

where N̂ = number of Cooper pairs on island, nₘ = C_g V_g / e (dimensionless gate charge).

The energy levels look like upward-opening parabolas — one for each integer Cooper pair number. Where two parabolas cross (at nₘ = 1), the Josephson coupling lifts the degeneracy, creating an avoided crossing with gap E_J. The eigenstates at this sweet spot are symmetric and antisymmetric superpositions of adjacent charge states.

**The sweet spot:** At nₘ = 1, the transition energy is first-order insensitive to gate charge fluctuations (the two parabolas are tangent). Coherence times are much longer here. The CPB is always operated at this bias point.

**Two-state approximation at nₘ = 1:**  
Near the sweet spot, the CPB looks like a spin-1/2 in a fictitious magnetic field:

```
H_CPB = -(1/2)[4E_C(1-nₘ)σz + E_J σx]
```

with transition energy:
```
ℏωₐ = √(E_J² + (4E_C(1-nₘ))²)
```

This is the Hamiltonian of a qubit. At nₘ = 1: ℏωₐ = E_J.

### The split CPB (SQUID geometry)

To make E_J tunable, split the single junction into two junctions forming a loop. A magnetic flux Φ threading the loop changes the effective Josephson energy:

```
E_J(Φ) = E_J,sum × cos(πΦ/Φ₀)
```

where Φ₀ = h/2e is the superconducting flux quantum. This gives a second knob:
- **Gate voltage** tunes nₘ (electrostatic, like Stark shift)
- **Magnetic flux** tunes E_J (like Zeeman shift)

---

## Part 3: Coupling qubit to cavity — deriving g

This is the most satisfying part of the chapter. The Jaynes-Cummings Hamiltonian is not assumed, it falls out naturally from circuit physics.

### Where the coupling comes from

Inside the cavity, the quantum voltage fluctuations V̂ act on the gate of the CPB:

```
Vₘ = V_DC + V̂
```

Substituting into the CPB Hamiltonian and expanding:

```
H_coupling = 2ℏg(a† + a)N̂
```

where the coupling constant is:

```
g = (eV₀/ℏ)β
```

with V₀ = √(ℏωᵣ/2C) the rms vacuum voltage in the cavity, and β = Cₘ/C_Σ the ratio of gate capacitance to total island capacitance (the voltage division factor).

### Rotating wave approximation

The full coupling has terms like a†σ⁺ (create a photon *and* excite the qubit simultaneously) and aσ⁻ (annihilate a photon *and* de-excite the qubit), these don't conserve the number of excitations and are rapidly oscillating. When ωᵣ + ωₐ ≫ g, |ωᵣ - ωₐ| (always satisfied here), these terms average to zero. Dropping them (the rotating wave approximation) gives:

```
H_coupling = ℏg(a†σ⁻ + aσ⁺)
```

This is exactly the Jaynes-Cummings interaction term from Chapter 2. The circuit approach has reproduced it from scratch.

### How large can g get?

The dimensionless coupling strength:

```
g/ωᵣ = β√(2Z₀/R_K)
```

where R_K = h/e² ≈ 25.8 kΩ is the resistance quantum. Since Z₀ ~ 50 Ω and R_K ~ 25,800 Ω:

```
g/ωᵣ ~ β × √(2 × 50/25800) ~ β × 6%
```

With β engineered close to 1, maximum g/ωᵣ ~ 1–10%.

Remarkably, the **fine structure constant α = η₀/R_K ≈ 1/137** appears in this formula, the fundamental constant measuring the strength of electromagnetic coupling in nature, showing up in a circuit equation.

**Why this is huge:** In 3D atomic cavity QED, g/ω ~ 10⁻⁷. In circuit QED, g/ω ~ 10⁻². That's five orders of magnitude larger. This is what allows circuit QED to reach strong coupling despite the noisy solid-state environment.

---

## Comparison table: circuit QED vs atomic cavity QED

| Parameter | 3D optical | 3D microwave | Circuit QED |
|-----------|-----------|--------------|-------------|
| g/ωᵣ | ~3×10⁻⁷ | ~5×10⁻⁷ | ~10⁻² |
| Cavity lifetime 1/κ | 10 ns | 1 ms | 160 ns |
| Qubit lifetime 1/γ | 61 ns | 30 ms | ~2 µs |
| Vacuum Rabi flops | ~10 | ~5 | ~100 |
| Critical photon number m₀ | 3×10⁻⁴ | 3×10⁻⁸ | ~10⁻⁶ |

Circuit QED wins on number of Rabi flops (~100 vs ~10) because its enormous g compensates for shorter coherence times.

---

## Connections to my background

The LC circuit quantisation is directly analogous to quantising a mechanical oscillator — flux δ = position x, charge q = momentum p. The transmission line analysis (input/output coupling capacitors, S-parameters, Lorentzian lineshape) is standard microwave engineering — same formalism I know from RF instrumentation, just applied to quantum regimes.

The β = Cₘ/C_Σ voltage division factor is a straightforward capacitor voltage divider — the quantum coupling constant comes from the most basic circuit analysis. This is a genuinely beautiful result: the most fundamental constant of quantum electrodynamics (the fine structure constant) shows up in the impedance ratio of two circuit elements.

---

## Open questions

- The rotating wave approximation drops counter-rotating terms (a†σ⁺, aσ⁻). At what coupling strengths does this break down, and what happens in the "ultra-strong coupling" regime? (Not addressed in this thesis — active research area 2010s onwards)
- Kinetic inductance depends on temperature and magnetic field. How large is the resulting frequency drift during an experiment? (Addressed in Ch. 7)
- The two-state approximation for the CPB assumes E_J ≤ 4E_C. In the transmon regime (E_J ≫ E_C), does this approximation still hold? (Addressed in Ch. 4 — yes, with corrections)
