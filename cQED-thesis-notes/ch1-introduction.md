# Chapter 1 — Introduction

**Pages:** 18–33  
**Reading time:** ~30 min  
**Status:** ✅ Done

---

## Core idea

Schuster's thesis is the founding document of circuit QED. The central question it asks is: can we do the quantum optics experiment of trapping an atom inside a mirror box — cavity QED — but replace the atom with a superconducting circuit and the mirror box with a microwave resonator on a chip? The answer turns out to be yes, and in some ways the chip version is *better* than the real thing.

---

## Why quantum computers, and why this approach

The motivation is quantum computation. Classical computers use bits (0 or 1). Quantum computers use qubits — quantum bits that can be 0, 1, or any superposition of both simultaneously. This enables algorithms that are exponentially faster for specific problems: factoring large numbers (Shor's algorithm), simulating quantum chemistry, optimisation.

The central challenge is **decoherence** — any interaction between the qubit and its environment destroys the quantum state. There are two distinct processes:

- **Relaxation (T₁):** the qubit loses energy to the environment and falls from |1⟩ to |0⟩
- **Dephasing (T₂):** the qubit's phase — the relative weight between |0⟩ and |1⟩ in a superposition — gets scrambled without energy loss

The fundamental tension: qubits must be isolated enough to preserve coherence, but coupled enough to be controlled and read out. These demands pull in opposite directions.

---

## What cavity QED taught us

Before circuits, physicists had already demonstrated remarkable physics with real atoms trapped inside optical or microwave cavities. The key idea: if you trap a photon between two highly reflective mirrors, it bounces back and forth many times before escaping. The atom sitting inside "sees" a very different electromagnetic environment than it would in free space.

Two important effects:

**Purcell effect:** The cavity suppresses spontaneous emission if the atom's frequency doesn't match any cavity mode. The atom simply can't emit — nowhere for the photon to go. Coherence is protected.

**Vacuum Rabi oscillations:** If the atom and cavity are resonant, a single quantum of energy oscillates back and forth between atom and photon. The atom emits a photon, the photon bounces back, the atom reabsorbs it — over and over. This requires **strong coupling**: the exchange rate g must exceed both the cavity decay rate κ and the atom decay rate γ.

Strong coupling had been achieved with real atoms (Caltech optical group, Paris microwave Rydberg atom group) but required enormous experimental effort — catching single atoms flying through a cavity at precisely the right moment.

---

## The circuit QED idea

The thesis proposes doing all of this on a chip using:

**The cavity:** a coplanar waveguide (CPW) resonator — a flat strip of superconducting metal on silicon. Gaps in the centre pin at both ends act as microwave mirrors. Photons bounce back and forth up to 10⁶ times. The 1D geometry compresses the electromagnetic field into a tiny cross section, increasing energy density by 10⁶ compared to a 3D microwave cavity.

**The artificial atom:** a Cooper pair box (CPB) — a tiny superconducting island connected to a reservoir via a Josephson junction. Cooled to ~20 mK, it behaves like a two-level quantum system. Its effective dipole moment is ~10,000× larger than a real alkali atom because billions of electrons act coherently.

These two effects — massive dipole moment and compressed field — combine to give coupling constants g that are orders of magnitude larger than atomic systems. This is how circuit QED reaches strong coupling despite the noisier solid-state environment.

**Reading out the qubit:** rather than directly probing the qubit, you send a microwave signal through the cavity. The qubit's state shifts the cavity's resonant frequency slightly — you read that shift. This is the dispersive readout scheme (developed fully in later chapters), and it means you never have to directly hit the qubit.

---

## Key numbers to remember

| Quantity | Symbol | What it means |
|----------|--------|---------------|
| Coupling strength | g | How fast atom and photon exchange energy |
| Cavity decay rate | κ | How fast photons leak out |
| Qubit decay rate | γ | How fast the qubit relaxes on its own |
| Strong coupling condition | g > κ, γ | The regime everything interesting happens in |
| Operating temperature | ~20 mK | Colder than outer space |
| Qubit frequency | ~5–10 GHz | Microwave, not optical |

---

## What Chapter 1 sets up for the rest of the thesis

| Chapter | What it does |
|---------|-------------|
| Ch. 2 | Full quantum theory — Jaynes-Cummings, dispersive limit, strong dispersive |
| Ch. 3 | How to build it — LC circuits, CPB, deriving g from a circuit diagram |
| Ch. 4 | Decoherence in the CPB — and why the transmon fixes it |
| Ch. 8 | Experiments — vacuum Rabi splitting, dispersive readout, photon number splitting |
| Ch. 9 | Time domain — qubit gates, single shot readout, single photon source |

---

## Open questions

- How exactly does the rotating wave approximation work when deriving the coupling Hamiltonian? (addressed in Ch. 3)
- What limits T₁ and T₂ in the CPB specifically — charge noise, flux noise, or something else? (addressed in Ch. 4)
- The Purcell effect can both protect and accelerate decay depending on detuning — is there an optimal detuning? (addressed in Ch. 2)
