
## Introduction ## 

We will like to perform the discrete Fourier transofmration using quantum computer: $(x_0, x_1, ...., x_{N-1}) \rightarrow (y_0, y_1, ...., y_{N-1}) $


Classical DFT is described as: $y_k = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} x_j e^{-2 \pi i (j*k)/N}$

Similary, for the quantum version of DFT, we start with the state $|x\rangle = \sum^{N-1}_{j=0} x_j |j \rangle$ and map it to $|y\rangle = \sum^{N-1} _{j=0} y_j |j\rangle$

where  $y_k = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} x_j e^{2 \pi i (j*k)/N} = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} x_j \omega_N^{jk}$


## Quantum algorithm 
Here is the quantum circuit for solving Simon's problem, let's check out the wavefunction step by step.
