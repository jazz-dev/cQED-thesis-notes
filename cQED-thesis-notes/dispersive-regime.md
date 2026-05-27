# Concept: The Dispersive Regime and Dispersive Readout

*Cross-reference: Ch. 2 (theory), Ch. 3 (circuit implementation), Ch. 8 (dispersive readout experiments)*

---

## What it is

The dispersive regime is the regime where the qubit and cavity are far off-resonance (|Δ| = |ωₐ - ωᵣ| ≫ g). No real photon exchange occurs — the qubit and cavity retain their individual characters. But a subtle residual interaction shifts their frequencies in a state-dependent way. This is the basis of almost all qubit readout in superconducting quantum computing today.

---

## How to derive the dispersive Hamiltonian

Starting from the Jaynes-Cummings Hamiltonian, apply a unitary transformation (Schrieffer-Wolff or Baker-Hausdorff) that eliminates the off-diagonal coupling to second order in g/Δ. The result:

```
H_disp = ℏ(ωᵣ + χσz)(a†a + 1/2) + ℏωₐσz/2
```

where **χ = g²/Δ** is the dispersive shift.

Two ways to rewrite this, highlighting different physics:

**Cavity perspective:**
```
H_disp = ℏ(ωᵣ ± χ)a†a + ...
```
The cavity resonance frequency shifts by +χ if qubit is excited, -χ if qubit is ground.

**Qubit perspective:**
```
H_disp = ℏ(ωₐ + 2χa†a)σz/2 + ...
```
The qubit transition frequency shifts by 2nχ where n = ⟨a†a⟩ is the mean photon number (AC Stark shift). Includes a vacuum shift g²/Δ (Lamb shift) even at zero photons.

---

## The dispersive readout protocol

1. Send a microwave probe tone at the bare cavity frequency ωᵣ
2. The qubit being in |0⟩ or |1⟩ shifts the cavity resonance by ∓χ
3. Detect the phase or amplitude of the transmitted signal — it encodes the qubit state
4. Infer qubit state from the detected signal

**Why this protects the qubit:**  
The probe tone never resonantly drives the qubit (it's at ωᵣ, not ωₐ). The information about the qubit state is encoded in a phase shift of the cavity, not in direct qubit excitation. This is a fundamentally indirect measurement.

**QND condition:**  
The dispersive Hamiltonian commutes with σz (qubit state) — meaning the measurement doesn't change which state the qubit is in. This makes it (approximately) quantum non-demolition. You can repeat the measurement and get consistent results, increasing fidelity.

*In practice:* Not perfectly QND because higher-order terms in g/Δ introduce small mixing. The demolition probability per measurement is approximately (g/Δ)² < 1%.

---

## The measurement in terms of homodyne detection

Experimentally: send a continuous microwave tone at ωᵣ through the cavity. Mix the transmitted signal with a local oscillator at the same frequency (homodyne detection). The output is a voltage proportional to the phase shift of the transmitted signal.

Phase shift at resonance:
```
φ = arctan(δω/(κ/2))
```
where δω is how far the cavity was shifted from ωᵣ.

When the qubit is in |0⟩: δω = -χ → phase shifts one way  
When the qubit is in |1⟩: δω = +χ → phase shifts the other way

The readout contrast is maximised when χ ~ κ/2 (the shift equals half the cavity linewidth).

---

## The AC Stark effect

When photons are present in the cavity (from a measurement drive or thermal occupation), the qubit frequency shifts:

```
ωₐ → ωₐ + 2nχ
```

This is the AC (dynamic) Stark shift — proportional to photon number n.

Consequence for measurement: the measurement drive that reads out the qubit *also* shifts the qubit frequency. This is quantum back-action — learning about the qubit state disturbs the qubit's phase. It's demanded by the Heisenberg uncertainty principle: extracting information about σz must introduce uncertainty somewhere else.

The measurement-induced dephasing rate:
```
Γ_meas = 2nκχ²/(Δ² + κ²/4 + χ²)
```

This shows there's a fundamental trade-off: larger χ gives better signal (bigger frequency shift) but also causes faster dephasing.

---

## Critical photon number

The dispersive approximation requires ng/Δ ≪ 1. Define:

```
ncrit = Δ²/4g²
```

Above ncrit, the Taylor expansion diverges and you return to the resonant regime. In practice, measurement drives must stay below ncrit. This sets a hard upper limit on probe power.

---

## Strong dispersive: from blurred to resolved

**Weak dispersive (χ < γ):**  
The Stark shift per photon (2χ) is smaller than the qubit linewidth (γ). Photons blur the qubit spectrum into a broader peak. You can still do QND readout of the qubit state (using many photons to average over the Stark fluctuations) but you can't resolve photon number.

**Strong dispersive (χ > γ, also χ > κ):**  
The Stark shift per photon is larger than both the qubit and cavity linewidths. Each photon number n produces a distinct, resolvable peak in the qubit spectrum at frequency ωₐ - 2nχ. You can read off the photon number distribution.

This is the photon number splitting result in Ch. 8 — roughly 10 resolved peaks observed.

---

## Connections to my background

The dispersive readout is a **state observer** in control theory terms. The qubit is the hidden state, the cavity is the output channel. The dispersive coupling is the output matrix C (in state-space: ẋ = Ax + Bu, y = Cx + Du). The QND condition is equivalent to the output matrix not feeding back into the state equation — a unilateral coupling.

The AC Stark shift is equivalent to a parameter variation (qubit frequency shifts when drive is on). Measurement-induced dephasing is the quantum analogue of measurement noise in a Kalman filter — you gain state information at the cost of injecting uncertainty into the state.

The trade-off between information gain and back-action is a quantum version of the observer uncertainty principle in classical estimation theory, but with a hard bound set by quantum mechanics rather than engineering choices.

---

## Open questions

- How does the optimal measurement strategy change if you want to maximise readout fidelity vs minimise back-action? (Related to quantum Bayesian and quantum trajectory theory)
- Can you do feedback — measure the cavity output continuously and use the result to correct the qubit state in real time? (Yes — quantum feedback control, e.g. Wiseman & Milburn — directly relevant to QuMaC-style experiments)
- What happens to readout fidelity when T₁ is comparable to the measurement time? (Single-shot fidelity analysis — addressed in Ch. 9)
