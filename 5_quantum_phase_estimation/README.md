 
## Introduction ## 

Quantum phase estimation (QPE) is a quantum algorithm to evaluate the phase $\phi$ corresponding to an eigenvalue $e^{2\pi i \phi}$ of a given unitary operator $U$, such that 

$$ 
U |\psi \rangle = e^{2\pi i \phi} |\psi \rangle 
$$

This algorithm was first introduced by Kitaev. It involves the inverse QFT and is a central routine in Shor’s algorithm and Quantum Amplitude Estimation.

## Quantum algorithm 

Here is the quantum circuit for performing quantum phase estimation, let's check out the wavefunction step by step.

<img width="982" height="474" alt="T7EIw" src="https://github.com/user-attachments/assets/63353145-8758-4fd3-b2ab-ca62321e1d17" />


1. After Hadarmard gate $|\psi_1 \rangle = H^{\otimes n} |0\rangle^{\otimes n} \otimes |\psi \rangle = |+\rangle^{\otimes n} \otimes |\psi \rangle= \frac{1}{2^{n/2}} \sum_{j=0}^{2^n-1}|j\rangle \otimes |\psi \rangle$
   (we switch to the binary representation j)

2. For the controlled-U gate

$|\psi_2 \rangle = \frac{1}{\sqrt{2}^n}  \[ (|0\rangle + U^{2^n-1} |1\rangle) \otimes (|0\rangle + U^{2^n-2} |1\rangle) \otimes ... \otimes (|0\rangle + U^{2^0} |1\rangle) \]  \otimes |\psi \rangle$  

Using the binary representation, we can rewrite the $\psi_2$ as 

$|\psi_2 \rangle = \frac{1}{\sqrt{2}^n} \sum_{j=0}^{2^n-1} e^{2 \pi i \phi j} |j\rangle \otimes |\psi \rangle$

Take 3 qubits for example

$|\psi_2 \rangle = \frac{1}{\sqrt{2}^3} \[ (|0\rangle + U^{2^2} |1\rangle) \otimes (|0\rangle + U^{2^1} |1\rangle)  \otimes (|0\rangle + U^{2^0} |1\rangle) \] \otimes |\psi \rangle = 
\frac{1}{\sqrt{2}^3} \[ (|0\rangle + e^{2 \pi i \phi {2^2}} |1\rangle) \otimes (|0\rangle + e^{2 \pi i \phi {2^1}}  |1\rangle)  \otimes (|0\rangle +  e^{2 \pi i \phi {2^0}} |1\rangle) \] \otimes |\psi \rangle $

For $|7\rangle$ is $|111\rangle$  => $e^{2 \pi i  \phi 2^2} \otimes e^{2 \pi i  \phi 2^1} \otimes e^{2 \pi i  \phi 2^0} |111 \rangle$ => $e^{2\pi i \phi j} |j\rangle $ 


3. Inverse Quantum Fourier Transformation ($QFT^{-1}$)

`Recall QFT` (N = 2^n)

$QFT_N |k \rangle = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} e^{2 \pi i jk/N} |j\rangle $

$QFT_N^{-1} |k \rangle = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} e^{-2 \pi i jk/N} |j\rangle $


4. if $|x_2 \rangle = |0\rangle$ , $(|0\rangle+ e^{2 \pi i 0.x_1 0 |1\rangle}) / \sqrt{2}$ (nothing really change).

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

