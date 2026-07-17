# Supplementary Material for the Quantum Logarithm Circuit

This repository provides the supplementary material for the paper:

**Resource-Efficient Fixed-Point Quantum Logarithm Circuit with Analytically Derived Error Bounds**

The complete circuit-level error analysis and its derivation are provided in [`Appendix.pdf`](./Appendix.pdf).

## Contents

- `Appendix.pdf`: Detailed error analysis of the proposed fixed-point quantum base-2 logarithm circuit.
- `LG_Table_ExperimentalResults.png`: Experimental results table for representative fixed-point inputs.
- `*.qasm`: QASM circuit files corresponding to the experimental cases listed in `LG_Table_ExperimentalResults.png`.

## QASM Circuit Files

This repository provides the QASM files used for circuit-level simulation. These files are intended to be simulated using **SliQSim**, a high-performance BDD-based quantum circuit simulator.

The QASM files follow the naming convention:

```text
LG_I_F_X_int.qasm
