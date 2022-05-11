## Problem Statement
You are given an array of size n containing integers. Design a linear time algorithm to find the sub-array (not necessarily contiguous) of maximum length such the values are non-decreasing.
___
## Problem Definition
$a_i$ := $i'th$ number in the array
$S_i$ := the non-decreasing sub-array of maximum length _ending at_ $i$, including it
$\Omega_i$ := the length of $S_i$
___
## Recurrence Relation
Stand at $a_i$ . The subsequence ending at $i$ either connects to a previous sub-array, or starts a new one. If it extends from a previous sub-sequence, it must extend from the longest previous sub-sequence. Otherwise, the length is just 1.
___
## Recursive Algorithm
Base Case:
* $i$ = 0, $\Omega_i$ = 0 {there are no elements in the sub-array}
 
Recursive Case:
$$
\begin {align} \quad
& K \in k,\; \Omega_K = max(\Omega_k)\\ 
&\Omega_i = 
	\begin {cases}
		\Omega_{K} + 1 &|\quad \exists \; k < i \; :a_i >= a_{k} \\
		1 &|\quad \nexists \; k < i \; :  a_i >= a_{k}
	\end {cases}
\end {align}
$$
Going back to search for the ideal $k$ will be $O(n)$ in the worst case, giving us a complexity of $O(n^2)$
___
## Runtime Analysis

| i          | 1   | 2   | 3   | 6   | 2   | 1   | 5   | 9   |
| ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
| $\Omega_i$ | 1   | 2   | 3   | 4   | 3   | 2   | 4   | 5    |
___
