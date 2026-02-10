 
## Introduction ## 

Quantum phase estimation (QPE) is a quantum algorithm to evaluate the phase $\phi$ corresponding to an eigenvalue $e^{2\pi i \phi}$ of a given unitary operator $U$, such that 

$$ 
U |\psi \rangle = e^{2\pi i \phi} |\psi \rangle 
$$

This algorithm was first introduced by Kitaev. It involves the inverse QFT and is a central routine in Shor’s algorithm and Quantum Amplitude Estimation.

## Quantum algorithm 
<img width="1920" height="793" alt="PhaseCircuit" src="https://github.com/user-attachments/assets/b1f3089b-6ee2-43fd-8ea1-edad4bd35934" />

Here is the quantum circuit for performing quantum fourier transformation, let's check out the wavefunction step by step.
$R_k$ is the dyadic rational phase gate

$$
R_k = 
\begin{pmatrix}
1 & 0 \\ 
0 & e^{2 \pi i /2^k} 
\end{pmatrix}
$$

<img width="3582" height="1194" alt="Q_fourier_nqubits" src="https://github.com/user-attachments/assets/4b74666a-519d-464f-a604-9219d7193afa" />

We check the first qubit first as the other follows the same way to derive. 

1. After Hadarmard gate $|\psi_1 \rangle = \frac{1}{\sqrt{2}} (|0\rangle + e^{2\pi i 0. x_1} |1\rangle)$ if $|x_1 \rangle = 0$, the factor =1 and = -1 when $|x_1\rangle =1$

2. if $|x_2 \rangle = |0\rangle$ , $(|0\rangle+ e^{2 \pi i 0.x_1 0 |1\rangle}) / \sqrt{2}$ (nothing really change).

if $|x_2 \rangle = |1 \rangle$

$$
\frac{1}{\sqrt{2}}
\begin{pmatrix}
1 & 0 \\
0 & e^{2 \pi i /2^2} \\
\end{pmatrix} 
[
\begin{pmatrix}
1 \\
0 
\end{pmatrix} 
+
\begin{pmatrix}
0 \\
e^{2 \pi i 0.j_n}
\end{pmatrix} ]
= \frac{1}{\sqrt{2}}
(|0\rangle + e^{2 \pi i (0.x_1 + 0.01)} |1 \rangle )
= \frac{1}{\sqrt{2}}
(|0\rangle + e^{2 \pi i (0.x_1 + 0.0x_2)} |1 \rangle )
= \frac{1}{\sqrt{2}}
(|0\rangle + e^{2 \pi i (0.x_1x_2)} |1 \rangle )
$$

3. when we keep doing the controlled-rotation gate, the final $|\psi \rangle = (|0\rangle + e^{2 \pi i 0.j_1j_2...j_n} |1\rangle)$

4. Do the same procedure for every single qubit and we will get the QFT of the bitstring.

5. Don't forget the swap operation at the end to flip the bitstring order (convention)

Rotation angle $|2^{-1}, 2^{-2}, 2^{-3},...2^{-n} \rangle$. Take $|1101\rangle$ for example, it will be [0.1, 0.01, 0.101, 0.1101], the corresponding rotation angle in the Fourier basis is [1/2, 1/4, 1/2+1/8, 1/2+1/4+1/16]

## Reference ## 

Kitaev, A. Yu. "Quantum measurements and the Abelian stabilizer problem." arXiv preprint quant-ph/9511026 (1995).

