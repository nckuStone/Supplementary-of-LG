# Supplementary Material for the Quantum Logarithm Circuit

This repository provides the supplementary material for the paper:

**Resource-Efficient Fixed-Point Quantum Logarithm Circuit with Analytically Derived Error Bounds**

The complete circuit-level error analysis and its derivation are provided in [`Appendix.pdf`](./Appendix.pdf).

## Contents

- `Appendix.pdf`: Detailed error analysis of the proposed fixed-point quantum base-2 logarithm circuit.
- QASM files: Circuit QASM files for the experimental cases listed in `LG_Table_ExperimentalResults.png`.

## Experimental QASM Files

The experimental cases are summarized in the following table.

<p align="center">
  <img src="./LG_Table_ExperimentalResults.png" alt="Experimental results of the proposed logarithm circuit" width="450">
</p>

For each row in the table, the corresponding QASM filename follows the format

```text
LG_I_F_X_int.qasm
```

where:

- `I` denotes the number of integer bits of the input.
- `F` denotes the number of fractional bits of the input and output.
- `X_int` denotes the integer encoding of the fixed-point input value.

For example, a row with `I = 8`, `F = 32`, and `X_int = 61` corresponds to the file

```text
LG_8_32_61.qasm
```

## Simulation with SliQSim

The provided QASM files can be simulated using **SliQSim**, a high-performance BDD-based quantum circuit simulator.

A typical workflow is:

1. Select the QASM file corresponding to the target case in `LG_Table_ExperimentalResults.png`.
2. Run the selected QASM file using SliQSim.
3. Read the output register `lgX`.
4. Interpret `lgX` using the fixed-point output format described below.

## Output Format

The circuit output register is denoted by `lgX`. 

It represents `lgX` in the fixed-point format
Q_{(⌈lg(n+1)⌉+1).F},
where 
\(n = I + F\).

Let
m = ⌈lg(n+1)⌉+1.

Then the output register `lgX` contains \(m+F\) bits:

```text
lgX = [integer part: m bits][fractional part: F bits]
```

That is, the last \(F\) bits are the fractional part, and the remaining higher-order bits are the integer part.

---

### References

* **SliQSim Repository**: [https://github.com/NTU-ALComLab/SliQSim](https://github.com/NTU-ALComLab/SliQSim)
