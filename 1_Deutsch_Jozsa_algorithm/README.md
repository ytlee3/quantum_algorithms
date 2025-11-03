## Problem statement 

We are given a hidden Boolean function $f$ in a quantum computer (oracle). This function takes a bitstring as input and outputs either 0 or 1 for each bit.

$f({x_0, x_1, x_2,..., x_n}) \rightarrow$ 0 or 1 for each bit, where $x_n$ is 0 or 1 

We assume that the function is either constant or balanced. A constant function returns all 0s or all 1s for any input, while a balanced function returns 0 for half of the possible inputs and 1 for the other half.
Take 2 qubits as an example. If our input is $01$, the possible outputs could be

$f_1(01) =00$, $f_2(01) =01$, $f_3(01) =10$, $f_4(01) =11$. 
 
In this case, $f_1$ and $f_4$ are constant functions since they return all 0s or all 1s, respectively.
$f_2$ and $f_3$ are balanced functions, as they output half 0s and half 1s depending on the input.
In the worst case, to determine whether this hidden Boolean function is constant or balanced, we need to test the first qubit twice and the second qubit once (since the last outcome is already known, we don’t need to test it twice).
In general, the worst-case number of trials required to determine the property of $f(x)$ is $2^{n-1}+1$


## Quantum algorithm 
Here is the quantum circuit for Deutsch-Jozsa algorithm, let's check out the wavefunction step by step.

<img width="600" height="400" alt="Screenshot 2025-10-28 at 21 44 37" src="https://github.com/user-attachments/assets/4f728fcf-6cc1-4ef2-847e-ce003e4839dd" />

1. $|\psi_0 \rangle = |0\rangle^{\otimes n} |1\rangle$

2. $|\psi_1 \rangle = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1} |x\rangle (|0\rangle -|1\rangle)$
