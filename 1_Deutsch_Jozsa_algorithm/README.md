## Problem statement 

We are given a hidden boolean function $f$ in quantum computer (oracle). This function takes bitstring as input and output either 0 or 1 for each bit. 

$f({x_0, x_1, x_2,..., x_n}) \rightarrow$ 0 or 1 for each bit, where $x_n$ is 0 or 1 

We hope that the function is either a constant function or a balanced. Constant function return all 0 or all 1 for any input and balanced function return 0 for half of the input and 1 for the other half.



Take 2 qubits for example, if our input is 01, the possible output could be $f_1(01) =00$, $f_2(01) =01$, $f_3(01) =10$, $f_4(01) =11$. In this case, $f_1$ and $f_4$ are constant functions as they return all 0 or all 1. $f_2$ and $f_3$ are balanced function as they output half of the 0 and half of the 1 based on the input. The worst case senerio to check if this hidden boolen function is either constant or balanced, we have to test the first qubit 2 times plus the second qubit once (we know the last information, don't have to do it twice).

General worst case: we need $2^{n-1}+1$ trial to certain the property of $f(x)$ 
