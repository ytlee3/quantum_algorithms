 
## Introduction ## 

We will like to perform the discrete Fourier transofmration using quantum computer: $(x_0, x_1, ...., x_{N-1}) \rightarrow (y_0, y_1, ...., y_{N-1}) $


Classical DFT is described as: $y_k = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} x_j e^{-2 \pi i (j*k)/N}$

Similary, for the quantum version of DFT, we start with the state $|x\rangle = \sum^{N-1}_{j=0} x_j |j \rangle$ and map it to $|y\rangle = \sum^{N-1} _{j=0} y_j |j\rangle$

where  $y_k = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} x_j e^{2 \pi i (j*k)/N} = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} x_j \omega_N^{jk}$, where $\omega = e^{2\pi i /N}$ is an N-th root of unity. Noted that the convention of sign in DFT varys. The corresponding inverse DFT is described as $x_k =\frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} y_j \omega_N^{-jk}$.

Let's take one qubit for example, we have $|\psi \rangle = \alpha |0\rangle + \beta |1\rangle$

$y_0 = \frac{1}{\sqrt{2}} (\alpha \omega^{ (0 * 0) /2} + \beta \omega^{( 0* 1) /2}) = \frac{1}{\sqrt{2}} (\alpha + \beta) $, $y_1 = \frac{1}{\sqrt{2}} (\alpha \omega^{ (0* 1) /2}) + \beta \omega^{(1*1)/2}) = \frac{1}{\sqrt{2}} (\alpha - \beta)$

QFT $|\psi \rangle = \frac{1}{\sqrt{2}} (\alpha+\beta) |0\rangle + \frac{1}{\sqrt{2}} (\alpha-\beta) |1\rangle$, where the QFT gate is the Hadamard gate.

We can also approach this in the matrix form, again, $\omega = e^{2\pi i /N}$

$$
F_{N}={\frac {1}{\sqrt {N}}}
\begin{pmatrix}
1&1&1&1&\cdots &1 \\ 
1&\omega &\omega ^{2}&\omega ^{3}&\cdots &\omega ^{N-1} \\\
1&\omega ^{2}&\omega ^{4}&\omega ^{6}&\cdots &\omega ^{2(N-1)} \\ 
1&\omega ^{3}&\omega ^{6}&\omega ^{9}&\cdots &\omega ^{3(N-1)} \\ 
\vdots &\vdots &\vdots &\vdots &\ddots &\vdots \\
1&\omega ^{N-1}&\omega ^{2(N-1)}&\omega ^{3(N-1)}&\cdots &\omega ^{(N-1)(N-1)}
\end{pmatrix}
$$

In the case of one-qubit DFT: 


## Quantum algorithm 
Here is the quantum circuit for solving Simon's problem, let's check out the wavefunction step by step.
