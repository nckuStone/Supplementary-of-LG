# Supplementary Material for the Quantum Logarithm Circuit

This repository provides the supplementary material for the paper:

**Resource-Efficient Fixed-Point Quantum Logarithm Circuit with Analytically Derived Error Bounds**

The complete circuit-level error analysis and its derivation are provided in [`Appendix.pdf`](./Appendix.pdf).

## Contents

- `Appendix.pdf`: Detailed error analysis of the proposed fixed-point quantum base-2 logarithm circuit.
- QASM files: Quantum circuit descriptions used for the experimental cases listed in `LG_Table_ExperimentalResults.png`.

## Experimental QASM Files

This repository provides the generated QASM files for the logarithm-circuit experimental cases. These QASM files can be simulated using **SliQSim**, a high-performance BDD-based quantum circuit simulator.

The experimental cases are summarized in the following table:

![Experimental results of the proposed logarithm circuit](./LG_Table_ExperimentalResults.png)

For each row in the table, the corresponding QASM filename follows the format

```text
LG_I_F_X_int.qasm


---

### References
* **SliQSim Repository**: [https://github.com/NTU-ALComLab/SliQSim](https://github.com/NTU-ALComLab/SliQSim)

