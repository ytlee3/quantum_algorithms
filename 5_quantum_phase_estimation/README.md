 
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


3. Inverse Quantum Fourier Transformation ($QFT^{-1}$, implemented as the QFT circuit but in the reverse order) 

`Recall QFT` ($N = 2^n$)

$QFT_N |k \rangle = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} e^{2 \pi i jk/N} |j\rangle $

$QFT_N^{-1} |k \rangle = \frac{1}{\sqrt{N}} \sum_{j=0}^{N-1} e^{-2 \pi i jk/N} |j\rangle $

$|\psi_3 \rangle = \frac{1}{\sqrt{2^n}} \sum_{k=0}^{2^n-1} e^{-2 \pi i jk/2^n} \frac{1}{\sqrt{2}^n} \sum_{j=0}^{2^n-1} e^{2 \pi i \phi j} |j\rangle$



## Reference ## 

Kitaev, A. Yu. "Quantum measurements and the Abelian stabilizer problem." arXiv preprint quant-ph/9511026 (1995).

