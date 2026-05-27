# Circuit QED — Thesis Reading Notes

**Source:** Schuster, D.I. (2007). *Circuit Quantum Electrodynamics*. PhD Thesis, Yale University.  
**Reader:** Jassmaira Singh  
**Background:** B.Tech Electronics & Instrumentation, MIT Manipal  
**Started:** May 2026

---

## What this is

These are my personal reading notes from Schuster's 2007 Yale PhD thesis, one of the founding documents of circuit QED. The thesis demonstrates, for the first time, strong coupling between a superconducting qubit and a microwave cavity on a chip, and introduces experimental techniques (dispersive readout, photon number splitting, on-demand single photon generation) that now underpin essentially every superconducting quantum computer in existence.

I'm reading this as part of building background in quantum measurement and control, with a particular interest in how classical control engineering concepts (feedback, readout chains, state estimation) map onto quantum systems.

---

## Why Schuster 2007

- It is the primary experimental paper for circuit QED as a platform
- The transmon qubit, invented here, is used in IBM, Google, and most other superconducting quantum computers today
- The dispersive readout scheme introduced here is still the dominant measurement technique in the field
- It is unusually well-written for a physics thesis, Schuster explains intuition, not just equations

---

## Repo structure

```
chapter-notes/      ← per-chapter summaries, key ideas, open questions
concepts/           ← deep dives on individual concepts that cut across chapters
summary.md          ← high-level "what I learned" what I'd say if asked
```

---

## Reading status

| Chapter | Title | Status |
|---------|-------|--------|
| Ch. 1 | Introduction | ✅ Done |
| Ch. 2 | Cavity Quantum Electrodynamics | ✅ Done |
| Ch. 3 | Cavity QED with Superconducting Circuits | ✅ Done |
| Ch. 4 | Decoherence in the Cooper Pair Box | 🔲 Not started |
| Ch. 5 | Design and Fabrication | 🔲 Not started |
| Ch. 6 | Cryogenic & Microwave Engineering | 🔲 Not started |
| Ch. 7 | Characterisation of cQED | 🔲 Not started |
| Ch. 8 | Cavity QED Experiments with Circuits | 🔲 Not started |
| Ch. 9 | Time Domain Measurements | 🔲 Not started |
| Ch. 10 | Conclusions and Outlook | 🔲 Not started |

---

## The one-paragraph summary

Schuster took the idea of trapping an atom inside a mirror box (cavity QED) and rebuilt it on a microchip, a superconducting circuit as the artificial atom, a strip of wire as the cavity. He showed that the atom and microwave photons could exchange energy coherently faster than either could decay (strong coupling), that you could read the qubit's state by measuring a frequency shift in the cavity without disturbing the qubit (dispersive readout), that individual photon numbers in the cavity could be resolved spectroscopically (photon number splitting), and that exactly one photon could be emitted on demand. The transmon qubit, introduced here to overcome charge noise, is now the hardware foundation of the quantum computing industry.

---

*Notes are written in plain language first, equations second. Open questions are tracked explicitly.*
