## Problem statement 

We are given an oracle function $f$, such that $f(x)$ is either a one-to-one or a two-to-one function. 
If $f(x)$ is a two-to-one function, it is promised that there exists a non-zero bitstring $b$ such that for any $x_1$ and $x_2$, if $f(x_1) = f(x_2)$, then $x_1 = x_2 \oplus b$.
Our goal is to find out if $f(x)$ is one-to-one or two-to-one function by finding the bitstring $b$.

In general, the worst-case number of trials required to determine the property of $f(x)$ is $2^{n-1}+1$, which is the same as Deutsch-Jozsa algorithm.


## Quantum algorithm 
Here is the quantum circuit for solving Simon's problem, let's check out the wavefunction step by step.

<img width="827" height="413" alt="The-quantum-circuit-corresponding-to-the-Simons-algorithm" src="https://github.com/user-attachments/assets/1e59fb97-a925-4362-aa90-5ceb101f44f9" />


1. First preparing n $|0\rangle$ state and the other n $|0\rangle$ state

$|\psi_0 \rangle = |0\rangle^{\otimes n} |0\rangle^{\otimes n}$

2. After applying the Hadamard gate, the wavefunction will occupy all basis states with equal probability, and we use x to denote the basis in numerical form. For example, $|0\rangle = |00...00\rangle, \ |1\rangle=|00...01\rangle, \ |2\rangle$ 
   
$|\psi_1 \rangle  = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} |x\rangle |0\rangle^{\otimes n} = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} |x\rangle |0\rangle^{\otimes n} $ 

3. We have the function $f$ (quantum oracle) that do the dot product between s and x 

$|\psi_2 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} |x\rangle | 0^{\otimes n} \oplus f(x) \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} |x\rangle | f(x) \rangle $

4. Applying n Hadamard gates to the first half qubit with Hadamard transformation $H^{\otimes n} |k\rangle =  1/\sqrt{2^n} \sum_{j=0}^{2^n-1} (-1)^{k \cdot j} |j\rangle$, where $k \cdot j = k_0j_0 \oplus k_1j_1 \oplus ... \oplus k_{n-1}j_{n-1}$ is the sum of the bitwise product

$|\psi_3 \rangle =  \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1}  |x\rangle | f(x) \rangle =  \frac{1}{\sqrt{2^n}} \sum_{x=0}^{2^n-1}  [ \frac{1}{\sqrt{2^n}} \sum_{j=0}^{2^n-1} (-1)^{x \cdot j} |j\rangle ] | f(x) \rangle =  \sum_{j=0}^{2^n-1} |j \rangle  [\frac{1}{2^n} \sum^{2^n-1}_{x=0} (-1)^{x \cdot j} |f(x)\rangle]$


5. When measuring the first n qubit, the probability of measuring the state  $|j\rangle $ is 
$|| \frac{1}{2^n} \sum^{2^n-1}_{x=0} (-1)^{x \cdot j} |f(x)\rangle ||^2 $

Condition one: if f(x) is an one-to-one function 

The measured probability will be $\frac{1}{2^n}$

 
 
 
 and we have  $|\psi_3 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)} H^{\otimes n} |x\rangle |-\rangle$. Due to the phase kickback, we ignore the state at the last qubit $|-\rangle$ first and let's take a look of the hadamard transformation.

$H^{\otimes n} |k\rangle =  1/\sqrt{2^n} \sum_{j=0}^{2^n-1} (-1)^{k \cdot j} |j\rangle$, where $k \cdot j = k_0j_0 \oplus k_1j_1 \oplus ... \oplus k_{n-1}j_{n-1}$ is the sum of the bitwise product

$|\psi_3 \rangle = \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{f(x)} H^{\otimes n} |x\rangle =  \frac{1}{\sqrt{2^{n}}} \sum_{x=0}^{2^n-1} (-1)^{x \cdot s} \[ \frac{1}{\sqrt{2^n}} \sum_{j=0}^{2^n-1} (-1)^{x \cdot j} |j\rangle \] =  \sum_{j=0}^{2^n-1}  \[ \frac{1}{2^{n}} \sum_{x=0}^{2^n-1} (-1)^{(x \cdot (s \oplus j))} \] |j\rangle  $

when $s=j$, $s \oplus j = |0\rangle$, where $|0\rangle \cdot |x\rangle$ is always 0, phase factor = 0, $|\psi_3 \rangle = |s \rangle$

When $s \neq j$, $s \oplus j \neq |0\rangle$, and since $x$ will go through all possible bitstrings, $(s \oplus j) \cdot x$ will result in an equal number of 0s and 1s (try it with a 3-qubit state and you will see). Consequently, the probability for the corresponding bitstring will be zero.

Therefore, when we measure, the measurement outcome will only correspond to the case where $|s\rangle = |j\rangle$.

### Reference 

Bernstein, Ethan, and Umesh Vazirani. "Quantum complexity theory." Proceedings of the twenty-fifth annual ACM symposium on Theory of computing. 1993.
   
