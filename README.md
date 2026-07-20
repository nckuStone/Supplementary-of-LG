# Supplementary Material for the Quantum Logarithm Circuit

This repository provides the supplementary material for the paper:

**Resource-Efficient Fixed-Point Quantum Logarithm Circuit with Analytically Derived Error Bounds**

The complete circuit-level error analysis and its derivation are provided in [`Appendix.pdf`](./Appendix.pdf).

## Contents

- `Appendix.pdf`: Detailed error analysis of the proposed fixed-point quantum base-2 logarithm circuit.
- QASM files: Circuit QASM files for the experimental cases listed in `LG_Table_ExperimentalResults.png`.
- `PIC/Circuit Width versus F.png`: Width-scaling comparison with prior quantum logarithm circuits.
- `PIC/Circuit Depth versus F.png`: Depth-scaling comparison with prior quantum logarithm circuits.

## Experimental QASM Files

The experimental cases are summarized in the following table.

<p align="center">
  <img src="./PIC/LG_Table_ExperimentalResults.png" alt="Experimental results of the proposed logarithm circuit" width="450">
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

## Additional Parameter-Choice Cases

For the case `LG_8_32_61.qasm`, two additional QASM files are provided to illustrate the effect of unbalanced parameter choices:

- `LG_8_32_61_N2.qasm`: The Taylor order is fixed to N=2, requiring more range-reduction rounds M=17 (MN>=(F+2)).
- `LG_8_32_61_M2.qasm`: The number of range-reduction rounds is fixed to M=2, requiring more Taylor terms N=17 (MN>=(F+2)).

These two cases can still achieve the same target error bound, but they require more circuit resources than the balanced choice. This demonstrates why the proposed parameter selection balances M and N.

Except for these two additional illustrative cases, the experimental QASM files follow the balanced parameter selection described in the paper, namely M=N=Theta(F^0.5).

## Resource-Scaling Comparison

To provide a more intuitive comparison with prior quantum logarithm circuits, we include width- and depth-scaling plots.

Bhaskar *et al.*'s LN module achieves O(2^-F) accuracy with width O(F^2 log2(F)) and depth O(F^3 log2(F)).

Wang *et al.* propose a qFBE-based logarithm circuit with width O(F^2) and depth O(F^3). Their work does not provide an analytical error bound and instead relies on numerical evaluation.

For the proposed logarithm circuit, we choose

```text
M = N = ceil(sqrt(F + 2))
p = F + M + 5
```

This parameter choice achieves O(2^-F) accuracy with asymptotic width O(F^1.5) and depth O(F^2.5).

For a more implementation-oriented estimate, a square-root circuit with `2 + 2p` input bits contributes width O(2 + 2p) and depth O((2 + 2p)^2 / 2). A multiplier with `2 + p` input bits contributes width O(2(2 + p)) and depth O((2 + p)^2).

Let 
c = ceil(sqrt(F + 2)).
Since `M = N = c` and `p = F + c + 5`, the estimated width is

```text
W_LG(F) = M(2p + 2) + N(2p + 4)
        = c(4F + 4c + 26).
```

The estimated depth is

```text
D_LG(F) = (1/2)M(2p + 2)^2 + N(p + 2)^2
        = c[2(F + c + 6)^2 + (F + c + 7)^2].
```

The following figures compare these estimates with the asymptotic resource trends of the prior circuits.

<p align="center">
  <img src="./PIC/Circuit%20Width%20versus%20F.png" alt="Circuit width versus F" width="450">
</p>

<p align="center">
  <img src="./PIC/Circuit%20Depth%20versus%20F.png" alt="Circuit depth versus F" width="450">
</p>

The hidden constants in the asymptotic complexities of the prior circuits are normalized to one. Therefore, these figures illustrate scaling trends rather than exact circuit-resource comparisons.

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
