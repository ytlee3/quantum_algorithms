## Problem statement 

We are given an oracle function $f$, such that $f(x)$ evaluates the dot product between x and the secret string s.

$f(x) = x \cdot s = x_0s_0 \oplus x_1s_1 \oplus ... \oplus x_{n-1}s_{n-1}$

Our goal is to find out the secret string s. In the worst-case scenario, we need to run the query n times to obtain the entire secret string.


## Quantum algorithm 
Here is the quantum circuit for Bernstein-Vazirani algorithm, let's check out the wavefunction step by step.

<img width="405" height="421" alt="figure" src="https://github.com/user-attachments/assets/e617ea19-78f1-4829-8193-6d9ff30ce25f" />

1. First preparing n $|0\rangle$ state and one $|1\rangle$ state

$|\psi_0 \rangle = |0\rangle^{\otimes n} |1\rangle$

2. After applying the Hadamard gate, the wavefunction will occupy all basis states with equal probability, and we use x to denote the basis in numerical form. For example, $|0\rangle = |00...00\rangle, \ |1\rangle=|00...01\rangle, \ |2\rangle = |00...10 \rangle$, $|x\rangle = |int_2(x)\rangle$ 
   
$|\psi_1 \rangle = \frac{1}{\sqrt{2^{n+1}}} \sum_{x=0}^{2^n-1} |x\rangle (|0\rangle -|1\rangle) = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} |x\rangle |-\rangle$

3. We have the function $f$ (quantum oracle) can map $|x\rangle|y\rangle$ to $|x\rangle|y\oplus f(x)\rangle$

$|\psi_2 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} |x\rangle |- \oplus f(x) \rangle$

if $f(x) =0$, $|x\rangle |- \oplus f(x) \rangle = (|0\oplus 0 \rangle - |1 \oplus 0\rangle ) / \sqrt{2}=|-\rangle$, if $f(x) =1$, $|x\rangle |- \oplus f(x) \rangle = (|0\oplus 1 \rangle - |1 \oplus 1\rangle ) / \sqrt{2}= - |-\rangle$ 

$U_f$ has propertis of phase inversion $|\psi_2 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)}|x\rangle |-\rangle$

4. Applying n Hadamard gates again and we have  $|\psi_3 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)} H^{\otimes n} |x\rangle |-\rangle$. Due to the phase kickback, we ignore the state at the last qubit $|-\rangle$ first and let's take a look of the hadamard transformation.

$H^{\otimes n} |k\rangle =  1/\sqrt{2^n} \sum_{j=0}^{2^n-1} (-1)^{k \cdot j} |j\rangle$, where $k \cdot j = k_0j_0 \oplus k_1j_1 \oplus ... \oplus k_{n-1}j_{n-1}$ is the sum of the bitwise product

$|\psi_3 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)} H^{\otimes n} |x\rangle =  \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)} \[ \frac{1}{\sqrt{2^n}} \sum_{j=0}^{2^n-1} (-1)^{x \cdot j} |j\rangle \] =  \sum_{j=0}^{2^n-1}  \[ \frac{1}{2^{n}} \sum_{x=0}^{2^n-1} (-1)^{f(x)}  (-1)^{x \cdot j} \] |j\rangle  $

Based on the above equation, the probability of measuring the state $|j\rangle$ is $|\frac{1}{2^{n}} \sum_{x=0}^{2^n-1} (-1)^{f(x)}  (-1)^{x \cdot j} |^2$

The probability of measuring $j= |0\rangle = |0\rangle^{\otimes n}$ is $|j\rangle$ is $|\frac{1}{2^{n}} \sum_{x=0}^{2^n-1} (-1)^{f(x)}  |^2$

if the $f(x)$ is constant then the measured probability is one, if the $f(x)$ is balanced then the measured probability is zero.
   
